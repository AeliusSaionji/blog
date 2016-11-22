I've been searching for a long time, and I finally figured out how to generate a libnotify event from a udev rule _without_ hardcoding the username into the rule or script. The answer is actually pretty simple, and I'm very surprised I couldn't find the answer on any wiki or forum.

<!-- more -->

There was [this ArchWiki entry](https://wiki.archlinux.org/index.php?title=Udev&oldid=453707#Triggering_desktop_notifications_from_a_udev_rule) which is no help at all. The author seemed to think you could insert a `$USER` variable into here "once you understand the example". What? If your generic example contains hardcoded elements it's a horrible example! /vent

Moving on.

I thought I might be able to use this blog's tutorial on [how to start systemd services from udev](http://blog.fraggod.net/2015/01/12/starting-systemd-service-instance-for-device-from-udev.html) for my purposes, but that quickly got very complicated and confusing. It took me an embarrasingly long time to realize this approach still requires a hardcoded username implemented somewhere. Womp womp.

I got the basic framework for my solution with the help of [hackaday](http://hackaday.com/2009/09/18/how-to-write-udev-rules/). They still hardcode the user, but thinking about what they did here caused me to arrive at the solution.

In their `for` loop, they iterate through every instance of their notification daemon. While I was cleaning up their useless use of grep, I wondered what that `for` loop actually accomplishes; are they expecting to have more than one instance of their notification daemon running? That doesn't make sense. My notification daemon of choice, [dunst](https://github.com/knopwob/dunst), doesn't even let you run it more than once per user. At which point it occurred to me, if this script is run as root, I can repurpose this for loop to iterate the search for a notification daemon through logged in users! I had to look up the `who` command as I had never seen it before, and from here the problem is solved. I no longer need to figure out which users to run notify-send as, I run it for **every logged in user**. Which makes sense for hardware events- all logged in users _should_ be getting these notifications.

Now if only I could find a way to not hardcode the notification daemon.

`/usr/local/bin/power_notify`

	#!/bin/sh

	# Display a notification for each logged in user
	user_notify() {
		users=$(who | awk '{print $1}')
		for user in $users; do
			# find DBUS session bus
			pid=$(pgrep -u $user dunst)
			export DBUS_SESSION_BUS_ADDRESS=$(sed -z -e '/DBUS_SESSION_BUS_ADDRESS/!d' \
				-e 's/DBUS_SESSION_BUS_ADDRESS=//' /proc/$pid/environ)
			su -c - $user "$@"
		done
	}

	# udev 99-lowbat.rules
	case "$1" in
		"low")
			user_notify "notify-send -u normal 'Low Battery'" ;;
		"critical")
			user_notify "notify-send -u critical 'Low Battery' 'Find power soon!'" ;;
		"suspend")
			user_notify "notify-send -u critical 'Suspend Imminent' 'The system is going down in two minutes!'"
			sleep 120
			systemctl suspend ;;
		"hibernate")
			echo "not implemented" ;;
	esac

`/etc/udev/rules.d/99-lowbat.rules`

	SUBSYSTEM=="power_supply", KERNEL=="BAT0", ATTR{capacity}=="2[05]", ATTR{status}=="Discharging", RUN+="/usr/local/bin/power_notify low"
	SUBSYSTEM=="power_supply", KERNEL=="BAT0", ATTR{capacity}=="1[05]", ATTR{status}=="Discharging", RUN+="/usr/local/bin/power_notify critical"
	SUBSYSTEM=="power_supply", KERNEL=="BAT0", ATTR{capacity}=="[0-9]", ATTR{status}=="Discharging", RUN+="/usr/local/bin/power_notify suspend"

For whatever reason I haven’t abandoned Logitech’s “Gaming Software” yet. It works well enough, I’m lazy, and having the UI spell out what buttons are mapped to what is useful sometimes. Some time ago I came across a game that required more buttons to play than I had on my mouse (Hitman Absolution for the curious), so I was forced to put more effort into my setup.

<!-- more -->

I have no experience with Lua, and I don’t really intend to learn it. I threw this together, it works, that’s about as far as I care to go. The script turns button 10 on my mouse into a modifier, like shift or control keys. A modifier does nothing on its own, but it modifies the action of any button it is pressed in conjunction with. You access the scripting interface by right clicking the profile icon and clicking “Scripting”.

If this doesn't render correctly, here’s a sprunge for you: <http://sprunge.us/DYGT>

    --Proof of concept multi key press
    --The button must be unassigned in the gui and mapped here
    --in order to 'swallow' the default action when the modifier is pressed
    --Otherwise, both the default action and the new mod action will be sent

    Mod = 0

    function OnEvent(event, arg)
        OutputLogMessage("event = %s, arg = %s\n", event, arg)
    --Modifier is button 10
        if arg == 10 then
    		if event == "MOUSE_BUTTON_PRESSED" then
    			--OutputLogMessage("Mod \n")
    			Mod = 1
    		elseif event == "MOUSE_BUTTON_RELEASED" then
    			Mod = 0
    		end
    	--Button 7
        elseif arg == 7 then
    		if event == "MOUSE_BUTTON_PRESSED" then
    		--Mod action
    			if Mod == 1 then
    				PressKey("z")
    		--Normal action
    			elseif Mod == 0 then
    				PressKey("spacebar")
    			end
    		--Release all bindings on button released
    		elseif event == "MOUSE_BUTTON_RELEASED" then
    			ReleaseKey("spacebar")
    			ReleaseKey("z")
    		end
    	--Button 5
        elseif arg == 5 then
    		if event == "MOUSE_BUTTON_PRESSED" then
    		--Mod action
    			if Mod == 1 then
    				PressKey("f")
    		--Normal action
    			elseif Mod == 0 then
    				PressKey("lshift")
    			end
    		--Release all bindings on button released
    		elseif event == "MOUSE_BUTTON_RELEASED" then
    			ReleaseKey("lshift")
    			ReleaseKey("f")
    		end
    	--Button 6
        elseif arg == 6 then
    		if event == "MOUSE_BUTTON_PRESSED" then
    		--Mod action
    			if Mod == 1 then
    				PressKey("c")
    		--Normal action
    			elseif Mod == 0 then
    				PressKey("lctrl")
    			end
    		--Release all bindings on button released
    		elseif event == "MOUSE_BUTTON_RELEASED" then
    			ReleaseKey("c")
    			ReleaseKey("lctrl")  
    		end
    	end
    end

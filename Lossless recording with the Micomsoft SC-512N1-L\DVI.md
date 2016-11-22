I couldn't find much information online about lossless recording, and I had frustrating recording issues (frame drops & frame insertions) I just couldn't figure out. The only useful information I could find online was that recording issues are probably user error, not a card defect. Over the course of two days, I have perfected the process of lossless recording. Here are some codec benchmarks and instructions on how to avoid frame dropping and frame inserting.

These results aren't as thorough as I would have liked them to be- I was careless and didn't properly record which combinations had a frame drop/insertion. I used peak results instead of average, in part because the peak was never far from the average, I would think the peak is more useful in this context, and because I had no way of actually calculating the exact average. I only used one video for all of the tests, and the start/end times of the recordings were not exactly the same. 

<!-- more -->

Peak values recorded, not average. No special steps (see notes) were taken to prepare for recording.

## Trial 1

	Time: 2.00 minutes
	Program: AmaRecTV x86
	Source: 1080p60FPS, Super Smash Brothers 4 intro

### x264vfw | Single pass lossless | ultrafast | Keep input colorspace

	CPU: 24%
	Write: 38MB/s
	RAM: 530.45MB
	Size: 2.27 GB (2,438,367,232 bytes)


### UtVideo YUV422 BT.601 VCM | frame divide count 8 | Optimize for compression ratio

	CPU: 15%
	Write: 88MB/s
	RAM: 298.26MB
	Size: 7.02 GB (7,540,113,408 bytes)


### Lagarith | Use multithreading

	CPU: 23%
	Write: 69MB/s
	RAM: 315MB
	Size: 4.71 GB (5,068,206,080 bytes)


### AMV4 | DR3

	CPU: 7%
	Write: 45MB/s
	RAM: 283.8MB
	Size: 3.09 GB (3,318,808,576 bytes)

## Trial 2

	Time: 2.00 minutes
	Program: VirtualDub x64
	Source: 1080p60FPS, Super Smash Brothers 4 intro

### x264vfw | Single pass lossless | ultrafast | Keep input colorspace

	CPU: 23%
	Write: 37MB/s
	RAM: 559MB
	Size: 2.25 GB (2,427,280,374 bytes)

### UtVideo YUV422 BT.601 VCM | frame divide count: 8 | Optimize for compression ratio

	CPU: 15%
	Write: 67MB/s
	RAM: 1256MB
	Size: 5.70 GB (6,129,589,248 bytes)

### Lagarith | Use multithreading

	CPU: 20%
	Write: 50MB/s
	RAM: 140MB
	Size: 4.39 GB (4,720,989,678 bytes)

### AMV4 | DR3

	CPU: 6%
	Write: 42MB/s
	RAM: 127MB
	Size: 3.09 GB (3,320,348,912 bytes)

#### Notes

This is my very first foray into the world of capture cards and lossless recording.

With certain encoders, AmaRecTV's audio preview would frequently sound distorted, but the resulting recording would sound fine.

Lagarith has some serious frame insertion problems, when writing to my slow HDD @ ~100MB/s. On the subject of frame insertions, I have read from many sources that viewing the preview stream is the most likely source of frame drops/insertions. I believe this information is sorely outdated- I spent the better part of two days trying to diagnose recording woes, and at least as far as VirtualDub x64 is concerned, the one and only cause is an interruption in writing to the disk. Disabling the preview does not help at all, on my machine- the required power is just too insignificant.

What does help is writing to a RAM disk. In all of my experimentation, I cannot recall there being ANY drops or insertions when using a RAM disk. Granted, I only have 16GB to work with and this leaves me with under 10 minutes, but I think the reasonable assumption is that the limiting factor is writing to a disk. Now, although VirtualDub (and Process Hacker) claims to never write faster than 100MB/s at most, I sometimes will even experience issues when writing to my SSD, which has a sustained average write speed of 350MB/s. This leads me to believe that the encoding process does not like to share disk bandwidth even if there is plenty to spare.

Using Process Hacker to suspend the indexing service (and related services), and setting VirtualDub's process to high I/O priority (changes in process priority have no effect) allows me to write to my slowest disk with no problems. I also added VirtualDub as an exception to my antivirus, and if I do experience any issues I sort processes by I/O in descending order, and end the ones that are causing trouble.

It does look like x264 is the best encoder to use simply because it has the lowest write speed and smallest output file size (though nothing but the weakest preset is usable). Not just for the sake of manageable file sizes, but also because the less we use the disk, the less chance we have of encountering frame insertions/drops. That said, it does not always perform so well (its compression ratio is not significantly better than the others in some of my recordings) and its CPU utilization was not insignificant, so if you're low on processing power AMV4 might be worth the 30USD. AMV4's low overhead and low file size is suspiciously impressive. Also suspicious: I extracted a frame from a video encoded with x264, and extracted the same exact frame from a video encoded with AMV4. I cropped both images in the same exact way (to remove the AMV4 watermark) and compared the two images using [Visual Similarity Duplicate Images Finder](http://www.mindgems.com/products/VS-Duplicate-Image-Finder/VSDIF-About.htm). They were 99% identical. If both videos are lossless, and the extracted frame is not altered in any way (I extracted said frames to lossless png format), I don't understand why the images wouldn't be exactly identical. It might have been user error, or AMV4 might have a dirty secret. I don't know how to proceed with testing to figure out exactly what's happening.

I know for a fact that in different scenarios, the tested codecs might not be as effective as the numbers shown here. That said, x264 is usually either significantly better than the competition, or "merely" just as good: at worst, it isn't worse, at best, it's a lot better.

AMV4 supports detecting and writing "null frames"- a frame that is just a placeholder saying "show the previous frame here". I noticed this while recording a game that is actually slightly above 480p30FPS, but upscaled at 1080p60FPS. AMV4 produced half the file size of any other encoder, every time. This is because the XBox360 just sends the every frame twice when displaying 30FPS on 60Hz displays for a total of 60FPS. AMV4 recognized that literally half of the video is junk data- instead of recording two duplicate images, only one image is recorded and a placeholder (null frame) is created in the table of contents (so to speak) to tell video players to just display the previous frame. This is a nifty feature, but I believe it should be possible to just use x264 and remove every other frame in the video to just get the video in 30FPS. I should look into this and write up a tutorial...

#### Rant
Although not entirely related, I feel it would be remiss of me to not mention lossy screen recording programs. In a thread discussing capture cards, I have read an opinion from an individual on the internet, as recently as Jan 2015, that recording should "always be done with a capture card in a separate PC". For lossless recording, yes, probably. Recording in general? Hell no. For the exclusive use of streaming? *screams externally*. Software based screen recording solutions can have negligible overhead, particularly under Windows 8/8.1 which features a number of improvements that allows screen recorders to run with virtually no overhead. If your machine is old enough that you don't have the resources to record a game, it's probably time for a new gaming rig. A good quad core processor has 8 logical threads- simply put, you can accomplish tasks in parallel and recording a game shouldn't be an issue. Unless you require lossless video for professional video editing, don't waste money building a separate capture rig. Put that money aside for a new gaming rig. Use some of it to buy Mirillis Action!, a 30USD screen capture program with virtually no overhead and a comprehensive set of features. It looks stupid (as all programs that don't adhere to the standard UI conventions do), but it's well worth the cost. Don't pay for the streaming subscription though, unless you're feeling particularly charitable. Second best program for general recording, and first best program for streaming: OBS Open Broadcasting Software. Action! is idiot friendly, OBS might require some research to operate. At the time of writing, OBS also doesn't support recording in some colorspaces for whatever reason, and even I can tell some of the colors (particularly green) are just incorrect in the resulting video file. OBS used to have the ability to create lossless screen recordings; that feature no longer works, but it might be coming back in the rewrite. VirtualDub has some capacity for screen recording, but it's confusing and thoroughly under documented (and likely under developed). I wouldn't bother with FRAPs- even back in the day when it was THE recording solution, I always found it rather poorly programmed.

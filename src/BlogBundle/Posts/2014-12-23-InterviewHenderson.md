---
title: "Interview with Ian Henderson"
date:   2014-12-23
tags: MediaConch, Interview
---

# Interview with Ian Henderson

Date: 12/23/2014

Interviewers: Dave, Jerome, Tessa

D: Describe your background research into FFV1 and Matroska?

I: Collection of HDCam and HDCam SR tapes for one particular job. It was open at the time as to how we were going to transfer these to digital files.
Looked at lossy compressions, various other formats, but it seemed if we're going to try and capture as much information as we can, the best way is to go with lossless compression.  So that limited the amount of options that were available.  I looked at MXF and jpeg2000 and initially I was very keen; but that actual implementation isn't very standardized.

Perceived wisdom in archives is that you follow what the broadcasters are doing, and I don't think that's the best fit.

FFV1 seemed fairly easy and controllable option. There didn't seem to be anything negative about it in regards to preserving the original source and keeping it available for future transcriptions and migration.

The reason for using Matroska: supported FFV1, we wanted to preserve all the audio streams available on the tapes (4 for HDCam, 12 for HDCam SR) and it had good support for multi-stream, and the expanded capacity for metadata storage.

D: What tools are you using right now to work with FFV1 and/or Matroska?

I: Transcoded externally via the BBC. If I need to do any work with it, I use ffmpeg.  We haven't got an awful lot of a toolset. Whatever I come across that could be useful: tools for ID, categorization, migration. At the moment, MediaInfo for examining video, and one or two other tools. QCTools was mentioned.

D: What tools do you use for compliance checking?

I: Fairly limited.  We use Droid for ID, and MediaInfo, and basically we retrieve whatever metadata information is in there. FFprobe. Something we'll have to look at. Any advice would be appreciated.

No problems with FFV1; only problem we had was with previews of files.  But with FFV1, no problems. We have 125-150 digital files output from the tape, no problems at all. Largely for checking, it was a visual comparison with the H264.  Making sure all the footage was there, the audio streams were available.  Really a manual check process. We need to get more into performance software.

We only have source material. This was quite an unusual set in that it was the first time we've ever had videotape. We needed to find the best fit for that job.

Because we retrieve material from government department, it's unusual to receive media.  We're now getting more and more stitched file content that we're retrieving.

J: Do you use MediaInfo manually?

I:  Basically manually. We look at the files themselves or run an instance over a number of files using a Windows .bat file. There might be an implementation in our archival system, that would basically be running the same check.

I'll find out more about that system.

D: Do you move MediaInfo results into a db or store in a text file?

I:  We store it in an archival system. SDB. NYU uses it. The info is stored within the database, a mixture of technical and description.

D: What coding specs do you use when you're requesting FFV1/Matroska?

I: There weren't that many options we were worried about with FFV1. We wanted FFV1 version 3, a number of slices, CRC for slices turned on,

[audio cuts out]

It was basically a set of parameters from Peter[Austria].

D: From Matroska?

I: We provided them a list of embedded metadata.

D: All official metadata tags? Not custom?

I: As far as possible, standard is always best. There's a reason that they're there.

It's quite resource heavy on playback. We don't tend to have much in the way of advanced spec PCs here.  But that's to be expected with HD material on playback.  MKV's been fine for holding all the stream and metadata content; FFV1 does a very good job retaining information.  I'm quite happy with it.

D: Any modifications to files after they get back from vendor?

I: At the moment, we're storing as received.  If there is a continuous recording session, we store that as 1 file. Shorter sections, individual files. Quite sizable files, no problems there.

J:  Is it problematic with FFV1 and Matroska not being formal standards?

I:  For us, it was a practical, pragmatic approach, and the fact that it was open--obviously if there's any need we can always move onto a further format.  Yes, I would like to see it a bit more promoted or seen as a standardized format.

FFV1: it does seem to be under-promoted; it's not on people's horizons at the moment.  People have heard something vaguely about it, or not heard of it all. It just needs its profile raised.  It does become a quite favorable option once people have had a look at it. It just needs a bit more of a push.

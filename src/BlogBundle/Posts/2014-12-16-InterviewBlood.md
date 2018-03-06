---
title: "Interview with George Blood"
date:   2014-12-16
tags: mediaconch, interview
---

# Interview with George Blood

Date: 12/16/2014

Interviewers: Dave, Erik

E: How is LPCM currently used at your facility?

G: We encounter LPCM in a variety of different ways. The most obvious example is when we perform the migration of analog audio recordings. Ninety-nine percent of the time, the analog materials we encounter are migrated to 96kHz/24-bit digital files with LPCM encoded data. In these files we also populate the BEXT chuck so that it exists should anyone wish to manage this metadata. Born-digital materials that we encounter are migrated in their native resolution, which is usually 48 or 44.1kHz/16-bit. We also encounter PCM from ADAT and DTRS at 20 and 24 bit. We see a tiny bit of format migration where we are taking other PCM formats and “normalizing” the data. For example, taking uncompressed files or things that are going to JPEG2000/MXF, etc.

E: Have you encountered any interoperability with LPCM?

G: In order to discuss interoperability issues with LPCM, we need to divide this conversation into LPCM as a codec itself, and what we take to be as issues with file wrappers. The biggest interoperability issue we’ve had in the past is text encoding for metadata; inconsistency between applications about whether the encoding was unicode or ASCII. As a solution, when we import textual metadata we now do a UTF-8 to ASCII crosswalk. We are now beyond issues of endianness, because it has just been “coded away”. That is, whether the bit stream is encoded as most significant bit or least significant bit first in the file. The playback applications now universally play either version.

If I had a wish list to deal with certain issues, however, it would be more interoperability in files larger than 2GB, a specification that was baked into the WAV file format since it’s inception. When you deliver files that are larger than 2GB, there’s some untested certain percentage of them that people will have problems playing, largely in part due to the newer RIFF64 spec has not yet widely adopted in all audio applications. The other thing you see are more wrapper-based issues, such as the packaging of individual mono or stereo pairs, an issue particularly in MXF. Another example being the behavior of stereo pairs in DV files. Audio applications do not uniformly interpret dual mono files as a L/R pair. Sometime you’ll get sequential playback, first channel 1, then channel 2. Or ONLY channel 1. When dealing with 4 channels, such as in MXF and DV.  The can be encoded as 4 mono files, or 2 stereo files. Sometime you’ll get the behavior just described, or the player will only deliver the first channel of the two pairs, and sometime you’ll get 4 individual channels (the correct answer).  Recently we’ve been fighting situations where we’re decoded 4 channels from analog tape, embedding all in the SDI stream, but the application will only wrap the first 2 channels.

E: How have your clients responded to these interoperability issues?

G: We deal with them in our shop. For us, if we can solve the issue of interoperability in our shop with the files that we are creating, then we can send the file deliverables out into the wild and they won’t come back with any issues. The amount of troubleshooting we used  to do with clients and how they were dealing with assets in their production/repository environments took a lot of time. By resolving as many interoperability issues ourself before we ship files saves us a whole lot of time and effort, if stuff has to be investigated and re-worked in any way.

For years we’ve been dealing with this interoperability issue, testing a lot of files we’ve created. For garden-variety WAV-wrapped PCM, for example, we will open the files in JHOVE. It’s not a particularly media-friendly validation environment, but it does handle these kinds of files. We find out the orders of the chunks, and whether the file is well-formed as JHOVE understands it. However, we encounter instances where we will go on and use BWFMetaEdit, either to probe the file or to fix things like padding-byte errors and such. JHOVE doesn’t give us error information. It’ll simply refuse to open a file or not display embedded metadata (for example of there’s a padding byte error).

E: Are their other programs that you find helpful in checking for conformance?

G: I would say that we don’t have tools to use for conformance, per se. Perhaps they exist, but we haven’t found any. There are some really nice tools in other areas that we use, particularly as we explore MXF. What we do now is open the files in a lot of different settings and do the testing empirically, as opposed to testing for conformance.

D: For PCM there’s no specific “structure”; raw PCM could be odd/even byte length, and it could start at any byte value, etc. One method of conformance checking is to look at common implementations of LPCM that do in fact have more implicit rules. For example, PCM in DV has restricted sample values that act as error codes. These things might be relevant to LPCM conformance. Beyond that we…

G: That’s really more of a wrapper issue rather than a PCM codec issue…

D: Exactly. We’re trying to figure out whether support of raw PCM itself is needed, or, whether we need to support conformity check on common wrappers of PCM, which can be a slippery slope. Or, should we focus on analyzing the contents of PCM for things list zero-padding in the lower bits, non-zero sampling, out-of-phase audio, etc. Taking the QCTools approach where we are analyzing the raw PCM coming out of the decoder.

G: Some of the things mentioned would be either useful or not a heavy payload. Knowing what the available headroom is, clipping or non-clipping is a light payload. Knowing whether there are padded bits, on the other hand, could be more difficult. When we were doingbit transference tests we found that bits were oftentimes dithered, as opposed to padded, which could be more difficult to detect. Knowing if files are padded with zeros would be useful information, however looking at wrapper-related issues for conformance is probably the place to draw the line, although I agree it is a slippery slope.

D: In the DV spec it adds additional rules about error concealment. Are there other standards like DV that use PCM in a modified way?

G: There are fringe cases like PrismSound 24 bit-packing and HDCD, as well as highly proprietary cases with good documentation like MLP and Dolby E. Ian Dennis at Prism sound has probes that look at bit streams and may be able to help with identifying these kinds of issues.

E: So, to confirm, would you prioritize identifying wrapper specifications over the stream itself?

G: Yes. PCM in and of itself is extremely simple. What happens after the data is created is where it gets interesting. For example, whether it’s funneled into a AES31 stream or a LightPipe or something like that, to the point where you get formatting issues.

D: In other words, there’s not a whole lot of demand for “What kind of PCM is this?”

G: Exactly. To take another example, back in the day we had issues with PCM F1 issues where the emphasis flag got lost in the migrationprocess. The emphasis flag feature starts with PCM10, but is only in the F1 and 1610 family as an option. If you migrate it as a AES-31 stream or through SPDIF, there is a flag for the emphasis. Likewise CD-DA and DAT have this flag, and support for it is required in the hardware. But the file wrappers do not have a place for this information so the feature drops out. You end up with encoded pre-emphasis without the technical metadata to know it needs to be decoded.

D: The CD format is where PCM has a lot of relevance. How do you do conformance checks of CD-R rips in particular?

G: Do you want a bit-for-bit copy or an error-corrected copy? Even if you want an ISO image, it will want to do the error correction in hardware coming off of the disc. For preservation we do DVDs to ISO images. However, it is uncommon to do ISO images for CD-R audio discs. As a result, things like CD text, pre-emphasis, and copy prohibit, buried the sub code will disappear.

D: With DVAnalyzer it will assess the bitstream coming off of the tape and throw flags indicating if there are errors in the read. This is used to determine how the read actually went. Are there similar approaches to PCM data ripped off of CD-Rs?

G: You would need access to the error correction polynomials. In our current rip station, our testers know at the block level what magnitude of error there has been, and whether it is detectable. But we don’t know any details about what’s going on otherwise. However, this feature is most-likely hardware-dependent and beyond the scope of your (implementation checker) project. Remember, CD playback is a system. Any test necessarily involves the data on the disc, the condition of the disc itself, and the machine that’s reading the data from the disc.

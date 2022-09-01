# Neural-Music-Demixing

## Welcome

The service receives a high-quality audio file and splits it into 4 sources: drums, bass, vocals and others. There is also the possibility of splitting into only one of these sources.

## What’s the point?

The service allows you to demix (split) the input audio file into various sources, including instruments. Separation is possible both for all 4 possible sources, and for one specific of the possible ones. So, for example, if you want to demix to all possible sources, then the output will be 4 audio tracks with drums, bass, vocals and everything else. If you want to demix only one of these sources, such as vocals, then you will end up with two audio files. In the first audio track there will be only vocals, in the second everything else except vocals.

## Model details:

## How does it work?

The user must submit an audio file for demixing. The audio file must be 44100 Hz stereo. Using machine learning methods, this audio file is separated into sources. At the output, the service will give a json string, where the key will be the name of the source, and the value will be bytes for their subsequent conversion into an audio signal.

### Example:

Json format string. 
If the client sent an audio file for splitting into 4 sources ("all"), the result will be the following:

> {"drums": "b'4//X////9'", "bass": "b'4//X////9'", "other": "b'4//X////9'", "vocals": "b'4//X////9'"}

If splitting into two sources was chosen, then an example output would be as follows:

> {"drums": "b'4//X////9'", "no_drums": "b'4//X////9'"}

Here, bytes are given for each source. Since the audio is two-channel, then transposition may be necessary. Be careful when converting bytes to an audio track. Check for correct sound. Requirements: 44100 Hz stereo.

## What to expect from this service?

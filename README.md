# Neural-Music-Demixing

## Welcome

The service receives a high-quality audio file and splits it into 4 sources: drums, bass, vocals and others. There is also the possibility of splitting into only one of these sources.

## What’s the point?

The service allows you to demix (split) the input audio file into various sources, including instruments. Separation is possible both for all 4 possible sources, and for one specific of the possible ones. So, for example, if you want to demix to all possible sources, then the output will be 4 audio tracks with drums, bass, vocals and everything else. If you want to demix only one of these sources, such as vocals, then you will end up with two audio files. In the first audio track there will be only vocals, in the second everything else except vocals.

## Model details:

The service is based on the Demux neural hybrid model. It is based on the U-Net convolutional architecture. The input waveform is processed both through a temporal encoder, and first through the STFT followed by a spectral encoder. The two representations are summed when their dimensions align. The decoder is built symmetrically. The output spectrogram go through the ISTFT and is summed with the waveform outputs, giving the final model output. Best of all, the model can demix bass and vocals. In the future, it is planned to improve the quality of demixing of different sources.

## How does it work?

The user must submit an audio file for demixing. The audio file must be 44100 Hz stereo. Using machine learning methods, this audio file is separated into sources. At the output, the service will give a json string, where the key will be the name of the source, and the value will be bytes for their subsequent conversion into an audio signal.

### Example:

Json format string. 
If the client sent an audio file for splitting into 4 sources ("all"), the result will be the following:

> {"drums": "b'4//X////9'", "bass": "b'4//X////9'", "other": "b'4//X////9'", "vocals": "b'4//X////9'"}

If splitting into two sources was chosen, then an example output would be as follows:

> {"drums": "b'4//X////9'", "no_drums": "b'4//X////9'"}

Here, bytes are given for each source. Since the audio is two-channel, then transposition may be necessary. Be careful when converting bytes to an audio track. Check for correct sound. Requirements: 44100 Hz stereo.

When tested locally, 3 demixes of 3 minutes of audio took about 30 seconds.

### Algorithm for converting bytes to audio signal (for the front):

1. Convert the string to a dictionary.
2. We cut off unnecessary characters for each sequence of bytes, which is still a string. In python it is 2 characters at the beginning ("b) and 1 character at the end (").
3. Encode into bytes again a string (now this string only with useful characters turns into bytes)
4. Create an array of int16 format from bytes, change the shape to a 2D array (for stereo). To do this, we make two arrays from one array, taking into account the fact that the values are in order. Transposing the array.
5. Save as an audio track with a frequency of 44100 Hz.

This algorithm is implemented in the client code after receiving a response from the server.

## What to expect from this service?

The client is expected to give the service 44100 Hz stereo sound, and the service will return the demixed audio files to the service, depending on the purpose of the demix. For all sources, the service should return 4 audio files with the following sources: drums, bass, vocals and others. For a source such as drums, the service should return 2 sounds: drums and everything else except drums.

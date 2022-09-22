# Neural-Music-Demixing

## Welcome

The service receives a high-quality audio file and splits it into 4 sources: drums, bass, vocals and others. There is also the possibility of splitting into only one of these sources.

## What’s the point?

The service allows you to demix (split) the input audio file into various sources, including instruments. Separation is possible both for all 4 possible sources, and for one specific of the possible ones. So, for example, if you want to demix to all possible sources, then the output will be 4 audio tracks with drums, bass, vocals and everything else. If you want to demix only one of these sources, such as vocals, then you will end up with two audio files. In the first audio track there will be only vocals, in the second everything else except vocals.

## Model details:

The service is based on the Demux neural hybrid model. It is based on the U-Net convolutional architecture. The input waveform is processed both through a temporal encoder, and first through the STFT followed by a spectral encoder. The two representations are summed when their dimensions align. The decoder is built symmetrically. The output spectrogram go through the ISTFT and is summed with the waveform outputs, giving the final model output. Best of all, the model can demix bass and vocals. In the future, it is planned to improve the quality of demixing of different sources.

## How does it work?

The user must submit an audio file for demixing. The user can only submit audio in wav format! In this case, the frequency and number of channels do not matter. Using machine learning methods, this audio file is separated into sources. At the output, the service will give a json string, where the key will be the name of the source, and the value will be bytes for their subsequent conversion into an audio signal.

### Example:

Json format string. 
If the client sent an audio file for splitting into 4 sources ("all"), the result will be the following:

> "{"drums": b'4//X////9', "bass": b'4//X////9', "other": b'4//X////9', "vocals": b'4//X////9'}"

If splitting into two sources was chosen, then an example output would be as follows:

> "{"drums": b'4//X////9', "no_drums": b'4//X////9'}"

For each type of sound, the bytes of the wav audio file with all the embedded information are given. There is also a converter on the server side. You need to submit any wav audio.

When tested locally, 3 demixes of 3 minutes of audio took about 30 seconds.


## What to expect from this service?

The client is expected to give the service 44100 Hz stereo sound, and the service will return the demixed audio files to the service, depending on the purpose of the demix. (Changed: you need to submit any wav file) For all sources, the service should return 4 audio files with the following sources: drums, bass, vocals and others. For a source such as drums, the service should return 2 sounds: drums and everything else except drums.

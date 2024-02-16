# Neural-Music-Demixing

## Welcome

The service receives a high-quality audio file and splits it into 6 sources: drums, bass, vocals, guitar, piano and others. There is also the possibility of splitting into only one of these sources and into a combination. You can choose what you need to get. Don't forget to leave feedback on the results! Your feedback is important to us!

## What’s the point?

The service allows you to demix (split) the input audio file into various sources, including instruments. Separation is possible either by all 6 possible sources, by combination, or by one specific one of the possible ones. So, for example, if you want to demix all possible sources, the output will be 6 audio tracks with drums, bass, vocals, guitar, piano and everything else. If you only want to demix one of these sources, such as vocals, you will end up with two audio files. The first audio track will contain only vocals, the second will contain everything else except vocals.

## Model details:

The service is based on the Hybrid Transformer Demucs. We use a combination of the two models to achieve the best separation. Our results clearly exceed the separation level of the standard model. Moreover, the model was trained on data from 6 sources, which added 2 new possibilities for separation: piano and guitar. The division of the piano especially stands out. We tried to improve this part compared to our competitors.

## How does it work?

The user must submit an audio file for demixing. The user can only submit audio in mp3 format! In this case, the frequency and number of channels do not matter. Using machine learning methods, this audio file is separated into sources. At the output, the user will receive the selected categories + other, where the unselected sources are stored (or <no_source> when selecting one source).

### Example:

If the user chose a combination of drums, guitar and vocals, then they will get the separated drums, guitar, vocals and the rest of the mixture in the output. The longer the audio, the longer it takes to process. The average waiting time for a standard song lasting 3-5 minutes is 40 seconds.


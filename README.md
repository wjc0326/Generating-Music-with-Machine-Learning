# Generating-Music-with-Machine-Learning
## Abstract
Final project for CIS 519 with Ruxuan Ji and Joan Shaho. We attempted to create a __ML-based music generator__ that can act as an assistant for young and inexperienced composers. We built a __Logistic Regression (LogReg)__ as our baseline model, and an __LSTM__ which is a good fit due to its ability to retain sequential information. The music generated by the LogReg model was not that good, with many silent and dissonant parts, while the LSTM model seemed to produce much better music. __In conclusion, LogReg is not robust enough for tasks such as music generation, but LSTM on the contrary seems to excel.__
## Installation
1. Go to https://magenta.tensorflow.org/datasets/maestro#download to download maestro-v3.0.0-midi.zip
2. Unzip the folder
3. Upload the unzipped folder to your Google Drive
4. You are ready to run these two colab docs
## Formal Problem Setup (T, E, P)
* __T__: 
  * __LogReg__: We used __128 binary L2-Regularized LogReg binary predictors__ (one for each possible note/pitch) and each model was trained independently. The goal of each of them was to predict whether the corresponding note should be part of the next time step based on the given sequence of previous time steps, with the positive class corresponding to playing that note. After training, we passed the same seed to all the predictors, and the positive predictions formed the note combination for the next timestep. The process was repeated and the music was generated.
  * __LSTM__: The data used for training was similar to the LogReg one with the only difference being the target data. Specifically, while for LogReg there was a __separate binary target label__ for each predictor, the LSTM had a __single categorical label__ which corresponded to the note combination in the next timestep.
* __E__: 
  * We used 93 songs from the __MAESTRO dataset__ which has classical piano pieces stored as __MIDI files__. Each file contained a __2D array__ where the __rows__ are __the possible notes (128)__ and the __columns__ are __the number of timesteps__. We recorded the notes played at each timestep and created a __dictionary__, with __keys__ corresponding to the __different note combinations in the training data__ and __values__ being __unique integers__. Lastly, the data was split to __50-timestep windows__ which formed the “context” for each prediction.
* __P__: 
  * We defined and applied the __cross-entropy loss__ between the __predicted__ and __target__ labels as our standard metric for performance for both the __LogReg__ and __LSTM__ models.

## Supplementary material
__Links to LogReg-generated songs:__

1-song trained logistic regression: [https://soundcloud.com/joan-shaho/1-song-trained-model-1](https://soundcloud.com/joan-shaho/1-song-trained-model-1)

50%-trained logistic regression: [https://soundcloud.com/joan-shaho/new133s-last50](https://soundcloud.com/joan-shaho/new133s-last50)

__Links to LSTM-generated songs:__

1-song trained LSTM: [https://soundcloud.com/joan-shaho/lstm-15-001](https://soundcloud.com/joan-shaho/lstm-15-001)

50%-trained LSTM: [https://soundcloud.com/joan-shaho/result-15-05](https://soundcloud.com/joan-shaho/result-15-05)

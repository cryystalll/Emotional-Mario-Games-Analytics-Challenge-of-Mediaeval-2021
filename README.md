# Emotional Mario: A Games Analytics Challenge of Mediaeval 2021
## I. INTRODUCTION : [Challenge Link of Mediaeval 2021](https://multimediaeval.github.io/editions/2021/tasks/emotionalmario/#:~:text=The%20task%20is%20called%20Emotional,video%20game%20Super%20Mario%20Bros.&text=This%20can%20include%20gameplay%20scenes,what%20happened%20during%20the%20game.)
<div align=center><img src="/img/game.png" alt="Cover" width="30%"/></div>

```
* A grand challange from MediaEval
* Motivation: game affects users’ emotions → the connection between emotion and games
* In this task, participants carry out multimedia analysis in order to gain insight into the emotion of players playing video games. 
* The task is called Emotional Mario because it focuses on the iconic video game Super Mario Bros.
```
## Task: Event detection
```
Participants carry out emotional anlaysis on facial videos and biometric data 
(e.g., heart rate and skin conductivity) collected from players playing the game. 
The goal is to identify key events (i.e., events of high significance in the gameplay). 
Such key events include the end of a level, a power-up or extra life for Mario, or Mario’s death.
```
<div align=center><img src="/img/a1.png" alt="Cover" width="40%"/></div>

## Dataset: [Toadstool](https://osf.io/qrkcf/)
* Download the dataset:
```
sudo apt install p7zip-full
7z x toadstool.zip.001
```
```
* The dataset consists of video, biometric data collected from 10 participants playing Super Mario Bros
* Participants wore wristband to collect the biometric data
```
* The dataset is separated into two main folders:
```
* participants: facial videos, biometric data, and game data from the ten participants
* scripts: Scripts about how they synchronize the game data with other data. A script to get mario game frame.
```
## Facial video in Participants
<div align=center><img src="/img/a2.png" alt="Cover" width="40%"/></div>

## Biometric Data in Participants
```
* ACC: the movement of the wearer
* EDA: the electrical conductivity of the skin
* BVP: blood Volume Pulse
* IBI: the time interval between individual heartbeats → the instantaneous heart rate/heart rate variability
* HR: the average heart rate values
* TEMP: the temperature of the person
```
## Game Data in Participants
```
* Use replay_game_session.py in scripts folder with participant_[num]_session.json in participants folder to get the game frames.
```
<div align=center><img src="/img/a3.png" alt="Cover" width="40%"/></div>

## Groundtruth
```
{"event": "status_up", "frame_number": 428}, 
{"event": "flag_reached", "frame_number": 1915}, 
{"event": "new_stage", "frame_number": 1916},...
```
## II. DATA CHOOSING
* A. Emotional data
```
* The given data which may considered have relation to participant’s emotions are facial videos, bio-features. I finally choose only the facial videos as input. The reason why I don’t use other data is that they may differs due to each participant’s body conditions. The standardize among all the other datas may be complicated, requires more background knowledges about biology.
```
* B. Game frame data
```
* Since the emotional data can only tell us if a game event happens, it can’t tell us which specific game event just happened, so I included the game frame data as input.
```
## III. TRYING: USING EMOTIONAL DATA AND GAME FRAMES
* A. Identify the participant’semotions
```
* I use a pre-trained model — FER to identify the emotion in the video.
* But since the process of splitting the video into frames and doing FER to all frames is time consuming(takes more than 10 hours to do FER to 60000 frames), so we decided to reduce the sampling rate to 3Hz, since +-25 frames is acceptable.
```
* B. Detect if a game event happened based on emotion datas to select the target frames
```
* Use CNN to train a model to select the target frames based on emotion data.
```
* C. Classify the game events
```
* Use CNN to train a model to classify the game events of selected target frame based on their emotion data & game frames.
Note that the dimension of a picture and the emotion data is different,
so I upgrade the dimension of emotion data to fit the dimension of picture.
```
## IV. GAN GAME FRAME TO OPTIMIZE THE ACCURACY
```
* Use GAN to generate some pictures to feed in the model for training
```
<div align=center><img src="/img/gan.png" alt="Cover" width="30%"/></div>

## IV. Results and Accuracy
```
However, I found that this method’s F1 score is low.
So I use game frames as input 
(since ground truth’s game event is not much)
I use GAN to generate more pictures to feed in the model for training by CNN model, 
and get higher F1 scores.
F1 score goes to 0.82.
```
```
I think that it’s because the player’s emotion is not directly related to the game event. 
By observing the emotion data, I found out some factors making the emotion data not accurate:
* 1. Everyone has different emotional response when facing same event. After watching the videos, we found out that some people laughed when Mario dies, while others may look frustrated in the same scenario.
* 2. Some people’s appearance may seems sad/angry/ happy, thus affected the result of FER. For example, in participant_3’s FER result, the value of sad is always very high.
* 3. Some people just don’t have significant emotional response.
```
```
* These factors are not stable, and I only has 10 participant as ground truth, so the model we trained are not accurate at all.
* After that, I change another method to achieve the task goal.
```







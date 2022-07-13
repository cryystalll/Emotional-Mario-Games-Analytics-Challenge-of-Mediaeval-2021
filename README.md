# Emotional Mario: A Games Analytics Challenge of Mediaeval 2021
* ![Variable Declaration](/img/game.png)
[Challenge Link](https://multimediaeval.github.io/editions/2021/tasks/emotionalmario/#:~:text=The%20task%20is%20called%20Emotional,video%20game%20Super%20Mario%20Bros.&text=This%20can%20include%20gameplay%20scenes,what%20happened%20during%20the%20game.)
* A grand challange from MediaEval
* Motivation: game affects users’ emotions → the connection between emotion and games
* In this task, participants carry out multimedia analysis in order to gain insight into the emotion of players playing video games. The task is called Emotional Mario because it focuses on the iconic video game Super Mario Bros.
* ![Variable Declaration](/img/a5.png)
## Task 1: Event detection
* ![Variable Declaration](/img/a1.png)
## Dataset: [Toadstool](https://osf.io/qrkcf/)
Download the dataset:
```
sudo apt install p7zip-full
7z x toadstool.zip.001
```
* The dataset consists of video, biometric data collected from 10 participants playing Super Mario Bros
* Participants wore wristband to collect the biometric data
* The dataset is separated into two main folders:
* participants: facial videos, biometric data, and game data from the ten participants
* scripts: Scripts about how they synchronize the game data with other data. A script to get mario game frame.
## Facial video in Participants
* ![Variable Declaration](/img/a2.png)
## Biometric Data in Participants
* ACC: the movement of the wearer
* EDA: the electrical conductivity of the skin
* BVP: blood Volume Pulse
* IBI: the time interval between individual heartbeats → the instantaneous heart rate/heart rate variability
* HR: the average heart rate values
* TEMP: the temperature of the person
## Game Data in Participants
* Use replay_game_session.py in scripts folder with participant_[num]_session.json in participants folder to get the game 
* ![Variable Declaration](/img/a3.png)
## Groundtruth
* ![Variable Declaration](/img/a4.png)
## Report






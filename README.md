<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/icon_ict2.png">

# Hi all, welcome to Thailand-Japan Student ICT Workshop 2022 repository :robot: :smile_cat: :desktop_computer:
### *A hands-on tutorial on hand gesture recognition for hardware control* 

###  22 December 2022
#### *by Robotic Engineering and Artificial Intelligence (REAI), Faculty of Engineering, Chiang Mai University*
---

> *This workshop is designed for those who are interested in integrating the microcontroller system with a machine learnign framework. Here, [MediaPipe](https://google.github.io/mediapipe/) is selected regarding its low computational resource requirement and simple implementation. To control microcontroller, [pyFirmata](https://pypi.org/project/pyFirmata/#:~:text=pyFirmata%20is%20a%20Python%20interface,Python%202.7%2C%203.3%20and%203.4.) is picked out to perform the serial communication between Arduino and Python. For the attendees' fullest advantages, this workshop requires:*
> 1. *A computer with a camera connected* ***(Attendees are responsible to bring this item)***
>2. *Arduino UNO R3 (Qty. 1)* ***(provided)***
>3. *USB square port data cable type B (Qty. 1)* ***(provided)***
>4. *Servo motor (Qty. 1)* ***(provided)***
>5. *Breadboard (Qty. 1)* ***(provided)***
>6. *Resistor (Qty. 5)* ***(provided)***
>7. *LED (Qty. 5)* ***(provided)***
>8. *Jumper wires* ***(provided)***
>
> *Attendees are also expected to complete installing the following softwares and libraries (regarding to the previously provided [guideline](https://colab.research.google.com/drive/1rvIae6hsvQDKnhotqOErPsn2PHxYOPm8?usp=sharing)).*
>
> <u><i>software</i></u>
>1. [*Arduino IDE*](https://www.arduino.cc/en/software)
>2. [*Visual Studio Code*](https://code.visualstudio.com/)
>
> <u><i>Python library</i></u>
>1. [*MediaPipe*](https://pypi.org/project/mediapipe/)
>2. [*OpenCV*](https://pypi.org/project/opencv-python/)
>3. [*pyFirmata*](https://pypi.org/project/pyFirmata/#:~:text=pyFirmata%20is%20a%20Python%20interface,Python%202.7%2C%203.3%20and%203.4.)

## ***Tool introduction***

#### <u>Arduino IDE</u>
Arduino IDE is the open-source Arduino Software which is designed for Arduino board users to make them capable to communicate with the hardware via coding, where IDE hereby stands for an integrated development environment which describing software for building applications that combines common developer tools into a single graphical user interface (GUI)[[1]](https://www.redhat.com/en/topics/middleware/what-is-ide#:~:text=An%20integrated%20development%20environment%20(IDE,graphical%20user%20interface%20(GUI).). In most of the works, to simplify the program and workflow, we use a prior developed programming resource called <i><u>library</u></i> which is defined in computer science as a programming part including processes and subroutines (with or without source code) which are necessary in one specific program or software workflow. 

#### <u>Necessary python libraries</u>
<u><i>[pyFirmata](https://pypi.org/project/pyFirmata/#:~:text=pyFirmata%20is%20a%20Python%20interface,Python%202.7%2C%203.3%20and%203.4.) </u></i>

This is a library allows python users to communicate with microcontrollers via the [*Firmata*](http://firmata.org/wiki/Main_Page) protocol which is one of the communication protocol between microcontrollers and a host computer.

[*OpenCV*](https://pypi.org/project/opencv-python/)

Open Source Computer Vision Library (OpenCV) is a library designed for using in computer-vision to develope high-level applications such as face detection, feature matching and object tracking [[2]](https://dl.acm.org/doi/10.1145/2181796.2206309).

[*MediaPipe*](https://pypi.org/project/mediapipe/)

It is a library developed by Google used in detecting face, body gestures and object from a streaming media by utilizing machine learning model. In this workshop, we are also using [*MediaPipe Hands*](https://google.github.io/mediapipe/solutions/hands) which is a hand and fingers tracking solution provided by the library. With this solution, it is perhaps helpful to hereby introduce the *Hand landmark* model for better understanding. 

> ***Hand landmark model*** is the model identifying the key point location of 21 3D hand-knuckle coordinates. Each coordinate has a specific keypoint value, as shown in the following figure, to allow us to design the hand gesture recognition program. 
>
><img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/hand_landmarks.png" width=500/> 
>
> *figure 1: 21 loacations in hand landmark model [[3]](https://google.github.io/mediapipe/solutions/hands)* 
>
> <img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/hand_crops.png" width=500/> 
>
> *figure 2: Hand gestures examples [[3]](https://google.github.io/mediapipe/solutions/hands)*

## ***Section 0: Getting started***

In this section, we will introduce you to VS code basic operation and virtual environment creation.

<u><i> VS code workspace creation </u></i>

- Download .zip file from the workshop [repository](https://github.com/JJGGtan/ICT_workshop2022.git) by clicking `Download ZIP` as shown in the following figure. 
<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/git_download_zip.png" width="800px"> 

- Unzip the file and then launch VS Code software.
<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/VScode_launch.png" width="600px">

- Within unzipped folder named `"ICT_workshop2022-main"` by default, go to directory `ICT_workshop2022-main\ICT_workshop2022-main\materials\codes\ICT Project code and controller`. Select the folder named `"ICT Project code and controller"`.

- Now, in the VS code left vertical panel, there is a previously called folder appear. On the top bar, select `Terminal` and then select `New Terminal` as shown in the following figure. 
<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/New_terminal.png" width="600px">

- Here, the terminal will appear on the bottom section of the VS code window as shown in this figure. 
<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/terminal_appear.png" width="600px">

- At this point, you can now write a command to create a virtual environment containing file as noted in the pre-workshop manual or as follows.
- 
```
python -m venv .venv source .venv/bin/activate
```

Then install the required libraries.
<li> <i><a href="https://numpy.org/">NumPy</a> : essential for performing mathematical operations </i> To do so, on the terminal, type
<code>python -m pip install numpy</code>
<li> <i><a href="https://matplotlib.org/">Matplotlib </a> : for data graphical visualization.</i> Type <code>python -m pip install matplotlib</code>
<li> <i><a href="https://pypi.org/project/opencv-python/"> OpenCV </a> : for real-time computer vision implementation </i> Type <code>python -m pip install opencv-python</code>
<li> <i><a href="https://pypi.org/project/mediapipe/"> MediaPipe </a> : for machine learning framework implementation </i> Type <code>python -m pip install mediapipe</code>
<li> <i><a href="https://pypi.org/project/pyFirmata/#:~:text=pyFirmata%20is%20a%20Python%20interface,Python%202.7%2C%203.3%20and%203.4."> pyFirmata </a> : for Python-Arduino serial communication </i> Type <code>python -m pip install pyFirmata</code>
</ol>

---

% !TeX spellcheck = en_US
% !TeX encoding = UTF-8
% !TeX root = ../thesis.tex

\chapter{Methodology}
\label{chap:methodology}  
\section{Outline}
% Process outline
This thesis aims to optimize the magnets and senors count, position and orientation in the joint. With all of the variables and constraints, creating a comprehensive mathematical model depending on the mentioned variables is extremely challenging and time-consuming. That is why a more brute-force approach is chosen—simulating many different possible setups and evaluating them. This is achieved through a pipeline, involving 4 steps - Artificial data generation, Model training, Model evaluation and Real-world validation
% Choice of simulation environment
\section{Simulation}
Firstly, a simulation environment is created. The tool of choice is a python simulation script with the magnetic field simulation library "magpylib". Its optimizations for magnetic field computing, the great visualization tools, and the easy implementation are the reason for this choice. The RCJ kinematics were simulated using 2 cylinders, representing both parts of the joint. The simulation allowed for movement in all 6 Degrees of freedom, including the 3 translations. For each magnet sensor setup, the sensor readings for each joint configuration had to be calculated, which meant 150 degrees of rotation (pitch) * 40 degrees of twisting motion (roll) * 20 degrees (yaw) of bending motion.  A resolution of 2 degrees was chosen because it is computationally inexpensive compared to higher resolutions, while still being able to capture the relationship between sensor readings and joint configuration. Translations between 0 and 3 mm (with 1 mm step) along the 3 axes were also included.  The orientations that the magnets could take were constrained to 90-degree rotations around each axis, with a 45-degree step. The position of the magnet(s) was determined by two variables - center offset (between 2 and 6 mm offset with 2 mm steps): the distance from the center of the rotating part to the center of the magnet, and center angle offset (0 or 45): the angle between the center line and the magnet(s). A Python script was set to iterate through all possible joint configurations within the constraints. In the time frame of the thesis, only experiments with one sensor were possible, which is why the simulations are more focused on the setups with 1 sensor.
% Choice of algorithm for capturing the relationship
\chapter{Model training}
The data was split in training and testing data, with respectively 80% and 20% part of the whole data. A simple neural network with 4 layers was chosen for the evaluation of each setup. The input node had 3 input nodes per sensor (one node per axis), 64 and 32 nodes in the hidden layers and 3 output nodes with "Adam" optimizer, representing the 3 possible rotations in degrees. For each neural network 100 epochs with batch size of 32 and learning rate of 0.0005 were durchgefuhrt. The small learning rate allows for better prediction accuracy, but could however cause overfitting. To combat this effect early stopping with the patience of 10 was implemented. The risk of overfitting is also mitigated by the fact that only values in a certain range can and will be predicted.
\chapter{Evaluation}
% Choice of the evaluation parameters
The evaluation parameter was chosen to be root mean squared error, because it is easily interpretable and directly shows the correlation between the sensor-magnet setup and prediction error. Mean absolute error would skew the results in favor of the smaller error, because the overshot predictions would cancel the undershot ones.
\chapter{Validation}
The best performing setup was transferred onto the real joint. The fixed part houses the sensor setup, while the moving part houses the magnet setup. The magnets used were cylindrical magnets with .. {specifications} 
Due to the complexity, required for measurement gathering setup in 6 DoF, the motion of the experimental setup was constrained to the sagittal plane (main rotation plane) with the ground truth being a 3D printed angle board. 

%% PLOTS USED DESCRIPTION
HARDWARE DESCRIPTION


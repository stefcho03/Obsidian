% !TeX spellcheck = en_US
% !TeX encoding = UTF-8
% !TeX root = ../thesis.tex

\chapter{Related work}
\label{chap:related work}
\remark{You can add a short paragraph here that briefly says what the related work contains.}

Contactless angle measurement method are diverse in their size, application, requirements and limitations. In this chapter a variety of angle estimation methods are looked into and evaluated for the use case of the RCJ. Then the most fitting one is chosen and its applications in the joint angle measurements are looked into. 

\section{Possible methods of contactless angle measurement}
There are 8 possibilities for contactless angle measurement. The following table presents them next to the challenges they pose.

\begin{table}[ht!]
\caption{Contactless angle measurement methods}
\vspace*{0.5cm}
\centering
\begin{tabular}{p{0,3\linewidth} p{0,3\linewidth} p{0,3\linewidth}}
\toprule
Method & Positive & Incompatibility \\
\midrule 
Magneto-resistive sensor & Robust to mechanical misalignment & Influenced by external magnetic fields\\
Capacitive sensors & Accuracy & Range \\
Inductive sensors & Robustness & Size \\
Ultrasonic & Independence from magnetic fields and light & Sensitivity to vibrations, Limited resolution \\
Laser interferometer & Accuracy & Precision requirements \\
Inertia measurement unit (IMU) & Compactness, Accuracy & Drift \\
Hall-effect sensor & Absolute value & Nonlinear relationship
\bottomrule
\end{tabular}
\label{tab:macros}
\end{table}


\citep{wang_review_2024}. Magneto-resistive sensors are robust to mechanical misalignment but are influenced by external magnetic fields. Capacitive sensors are highly sensitive but have limited range. \citep{kumar_technologies_2021} Inductive sensors are very robust, but their size prevents them from being viable. Ultrasonic sensors are independent of magnetic or light properties, but they have limited resolution and are not suitable for vibrations \citep{singh_effect_2017}. Laser interferometers are extremely accurate, but require a very precise configuration \citep{loughridge_tutorial_2013}. 

Only Inertia measurement units (IMUs) and Hall-effect sensors fit the required parameters - they both fit in the joint and allow 3DoF measurements. IMUs however have a significant drawback when used for long periods of time. The accumulating estimation error is rising exponentialy with time, causing large amount of drift. Another advantage of the Hall-effect sensors over IMUs is the need for calibration. IMUs approximate the position based on relative movement and therefore need to be calibrated before each use, which is not the case for Hall-effect sensors, which measure the absolute position and require only one calibration. 
This leaves Hall-effect sensors, specifically 3D Hall-effect sensors, as the best option for measuring rolling contact joints. The problem that proves very difficult is extracting enough information from the sensor readings to be able to determine the joint configuration. This is mainly caused by not having enough variance in the resulting magnetic field, mainly due to the magnet configurations \citep{jin_nonlinear_2007}.

\section{Uses of Hall-effect sensors for other angle measurements}
% Angle measurement with Hall-effect sensors
Using a Hall-effect sensor to measure an angle contactlessly is not a new concept. In \cite{lee_applications_2011} a radially polarized magnet is being rotated close to a 2D hall-effect sensor, with the help of which the degree of rotation is being determined. This setup is being widely used in the automotive industry to determine the position of the crankshaft or the wheel speed without having to worry about wear of the sensor. The achieved accuracy is +- 0.6 degrees. 

\section{Angle measurement of high DoF joints}
% Joint angle measurements
This widespread and researched solution cannot be applied to the intricate nature of the human joint. Every human has unique joints that behave differently than those of other people, which, combined with the high DoF nature of the human joint forces the implementation of contactless angle measurement methods. Many different complex methods are being used to approximate the position of the human joint, such as MRI in \cite{graichen_glenohumeral_2000} for shoulder joint configuration estimation, a combination of acceleration, angular rate, and magnetic sensors in \cite{odonovan_inertial_2007} for ankle joint configuration estimation or 4 inertia measurement units in \cite{alvarez_upper_2016} for the elbow joint configuration estimation. All of these methods require heavy computation and are not taken into consideration for this use case.

% Exoskeleton joint angle measurements
Thankfully, in the human-designed joints, every parameter is known, and its behavior stays the same no matter the user. This allows for simpler measurement methods in low DoF joints like the potentiometer used in \cite{tsai_design_2019} and the two potentiometers used in \cite{tanaka_development_2013}.
% Contactless exoskeleton joint angle measurements
In higher DoF joints, however, the angle measurement becomes much more complex. In the following different ways of using Hall-effect sensors for joint angle measurement are looked into. 
% Contactless joint angle measurements with Hall-effect sensors
%1DoF Finger
The simplest case of measuring a joint angle using a Hall-effect sensor is found in \cite{}. The setup used in this paper consist of 1 radialy polarized permanent magnet and one 3D Hall-effect sensor, which is very similar to the well-researched method used in the automotive industry. This method is limited to only 1 DoF and could not be used for RCJ. 

The use of Hall-effect sensor for measuring knee flexion is implemented in \cite{rivera_3d-printed_2022}, where the sensor measures the angle of radially polarized magnet is being used to measure the flexion angle in the rotation plane. This method meausures is used to estimate the users' activity and therefore does not require high accuracy. 

% Dog implants
Two separate papers have implemented a method for measuring the flexion angle of dog joints using implanted magnets and sensors. The first one uses a setup with two magnets and one 1D sensor, while the second one uses an array of 3 sensors and 1 magnet. Both of the proposed methods work only in 1DoF and have 2.5 and 5 degrees of error respectively. While the joint type is the same, the lack of Degrees of Freedom prevents them from being used for the goal of the thesis. 
% Spherical joint 6DoF (Overkill)
The last relevant for this thesis paper is of a measurement method, which allows for the 3D position estimation of a ball-in-socket joint. This method uses a combination of 3 differently oriented magnets and 4 sensors. The use of highly variant magnetic field in combination with advanced machine learning methods allowed for the highly precise (RMSE 0.1) measurement in 3DoF. This however does not account for the moving center of rotation and asymmetric geometry present in the RCJ. This creates the need of a new measuring method for the RCJ.


% !TeX spellcheck = en_US
% !TeX encoding = UTF-8
% !TeX root = ../thesis.tex
\chapter{Fundamentals}
\label{chap:fundamentals}
% Terminology
Firstly, a few definitions have to be made.


% Rolling contact joint kinematics
\section{Rolling contact joint kinematics}
The defining kinematic feature of a Rolling Contact Joint (RCJ) is its combination of rotation and translation. Unlike a simple revolute joint with a fixed center of rotation, an RCJ's center of rotation translates as one curved surface rolls on another. This complex motion poses a significant challenge for position estimation. While the joint has multiple Degrees of Freedom (DoF), this analysis will focus on the primary plane of motion corresponding to knee flexion and extension, as the other motions' kinematics are simpler and can be modeled with simple rotation around an axis.
The rotation and translation depend on the ratio of the 2 radii, which for the frame of this thesis are fixed and already determined. On the surface, the movement may resemble a simple rotation around a fixed point, but the rotation around its axis must also be considered.  It is also different than simple rotation around a fixed point, because of the constant translation of the rotation center and asymmetric geometry. The rotation degrees around its axis are not the same as the rotation degrees around the static part, which creates the need to calculate how much the rotating part rotates around its axis.
% Rolling contact kinematics figure DELFT paper
\begin{figure}[ht!]
    \label{fig:prototype}\includegraphics[width=1\textwidth]{figures/Rolling contact joint/RCJ_kinematics}   
    \caption{Generalized kinematics of a two-link rolling contact joint, illustrating the relationship between radii ($R_1$ and $R_2$) and angular displacements ($\alpha$ and $\beta$)}
    \label{fig:Kinematics}
\end{figure}
The fundamental principle governing the joint's movement is the no-slip condition. To maintain pure rolling contact, the arc length traversed on the static component must equal the arc length traversed on the moving component. As illustrated in \cref{fig:Kinematics}, this kinematic constraint links the angular displacement of the static part ($\alpha$) and the moving part ($\beta$) relative to their respective radii, ($R_1$ and $R_2$): 
\[ \Dot{\alpha}\cdot R_1 = \Dot{\beta}\cdot R_2 \]

From this, the total flexion angle of the joint, $\alpha$, can be defined as the sum of the individual angular displacements:
\[\alpha = \alpha_1 + \alpha_2 = \alpha_1 + \frac{r_1 \cdot \alpha_1}{r_2}\]
% RCJ Kinematics Asfour paper
\begin{figure}[ht!]
\label{fig:both}
    \centering
    \subfigure[RCJ prototype investigated in this thesis.]{\label{fig:prototype}\includegraphics[width=0.4\textwidth]{figures/Rolling contact joint/RCJ_prototype}}    
    \hspace{1cm}            
    \subfigure[2D representation of the RCJ]{\label{fig:circles}\includegraphics[width=0.5\textwidth]{figures/Rolling contact joint/RCJ_circles}}                
    \caption{Rolling contact joint}
    \label{fig:RCJ}
\end{figure}

\cref{fig:both} shows the physical RCJ prototype in \cref{fig:prototype} and its 2D representation \cref{fig:circles}. Based on the design by Beil et al. \cite{beil_rolling_2019}, its rolling surfaces are designed with a static radius ($r_1$) of 11.4 mm and a moving radius ($r_2$) of 13.1 mm to optimize the joint's torque characteristics. The primary range of motion for the flexion angle ($\alpha$) is 0° to 138°. The joint also allows for secondary motions, including a 20° bend and a 34° twist, which also need to be measured.

\section{Quaternions}
For simulating rotations within this thesis, quaternions are employed. They are selected over other rotation representations, such as Euler angles and rotation matrices, due to their inherent numerical stability, computational efficiency, and avoidance of gimbal lock. \\
A quaternion $q$ is an extension of complex numbers and is expressed in the form:
\[ a + b\boldsymbol{i} + c\boldsymbol{j} + d\boldsymbol{k}\]
where $a, b, c$ and $d$ are real numbers, while $\boldsymbol{i}, \boldsymbol{j}$ and $\boldsymbol{k}$ are the fundamental quaternion units that follow the multiplication rules shown in \cref{tab:quaternions}. 
\begin{table}[]
\caption{Quaternion multiplication table}
\vspace*{0.5cm}
\centering
\begin{tabular}{|l|l|l|l|l|}
\hline
\rowcolor{gray!20} 
x          & 1          & \textbf{i}  & \textbf{j}  & \textbf{k}  \\
\hline
\cellcolor{gray!20}
1          & 1          & \textbf{i}  & \textbf{j}  & \textbf{k}  \\
\hline
\cellcolor{gray!20}
\textbf{i} & \textbf{i} & -1          & \textbf{k}  & \textbf{-j} \\
\hline
\cellcolor{gray!20}
\textbf{j} & \textbf{j} & \textbf{-k} & -1          & \textbf{i}  \\
\hline
\cellcolor{gray!20}
\textbf{k} & \textbf{k} & \textbf{j}  & \textbf{-i} & -1 \\
\hline
\end{tabular}
\label{tab:quaternions}
\end{table}

The left column shows the first factor and the first row shows the second factor. This will be of use in combining rotations, which happens with simple multiplication of the 2 quaternions.
In the context of rotations a spatial rotation around a fixed point  of $\theta$ radians about unit (with length equal to 1) axis ${x,y,z}$ can be represented by the quaternion \[[\cos{\frac{\theta}{2}}, x\cdot\sin{\frac{\theta}{2}}, y\cdot\sin{\frac{\theta}{2}}, z\cdot\sin{\frac{\theta}{2}}]\]. The use of this representation allows for efficient simulation of discrete positions. Simulating continuous movement, however, requires computationally heavy interpolation methods like the Spherical Linear Interpolation (SLERP) to ensure a path of constant angular velocity.
\section{Magnetic field computation}
A permanent magnet generates a magnetic field, represented as a vector field. According to the Biot-Savart law, the strength and direction of this field can be calculated by summing the individual vector fields induced by each magnet. The Biot-Savart law is expressed as: 
\[\mathbf{B}(\mathbf{r}) = \frac{\mu_0}{4\pi}
\int_{V}\frac{\mathbf{J}(\mathbf{r'})\times(\mathbf{r}-\mathbf{r'})}
{|\mathbf{r}-\mathbf{r'}|^3}dV'\]
with: \\
$\mathbf{r}$ being the observation point (where the measurement takes place) \\
$\mathbf{r'}$ being the source point inside the magnet \\
$\mathbf{J}$ being the current density (derived from $\nabla$ $\times$ $\mathbf{M}$ with $\mathbf{M}$ being the magnetization vector of the magnet) \\
V being the volume of the magnet \\
$\mu_0$ being the permeability of free space \\

The magpylib library approximates this integral using numerical methods with an error below $10^{-6}$ Tesla \cite{ortner_magpylib_2020}. In the RCJ context, $\mathbf{r'}$ relates to the kinematic equations, while the magnetization vector $\mathbf{M}$ depends on the number, orientation, position, and strength of the magnetic elements.

Accurate field strength calculations require accounting for all magnetic and metallic components in the system, along with precise knowledge of the measurement axes' positions.
The complexity of the calculations needed to determine the magnetic field strength led to the use of simulations and numerical methods. Determining the position based on the field strength using analytical methods would require the inverse equation to be bijective, which could not be the case for every magnet-sensor setup. Using the analytical method would require using a lookup table, which should contain around 3.5 million entries to be robust to translation noise, with each entry having at least 6 entry points (3 for position and at least 3 for sensor readings). This would require a large amount of space ($\geq 300MB$), which is not always present in low-level controllers with limited memory. 
% Hall-effect sensors
\section{Hall-effect sensor}
The Hall effect, discovered by Edwin Hall in 1879, describes the generation of a potential difference (the Hall voltage) across an electrical conductor when subjected to a perpendicular magnetic field. This phenomenon enables the measurement of magnetic field strength along the plane of the conducting plate. A visual representation of the effect is shown in \cref{fig:Hall effect}.

\begin{figure}[ht!]
\centering
\includegraphics[width=1\textwidth]{figures/Hall effect/Hall effect}
\caption{Schematic of the Hall effect principle.}
\label{fig:Hall effect}
\end{figure}

A Hall-effect sensor quantifies magnetic field strength by detecting the polarization of a conducting plate induced by the field. In this work, a Melexis 90393 3D Hall-effect sensor is employed to measure the magnetic field generated by permanent magnets embedded in the rotating joint component.
% Neural networks
\section{Neural network}
The relationship between the joint's movement and the sensor readings is nonlinear across all degrees of freedom. Due to the highly variant magnetic field, this nonlinearity manifests differently in each rotational plane. Consequently, advanced function approximation methods are required to model the system accurately.

Artificial neural networks (ANNs) are a well-established method for approximating complex functional behaviors. Theoretically, ANNs can approximate any continuous function to arbitrary precision \cite{hornik_multilayer_1989}. In this work, an ANN is employed to model the relationship between the Hall-effect sensor readings and the joint's angular position.

The ANN was selected for its simplicity of implementation and computational efficiency during training—critical advantages when evaluating numerous experimental configurations. Compared to more sophisticated machine learning algorithms, ANNs offer faster training times while maintaining sufficient modeling capability for this application.

 Because of the highly variant magnetic field, the nonlinear magnetic relationship is different in the different rotation planes. This calls for more advanced methods for function approximation. 
An artificial neural network is a method used to approximate the behavior of functions. Theoretically, every possible behavior could be captured via an artificial neural network. \cite{hornik_multilayer_1989}
An artificial neural network is being used to capture the relationship between the readings of the sensor and the position of the joint. It is simple to implement and is trained relatively fast in comparison to more advanced machine learning algorithms, which is key if the goal is to evaluate as many setups as possible. 


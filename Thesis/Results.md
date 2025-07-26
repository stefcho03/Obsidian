% !TeX spellcheck = en_US
% !TeX encoding = UTF-8
% !TeX root = ../thesis.tex

\chapter{Evaluation}
\section{Importance of magnetic field variance}
Low magnetic field variance makes extraction of information in certain ranges of motion impossible. In example in \ref{fig:bad_config simulation} a magnet was placed in the center of the moving part, with its polarization vector being parallel to one of the measurement axes. This made the angle estimation in the sagital plane (main rotation plane) impossible. The sensor readings are not changing with movement of the joint, which results in the poor performance of the Neural Network in \ref{fig:bad_config NN} trained with the data from the simulation. 
\label{fig:bad_config}
    \centering
    \subfigure[Simulated sensor readings of the visualized movement.]{\label{fig:bad_config simulation}\includegraphics[width=0.4\textwidth]{thesis-latex-template/figures/Results/Bad_configuration_simulation.png}}    
    \hspace{1cm}            
    \subfigure[Neural network predictions.]{\label{fig:circles}\includegraphics[width=0.5\textwidth]{thesis-latex-template/figures/Results/Bad_configuration_prediction.png}}                
    \caption{Results with bad configuration}
    \label{fig:bad_config NN}
    
\section{Two-sensor setups}
Firstly the setups with 2 sensors were simulated. The position of the sensors was expressed through polar coordinates - one for the angle offset and one for the center offset. Both of the sensors were placed on the same plane, and on the diameter of the static part, limiting the parameters to be optimized to 2. The magnet position and orientation were the same as in the example shown before (\ref{fig:bad_config}) and constant throughout the simulation. This allowed for the sensor position to be evaluated, being the only changing parameter.In total 96 2-sensor setups were evaluated. Figure \ref{fig: RMSE_2s} shows the RMSE of all simulated setups. The best setups had an RMSE of 2,181°. The sensors had 0° center offset (the magnet and both sensors were standing in a line in the starting position) and were offset from the center by 4 mm.
\begin{figure}
    \centering
    \includegraphics[width=0.5\linewidth]{thesis-latex-template/figures/Results/Figure_9 (RMSE_2s).png}
    \caption{RMSE of 2 sensor setups, sorted by error.}
    \label{fig:RMSE_2s}
\end{figure}
\section{Two-magnet setups}
Due to the large number of possible setups for 2 magnet setups, a few considerations are to be made. Firstly, only the setups creating large magnetic field variance are considered. This means limiting one magnet to only possible rotations of 0, 90 and -90 degrees around each axis and the second to 0, 45 and -45 degrees  around each axis. The centers of the magnets are also limited in one plane, meaning constant position in the z-axis.  
In total 1480 2-magnet setups were simulated and evaluated. The best achieved RMSE was 0.166. Figure{} shows the RMSE of the different setups, sorted by RMSE. The best-performing setup is the following: \\
	\textbf{Magnet 1}
    \begin{itemize}
        \item 6.5 mm offset from the center of the moving part
        \item 45 degrees rotated around the x-axis
    \end{itemize}
    	\textbf{Magnet 2}
    \begin{itemize}
        \item 4.5 mm offset from the center of the moving part
        \item 90 degrees rotated around the y-axis
    \end{itemize}
		 
This setup provides a lot of magnetic field variance with the polarization vectors oriented in different directions and not being a part of the sagittal plane. 
\begin{figure}
    \centering
    \includegraphics[width=0.5\linewidth]{thesis-latex-template/figures/Results/Figure_5 (RMSE 1 Sensor).png}
    \caption{RMSE of 2 magnet setups, sorted by error.}
    \label{fig:RMSE_2s}
\end{figure}
\section{Validation}
The trained neural networks were then tested on both simulated and real environments. The test consists of making predictions using the trained neural networks. An additional parameter - R$^2$ was added to show the correlation between prediction and actual angle. The higher the  R$^2$ coefficient - the higher the correlation
\subsection{Simulation}
The pure rotation (twist and bend degrees are 0) and pure twisting (rotation and bend degrees are 0) motion are predicted with high accuracy. Bending motion predictions however have no correlation with the actual degrees. Rotation motion is predicted accurately throughout the whole motion of bending and twisting motion. Twisting motion predictions have an offset depending on rotation and bending motion. 
\subsection{Experiment}
The best performing setup was transferred onto a real RCJ. The same pipeline was repeated, only this time using data, gathered with the experimental setup. This was done by moving the RCJ around and recording the sensor readings every degree. The gathered data was augmented using artificial noise. Different translations that were taken into account in the simulations were not part of the experimental data gathering due to the sophisticated setup, required for accurate translation through the whole range of motion. This, however does not make the gathered data any less accurate, because of the tensioning of the cables. The same kind of neural network was then trained and used to predict the angle. The prediction experiment was done by moving the joint around and recording the predictions and the actual angles every 2.5 degrees. Figure{} shows the relationship between predicted and actual angles in the real-world scenario. Figure{} shows the absolute error throughout the range of motion. The resulting error was kept under 3 degrees througout the whole 90 degrees. The RMSE was calculated to be 1.3 degrees. 

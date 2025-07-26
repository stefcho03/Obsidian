Slide 2:
One of the main problems with mechanical design of wearable exoskeleton joints is the misalignment issue. Oversimplified joint kinematics can lead to misalignment of the human and exoskeletons joint. This leads to discomfort, ineficient movement and in some cases - injury. The rolling contact joint proposed in Asfour et. al proposes a solution to the misalignment problem, offering closer mimicking of the human joint kinematics without redundant mechanical complexity. 

Slide 3:
It comes however with its challenges - conventional actuation and position estimation methods are not compatible with it. A contactless angle measuring method is required because of the 6DoF nature of the joint. This thesis investigates the position sensing performance of the RCJ relying on a contactless sensing method and proposes a way for evaluating different measuring setups.

Slide  5:
There are a lot of methods for contactless angle measurement, including optical, magneto-resistive and ultrasound methods. Most of them, however do not fit this use case due to various reasons such as their size, accuracy, resolution or setup requirements. The 2 compatible methods left are measurement with Hall-effect sensor and IMUs. IMUs however display the tendency to drift in prolonged use and have to be calibrated before each use.

Slide 6:
The use of Hall effect sensors for position estimation has been used successfully implemented before in different types of joints. 

Slide 7:
The ones that are of most interest for the goal of the thesis are Johnson et. al and Hoang et. al, because of the similarity in setups and  data evaluation

Slide 8:
Johnson et. al proposed a method for measuring the angle of rolling contact joints with array of sensors and a singular magnet. This solution does not provide a method for sensing the other 2 rotations.

Slide 9:
Hoang et. al shows the need for variance in the magnetic field. The proposed method makes use of 3 differently oriented permanent magnets and 4 sensors. The proposed method however takes a ball in socket joint, which's center of rotation is fixed and therefore not applicable for rolling contact joints. Also the use RNNs for estimating the relative movements instead of absolute position does not fit the goal of the thesis.

Slide 11:
For the goal of joint estimation a pipeline was created - firstly synthetic data was generated using python simulations. The data was then used to train neural networks, which were then evaluated and the best one was chosen to be validated in the real world. 

Slide 12:
For the data generation the python library magpylib was chosen because of its optimizations for magnetic field computations and the great visualization tools. 

Slide 13:
Using the artificial data, simple neural networks were trained to predict the rotation angles based on the sensor readings. Each magnet/sensor setup was used to train different neural network. The Neural Networks were then evaluated based on their RMSE.

Slide 14:
The setup that shows the best performance in providing the best training data for the neural network will be transferred to the real world and the same pipeline will be repeated, only this time with real training data. 

Slide 16:
The simulations confirmed the need of magnetic field variance when using one sensor. While the one magnet/sensor setup can work in 1DoF applications, in the case of multiple degrees of freedom applications variance is particularly important. Lack of variance will most probably cause large range of the main movement to be impossible to estimate in certain positions. 

Slide 17:
No change on the magnetic sensor readings results in an impossible prediction

Slide 18:
The results from the neural networks confirm the hypothesis that highly variant magnetic field is necessary if the goal is to estimate the angle using only one sensor. If the goal is to estimate the position using only one magnet, two sensors are required.

Slide 19:
Here is a plot of all of the tested setups with different angles of rotation. To prevent testing all of the possible setups, the rotation of the first magnet was limited to 0, 90 and -90, while the second was limited to 0, 45 and -45. This ensures enough variance while preventing the same setup being tested twice.

Slide 20:
The best setup among the tested ones is the one with different offsets and different rotations around different axes. This gives us maximal variance because of the polarities being orthogonal to each other while also not being limited to the same plane. 

Slide 21:
The setup was then transferred onto the real joint and its performance in predicting the main angle of rotation was tested. The ground truth is a 3D printed goniometer (?). The measured range of motion was 90 degrees. The possibility for translation was still there, depending on the tensioning of the joint.

Slide 22:
On this graph the simulated sensor measurements are compared with the actual ones. The behavior is very similar with the biggest error being on the x-Axis measurement. This is caused mostly by the influence of the pins that hold the ropes together and other small influences such as the magnetic field of the earth.

Slide 23:
On this graph we can see the results of the trained on real data neural network. Data augmentation was used to gather more samples than the ones gathered originally. Despite the relative small training sample, the trained neural network shows promising results in predicting the main angle of rotation. The absolute error is kept in the range of 3 degrees.

Slide 25:
Future work includes making more sophisticated setup for gathering of real data, that allows information from all 3 rotations to be gathered. Other possibility would be mapping the simulated data to the real data with the help of algorithms. Experimenting with 2 sensor should also be considered because of the better results shown in the simulations. This is however more complicated and requires development of custom PCBs. Other methods of angle prediction could also be considered. Fine tuning the already existing neural networks or implementation of new ones such as RNNs could deliver better results in the specific use cases.

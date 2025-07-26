Final presentation
	1. Cover slide
		Topic, Name, Supervisors, Professors
	2. Structure slide
		What is where
	3. Introduction
		Why is measuring the angle contactlessly important
		Why is the joint being introduced
	4. Methodology 
		Artificial data
			- Use of magpylib because of the numerical optimizations for magnetic field computation and its good visualization tools
			- gifs with the movement and magnetic field?
			- Multiple different magnet-sensor setups 
			- Simulating sensor readings for a lot of the joint configurations within the allowed movement range
		Training a simple neural network on the simulated data
			- Relationship nonlinear but still relatively simple 
			- Analytical solution would require minimizing an equation with a lot of variables that could also change depending on the number of magnets, their position and orientation, position and orientation of the sensor(s) and so on
			- Use of neural network does not require creating a new equation for each configuration
		Using the absolute error to determine a good setup
			- Images of the magnetic field with low and high variance
			- Transferring the best and worst setups on the real joint 
	5. Results
		Highly variant magnetic fields produce better results
		Use of 2 sensors much more effective
			- Using 2 magnets and one sensor for the real world experiment
			- +- 3 degrees of error in rotating plane
			- Video of using the resulting animation
		
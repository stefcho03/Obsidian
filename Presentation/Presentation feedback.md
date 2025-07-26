Also here is my feedback for the presentation:  

- of course it was really good, congratulations again

The comments I had were:  

- you could have spent a bit more time at the related work to explain the concepts, but I think you touched upon the most important aspects
- terminology was mostly consistent, at the end of the presentation you were using setup and configuration interchangeably
- I think we already talked about this, but every time you presented a plot, you said "as you can see" - but a better way is to say "This plot demostrates/shows ...". With the first sentence, you kind of rely on the interpretation from the viewers to understand the plots, in the second version, you base the findings on the plot and not on the audience. I hope this makes sense.
- For the plots that show the RMSE values with ordered configurations (blue dotted plot), you said 2 times that "The RMSE decreases over time", and I was not sure what you meant with this. Also, I was thinking for these dotted plots that show the configurations. I think it would make sense to plot them without the interpolation curve, only dots. Because these are discrete configuration, and there is actually nothing in between two configurations.

Comments from Tamim/audience (reconstructed from my and Charlotte's notes):  

- Stefan used only the needed words -> positive comment
- Is it relevant that one cylinder is not moving? Does it make a difference?
- What are the results for 1DoF simulation? -> better to compare it with real-world experiments - Table with RMSE including sim3DoF, sim1DoF, real1DoF
- Is 1.3 deg a good results? -> This question is a bit my fault. I promised you this paper that mentions what is good precision, but sadly I am unable to find it.
- What were the design goals? Target precision?
- Is the system affected by other objects from environment?
- So you also need calibration, how is this better than IMUs? - only one calibration, not multiple
- Wouldn't a classical regression be possible?
    - Tilman: Looks quadratical?
    - only 1 DoF not all 3DoF!
- Student: How did you gather the real data? Is it accurate enough?
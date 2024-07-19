# Project 1 - Automotive Performance Package
In this project, you'll simulate the logic for an automotive performance package. Vehicles today have dozens of computers that work together to adjust the car's behavior in response to data read from hundreds of sensors. In this simplified system, assume that you are responding to two sensors—speed and lateral acceleration—to decide between a "high performance" and "economy" mode.

![image](https://github.com/user-attachments/assets/23d21f2e-f785-41e2-a385-99fe91eeaef2)

In order to simulate the sensor data, the model uses a block that you haven't seen yet: the Signal Editor block.

![image](https://github.com/user-attachments/assets/e42cfc28-5f29-45f7-ac61-f231e7f41cdc)

Don't worry, though, Signal Editor is just another type of source, like Sine Wave or Ramp. You can inspect these signals by using what you learned previously, and by adding a Scope to the model.

# Step 1
You must first preprocess the input data. In particular, you must find the absolute value of lateral acceleration, so that the model treats left and right turns the same way.
Add an Abs (Simulink > Math Operations) block to take the absolute value of lateral acceleration.

# Step 2
This pseudocode describes the logic for choosing a driving mode.<br>

    if (speed >= 100 km/h) OR (speed >= 35 km/h AND abs(lateral acceleration) >= 3 m/s2) 
  
      use mode 2 
      
    else 
  
      use mode 1 
      
    end 
  
You will model the boolean statements in this step, then add the logic.
Add three Compare to Constant blocks to the model. Set their conditions accordingly.
Connect the blocks to their appropriate signals (e.g. >= 3 is related to acceleration). Remember you can branch any signal by using the right mouse button to click and drag.

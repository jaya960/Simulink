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

# Step 3
Add a Logical Operator block to the model. Use the default Operator value, AND. Connect the appropriate Compare to Constant blocks to create the statement: <br>

        speed >= 35 km/h AND abs(lateral acceleration) >= 3 m/s2

# Step 4
Add a second Logical Operator block to the model. Change its Operator to OR. Connect the blocks to create the statement: <br>

        (speed >= 100 km/h) OR (speed >= 35 km/h AND abs(lateral acceleration) >= 3 m/s2)

# Step 5
The final step is to add the logical statement, described here: <br>

    if (speed >= 100 km/h) OR (speed >= 35 km/h AND abs(lateral acceleration) >= 3 m/s2)
   
        use mode 2
        
    else
    
        use mode 1
        
    end

Add a Switch block to the model and connect the output from the previous task to the control signal. Add two Constant blocks, with values 1 and 2, to represent the driving modes. Connect the blocks to the appropriate locations on the Switch block.

# Step 6
You successfully modeled the logic for choosing a driving mode based on speed and acceleration data! To verify that this is performing as you expect, try adding a Scope block to the model.
Use the Scope to view three signals in the same window: speed, acceleration, and mode choice. You can plot the signals on separate axes using the View > Layout menu in the Scope toolbar.

# Observation
![image](https://github.com/user-attachments/assets/4d508400-743b-40f2-99d2-4756b0d854b5)

## Project - Thermostat Model

To keep the house comfortable, you might want to control the temperature, using a strategy based on the current and desired temperatures. This is called a control system, and is exactly what a thermostat is! Since most controllers are digital, they are often modeled as discrete systems.

![image](https://github.com/user-attachments/assets/20f2451b-7b07-42bb-afb1-5d282c278b27)

A controller measures the error between the set and measured temperatures and sends a command signal based on that error.

![image](https://github.com/user-attachments/assets/1bce9098-2ef8-4ef4-a3fb-1a5aea9840e0)

A controller measures the error between the set and measured temperatures and sends a command signal based on that error.For example, a very simple control strategy could be to turn the furnace on if the house is cold, and off if it is hot.

![image](https://github.com/user-attachments/assets/07392fee-3e2c-4c81-9db2-e8f15499b3dd)

For example, a very simple control strategy could be to turn the furnace on if the house is cold, and off if it is hot.The result, as shown here, is the proper average temperature, but with a lot of fluctuations.

![image](https://github.com/user-attachments/assets/be729286-454a-4da5-9086-529ff7964286)

Instead, you can specify the controller output as proportional to the error. For example, if the temperature is close to the set point, little heat is required. If the temperature difference is large, though, the heater should be at maximum power.

![image](https://github.com/user-attachments/assets/63a7afbd-8f12-4c56-babc-2880123b7fc6)

Instead, you can specify the controller output as proportional to the error. For example, if the temperature is close to the set point, little heat is required. If the temperature difference is large, though, the heater should be at maximum power.The result is a much more consistent temperature, but the temperature never quite reaches the set point. To address this, you can also consider the accumulated error over time.

![image](https://github.com/user-attachments/assets/9e465476-643f-4ef8-9c9c-15f9543af6f1)

The result is a much more consistent temperature, but the temperature never quite reaches the set point. To address this, you can also consider the accumulated error over time.This is done by integrating the error and increasing the control effort if the accumulated error grows. This type of control is aptly named proportional-integral, or PI, control.

![image](https://github.com/user-attachments/assets/0645d2e2-9ea4-4b55-83f7-a558df0897a5)

This is done by integrating the error and increasing the control effort if the accumulated error grows. This type of control is aptly named proportional-integral, or PI, control.In this project, you model the discrete equations representing a PI controller. The model contains a set temperature and a block representing the house, similar to the model you built previously. You must create the controller.

![image](https://github.com/user-attachments/assets/f0083465-c9d1-4ca6-bf05-c9ed6e5a70a0)

The design variables Kp and Ki, and the sample time Ts, have been defined in the MATLAB workspace.









# Project 1 - Automotive Performance Package
In this project, you'll simulate the logic for an automotive performance package. Vehicles today have dozens of computers that work together to adjust the car's behavior in response to data read from hundreds of sensors. In this simplified system, assume that you are responding to two sensors—speed and lateral acceleration—to decide between a "high performance" and "economy" mode.

![image](https://github.com/user-attachments/assets/23d21f2e-f785-41e2-a385-99fe91eeaef2)

In order to simulate the sensor data, the model uses a block that you haven't seen yet: the Signal Editor block.

![image](https://github.com/user-attachments/assets/e42cfc28-5f29-45f7-ac61-f231e7f41cdc)

Don't worry, though, Signal Editor is just another type of source, like Sine Wave or Ramp. You can inspect these signals by using what you learned previously, and by adding a Scope to the model.

## Step 1
You must first preprocess the input data. In particular, you must find the absolute value of lateral acceleration, so that the model treats left and right turns the same way.
Add an Abs (Simulink > Math Operations) block to take the absolute value of lateral acceleration.

## Step 2
This pseudocode describes the logic for choosing a driving mode.<br>

    if (speed >= 100 km/h) OR (speed >= 35 km/h AND abs(lateral acceleration) >= 3 m/s2) 
  
      use mode 2 
      
    else 
  
      use mode 1 
      
    end 
  
You will model the boolean statements in this step, then add the logic.
Add three Compare to Constant blocks to the model. Set their conditions accordingly.
Connect the blocks to their appropriate signals (e.g. >= 3 is related to acceleration). Remember you can branch any signal by using the right mouse button to click and drag.

## Step 3
Add a Logical Operator block to the model. Use the default Operator value, AND. Connect the appropriate Compare to Constant blocks to create the statement: <br>

        speed >= 35 km/h AND abs(lateral acceleration) >= 3 m/s2

## Step 4
Add a second Logical Operator block to the model. Change its Operator to OR. Connect the blocks to create the statement: <br>

        (speed >= 100 km/h) OR (speed >= 35 km/h AND abs(lateral acceleration) >= 3 m/s2)

## Step 5
The final step is to add the logical statement, described here: <br>

    if (speed >= 100 km/h) OR (speed >= 35 km/h AND abs(lateral acceleration) >= 3 m/s2)
   
        use mode 2
        
    else
    
        use mode 1
        
    end

Add a Switch block to the model and connect the output from the previous task to the control signal. Add two Constant blocks, with values 1 and 2, to represent the driving modes. Connect the blocks to the appropriate locations on the Switch block.

## Step 6
You successfully modeled the logic for choosing a driving mode based on speed and acceleration data! To verify that this is performing as you expect, try adding a Scope block to the model.
Use the Scope to view three signals in the same window: speed, acceleration, and mode choice. You can plot the signals on separate axes using the View > Layout menu in the Scope toolbar.

## Observation
![image](https://github.com/user-attachments/assets/4d508400-743b-40f2-99d2-4756b0d854b5)

# Project 2 - Thermostat Model

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

# Project 3 - Peregrine Falcon Dive

When diving for prey, the Peregrine falcon can reach speeds of up to 350 km/h. As the falcon dives, the two forces acting on it are gravity and air drag. The equation of motion for this is:

![image](https://github.com/user-attachments/assets/12d352f5-00f4-46ad-9ecd-34ea380e4b23)

As it approaches the ground, however, it changes the angle of its wings. This increases drag, which rapidly decelerates it to a safe landing speed. You can model this process in the equation of motion as a change in the area A and drag coefficient Cd. In this project, you must use Simulink to model this behavior in two parts. First, you model the equation of motion for a given set of drag parameters. In the second part, you model the wings opening to slow the bird down.

![image](https://github.com/user-attachments/assets/82fa2f9f-5373-4bd2-bac7-90060b6d9bdf)

Assume a fixed wing area A and drag coefficient Cd. The constants rho, g, Cd, m, and A have been defined as variables in the MATLAB workspace.
## Step 1
Add the appropriate number of Integrator blocks to the model. Create stubs of the signals and label them appropriately, following the notation v, v_dot for successive derivatives.

## Step 2
Use a Math Function block to square the velocity signal (v).
Add a Constant block with the value: 0.5*rho*Cd*A.
Multiply these two signals using a Product block.
Note: You can achieve steps 2 and 3 with a Gain block. However, to support the future logic for changing parameters mid-flight, please use a Product block.

## Step 3
The right side of the equation also contains the gravity term.
Add a Constant block with the value m*g. Use a Subtract block to construct the right side of the equation, incorporating the result of the previous task.

## Step 4
Next, you must equate the left and right sides of the equation of motion. Since you already have a signal for v_dot, try rearranging the equation as:

![image](https://github.com/user-attachments/assets/b3be60ad-4e6b-4c4c-872c-b5fd5b4eea2a)

This form shows that you must multiply the existing signal by 1/m.
Add a Gain block with the value 1/m, and connect it to the output of the Subtract block. Connect the unconnected port of the Gain block to the signal v_dot to create the equality.

## Step 5
Set the Initial condition for velocity to -10 (representing m/s).

## PART 2
In this first part of this project, you modeled the dive of a peregrine falcon with fixed parameters. Next, you'll add the logic to describe the falcon opening its wings and decelerating.
The next lesson begins with a version of this model where some blocks have been rearranged or reoriented. Organizing all of the states and integrators in a single row, with coefficients and other terms arranged below them, enables you to quickly characterize the system.
Try this yourself! Click on a block and select the Format tab of the Simulink toolstrip. Use the icons in the Arrange section to rotate or flip the selected block.

## Step 2.1
Add a Switch block to the model. This block selects the appropriate coefficients for the drag term, so connect the output of the Switch to the input of the Product block.

## Step 2.2
The falcon opens its wings when it senses that it is near the ground. Assume this occurs at a height of 15 meters. This pseudocode describes that behavior: <br>

        if h ≥ 15 m 
             Cd = Cd1, A = A1
        else
             Cd = Cd2, A = A2
        end
 
## Step 2.3
The switch condition depends on height, but the only states in the model are acceleration and velocity. You must add another Integrator block.
Add a second Integrator to the model. Branch v to the input of the new Integrator. Create a signal stub for the output of this Integrator block and label it h.

## Step 2.4
The output of this last integrator is the falcon's height, which is the signal that drives the switch condition.
Connect the height to the control signal (middle port) of the Switch block. Double-click the Switch block and set these parameters: <br>

> Criteria for passing first input: u2 >= Threshold <br>
> Threshold: 15 <br>

## Step 2.5
Since you added a new Integrator block, you must set its initial condition as well.
Set the Initial condition to 60 (representing meters).

## Step 2.6

At these speeds, a falcon's dive is over in just a few seconds.
Change the simulation Stop time to 2.5.

## Step 2.7
The behavior of the Switch block depends on height, but has a strong effect on velocity as well. Use a Scope to compare the two signals.

## Observation of Scope
![image](https://github.com/user-attachments/assets/03de00a9-3040-448b-b837-c507d2b24a98)









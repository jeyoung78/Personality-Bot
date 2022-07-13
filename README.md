1.0 Introduction
Due to Covid-19 people might not have the same social interaction as they had before, emotional support is needed more than ever. However, everyone is busy all the time adjusting to their new lifestyle. Human interaction through social media may not even be the answer for everyone’s emotional support. Thus, we have created the “Personality Bot.” The robot will play with you. It will have 5 states of emotion (tired, happy, sad, angry, and excited). When interacting with the robot in a certain way it will trigger any of these emotions.
2.0 Software Design and Implementation
The overall program of this robot is to provide the emotional response of a robot. The overall program of this robot splits up into six states of emotions for the robot (which is also the functions of the robot):
They are the Angry state, Happy state, Sad state, Asleep state, Excited state, and Tired state. To make the robot resemble emotional support (which is the problem we try to solve with our robot), we choose these emotions as they describe the normal emotion of every human being. The reasons why these tasks are chosen specifically are:
-	The Angry state: this state is chosen because it implements the IR beacon sensors. IR beacon sensors will let the robot follows the beacon holder and move toward them whenever it is “Angry”. It fits one of our constraints, as we need 4 types of inputs, and the IR sensor is one of them. 
-	The Happy state: this state is chosen because we want to implement the third motors to respond to the constraint. It implements the for-loop inside the function, which tells the robot to move his hand back and forth 5 times.
-	The Excited state: this state is chosen as a subsequent complimentary of the happy state. After being happy, the robot becomes excited. The robot will use the timer (which is one of the constraints) and compare itself to the live time when it becomes awake. 
-	The Sad state: This state happens with the implementation of the timer and sensor. If the IR Beacon does not find the user after the amount of time (which is 10 seconds with our robot), then the robot will have to move his back corresponding to the IR beacon (which is the decisions requirement for the code). The sad state takes in the beacon input for this state.
-	The Asleep state: this state is chosen because we need a starting point of the code. This state includes one of the inputs in the list of the four inputs, which is the accelerometer.
-	The Tired state: This state implements the last type of input, the touch sensors. We also use this state to reset the timer and use that timer again for the later application.
Task list for the demo: 
1.	Check if the robot can distinguish between the small contact and the large contact. The starting state of the robot is the asleep state. 
2.	Begins with the happy function, small contact will be tested first. The excited state will follow right after the happy state. The tired state will also follow that.
3.	Check if the happy state come back if the robot receives the touch sensor.
4.	Redo the happy state to back to the asleep state. 
5.	Check the angry state. Check the excited path first. 
6.	Redo the angry state, check for the sad path. The sad state will go to tired state. Do a final check if the robot returns to tired state.
There is a small change from earlier tasks lists. We decide not to use Enter button to end all tasks, but instead using stop the program after 10 seconds when the robot is in the asleep state. 
Table 1: List of Functions Used
	Function Parameter	Return Type	How it works
brake()	n/a	void	Whenever angry state and excited state end, this function is used to stop the robot’s movement. The function does so by simply setting the values of power of both motor A and D to zero.
goToState()	State of robot, acceleration of robot	int	When the robot changes an emotional state, it returns an integer that corresponds to the next emotional state. goToState() receives that integer and calls a function for the right emotional state. 
asleepState()	Acceleration of robot	int	asleep() function prompts for sensor value from accelerometer. While the accelerometer does not detect any value, meaning that the robot is not moving, the robot is not in any emotional state and thus does not take any action. Once it detects a motion, the robot wakes up and is in happy state. However, if one of the sensor values from the accelerometer exceeds hundred, meaning that the robot is pushed with a huge amount of force, the robot is in the angry state. 
happyState()	n/a	int	Once the robot detects a mild push, the robot is automatically in happy state, calling happyState() function. Once the function is called, it makes the arm attached to motor B wave five time with the use of for loop. 
angryState()	n/a	int	If the robot detects a strong push, the robot is in its angry state, calling angryState() function. Once the function is called, the robot makes roaring sound and chases the beacon at full speed. If the robot succeeds hitting the beacon, the robot is in excited state. If the robot fails hitting the beacon, it is in sad state. 
excitedState()	n/a	int	If the robot succeeds hitting the beacon, the robot is in excited state and calls excitedState function. For 10 seconds it rotates as fast as it can and goes into tired state. 
sadState()	n/a	int	The robot is in sad state when it fails to hit the beacon during angry state. For ten seconds, the robot will turn its back against the beacon with the use of turn() function. After ten seconds, the robot will call tired state.
tiredState()	n/a	int	Once the tiredState() function is called, the robot makes a noise which indicates that it is in tired state and waits for a touch for ten seconds. If it detects a motion within that ten seconds, the happyState() function is called, and if it does not the robot calls asleepState() function. 

Table 2: List of Data and How They are Stored
Variable	Data Type	Explanations
accelerometer	tHTAC	Acceleration of three directions, x, y, and z are stored in this variable. tHTAC is a struct that contains three integer values that correspond to x, y, and z acceleration of the robot. 
transition	int	This variable stores emotional state of the robot. For example, integer value of happy state is 1, sad state is 2, angry state is 3, and so on. This value is inputted to goToState function and is used to call function for the right emotional state. 
heading	float	This variable stores the direction of the beacon sensor that the IR sensor receives so that the robot can look towards or chase the beacon sensor when it is in happy or angry state. 
Count	int	This variable saves how many times did the robot wave its arm.

The software design decisions are split into three main steps [1]:

Software planning: 
-	There are a few constraints that we must build around, so the software planning is initially adapted to what the constraints are. The constraints of this project are to build a robot that is having the third motors, the use of at least 4 distinct types of inputs, the timers, repetitions, decisions and six nontrivial functions. As a result, our robot goes strictly around those constraints. 
-	The conceptualized process at that time is to build a robot that can work around these constraints, which we decide to work with the personality robots because of the evenly shared variety of the functions that our group is doing. 
-	Before working on the robot, we planned on building the 6 non-trivial functions that are evenly weight between the others. The 6 personalities - which are the design frames of our robot - are happy, asleep, excited, tired, sad, and angry. We have one or two linear connections between the personality of the robot, but for the most part, the personality of our robot is not fully linear. In other words, when the robot receives an emotion, the code ends. 
-	Our plan is grand, with the expectation that we can detect users with the distance at most equal to the whole WEEF LAB room. We also want our accelerometer to work without being finicky, as it is important that the robot can distinguish between a soft contact (for the happy response of the robot) or a strong contact (for the angry response of the robot) from the user. 

Design problem-solution co-evolution:
-	The co-evolution of the program occurs when we have the flow chart and have some connections between the emotions of the robot. After receiving advice, the connection between the emotional tasks of the robot changes. There are some linearity and strong decision connection between the emotions of the robots. For example, we can connect the tired state with the asleep state or connect the angry state with the sad state or the excited state. We realize it is important to connect all those states together, as it will create a more interesting robot with the unexpected emotions to the user. 

Design reasoning: 
-	There are some unexpected events that happened which our design be unable to follow precisely the flowchart that is presented. One of the problems is the limitations of sensor. For instance, regarding the IR beacon sensor, we could not make it so that the user could move anywhere and get the robot to find the user, but the robot can detect a range of around 1.5m. The IR sensor also gets hindered if there is object between the IR sensor and the beacon. As a result, our software decision is implementing that the user must be around the radius of 1.5m inside the robot sensing radius as our constraints for using this robot.
-	Our software decision takes into consideration of modularization and concurrency. The design verification of the demo shows that the robot works well under the modification of the design decisions after two weeks of work. 

Trade-off: 
-	The biggest trade off we encounter is between the distance the robot works get the output and the precision. As discussed above, if there is an object that is placed between the IR sensor and the beacon, the robot will not work. Our robot only works in a small area, and that 1m distance without obstruction is always important for the robot to work from the beginning to the end of the program.

3.0 Motors and Sensors Tests
First, we ensure that the sensors and motors were working properly. 
Motor test - We just ran a test to move all 3 motors by moving the motors forwards and then backwards.
Sensors test – After you hook up the touch, IR sensors, accelerometer and motor encoder to the different ports, use the EV brick to display and ensure the sensors are connected properly
1.	Touch sensor test – push the touch sensor to ensure the displayed value is changed
2.	IR sensor test – move the beacon around and ensure the displayed value is changing
3.	Accelerometer test – Ran the sample code hitechnic-accelerometer-test1.c and hitechnic-accelerometer.h inside the sample file of robotC to verify the accelerometer is working
4.	Motor Encoder test – use a tape to measure a preset distance and use the sample code from previous class to make the robot travel the preset distance.
 
Unit Test: The purpose is to test each state individually to confirm it is working as expected
 
Happy State - The robot will display a happy face on the screen, followed by waving its arm back and forth 5 times and then say the phrase “hello good morning”.

Test H1: Is the expression correct?
The robot should display the “Big smile.rgf” as shown in Figure 1 [2].
   
Figure 1: Happy State Facial Expression
Test H2: Does the accelerometer value corresponds to the display icon?
To confirm the accelerometer value, we have added a line of code to display the change of values in the accelerometer and this will confirm that the robot is in the happy state. This line of code will be displayed on the 2nd and 3rd line of the EV3 brick. This debug line of code will be commented out in the final version. 
Test H3: Does the arm wave back and forth 5 times? 
We tested the arm to move back and forth separately. Once we have confirmed that the robot arm can move back and forth, we made sure the robot arm moved back and forth five times.
 

Test H4: Does the robot say, “hello good morning”?
Ensure you can hear the phrase “hello good morning”
 
Angry State – The robot will display an angry face on the screen, followed by making T-rex sound and then it will turn to the user and start chasing the person holding the beacon for 10 seconds. The robot should stop after 10 seconds. The angry state action relies on the IR sensor and the beacon to work. The robot will move to follow the beacon.  

Asleep State - The robot will display a knocked-out face on the screen and produce a snore sound. If the robot is in the asleep state for longer than 10 seconds, the program will end. This should be the first state that the robot goes into once the program starts.  

Sad State – The robot will display a sad face on the screen, make a crying sound and followed by turn 180 degrees away from the direction of the beacon 

Tired State: The robot will display a tired face on the screen and wait for user interaction by using the touch sensor. If the robot is not interacted with within 10 seconds it will go to the Asleep state. If touch sensor detects user interaction during the 10 seconds, it should move to the Happy state.

Figure 7: Flow Chart of the Program
1. Asleep
If the human does not interact with the robot, the program will end. The Asleep state 	will show a Knockout face and have a snore sound.
2. Asleep->Happy->Excited->Tired-> Asleep
The Asleep state will show a Knockout face and have a snore sound. After the user nudges the robot, the robot will enter the Happy state. In the Happy state it will display a big smile and wave his hand 5 times back and forth and say “Hello Good morning”. Once completed the Happy state, it will go to the Excited state. This will spin in a circle for 10 seconds while displaying a crazy face. Then it will enter the Tired state which will display a tired face. Since we do not touch the touch sensor for 10 seconds, the robot will go back to the Asleep state. 
3. Asleep->Happy->Excited->Tired-> Happy
The Asleep state will show a Knockout face and have a snore sound. After user 	nudges the robot, the robot will enter the Happy state. In the Happy state it will display a big smile and wave his hand 5 times back and forth and say “Hello Good morning”. Once completed the Happy state, it will go to the Excited state. This will spin in a circle for 10 seconds while displaying a crazy face. Then it will enter the Tired state which will display a tired face. Since we touch the touch sensor within 10 seconds, the robot will go back to the Happy state.
4. Asleep->Angry->Sad->Tired
The Asleep state will show a Knockout face and have a snore sound. After user gives 	the robot a moderate push, the robot will enter the Angry state at which the robot will display an angry face, make T-rex sound, and start chasing the person holding the beacon. If the robot touch sensor has no contact of the person holding the beacon, the robot will enter the Sad state. During the Sad state, the robot will display a sad face, make a crying sound, followed by turn 180 degrees away from the person holding the beacon. It will then enter the Tired state.
5. Asleep->Angry->Excited
The Asleep state will show a Knockout face and have a snore sound. After user gives the robot a moderate push, the robot will enter the Angry state at which the robot will display an angry face, make T-rex sound, and start chasing the person holding the beacon. If the robot touch sensor has contact of the person holding the beacon, the robot will enter the Excited state. During the Excited state, the robot will display the crazy face and turn in circles for 10 seconds.
Significant Error
The significant error encountered was that the IR and beacon sensors were not as accurate as we had expected. Once the distance between the IR sensor and the beacon exceeds a meter, the sensors read only zero, and when the beacon sensor is behind the robot, the sensors read 50. 
The problem was resolved by the team using these incorrect measurements. For instance, we wanted the robot to turn away from the beacon sensor when it is in sad state. We took advantage of the fact that robot 

Conclusion and Recommendation

In conclusion, the robot has performed all of the tasks and achieves all the constraints. The robot has solved our problems that we laid out at the beginning – providing a friend for the user. The robot has incorporated the code to provide emotional support for the user, and it will assist in helping with emotional support for the user of the robot.  
If we had more time and it was for the industry, we would have made the robot more interactive. We would have added more emotional states and more diverse reactions for each emotional state so that users can feel the robot actually has a personality.  

References

[1] 	Antony Tang, Aldeida Aleti, Janet Burge, Hans van Vliet, "What makes software design effective?," 2010. [Online]. Available: https://www.sciencedirect.com/science/article/pii/S0142694X10000669. [Accessed 26 November 2021].
[2] 	N. Ward, "Lego EV3 standard bitmaps and sounds," [Online]. Available: https://sites.google.com/site/ev3basic/ev3-basic-programming/using-buttons-the-screen-and-the-leds/lego-ev3-standard-bitmaps. [Accessed 22 Nov 2021].



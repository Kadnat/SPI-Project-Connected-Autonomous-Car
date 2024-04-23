# SPI Project : Connected Autonomous Car

## Introduction
Autonomous vehicles, once considered mere elements of science fiction, are now at the forefront of technological development in the automotive industry. Advances in this sector promise to radically transform the way we conceive and approach mobility. At the intersection of artificial intelligence, robotics, and automotive engineering, these vehicles represent a major transition towards safer, more efficient, and environmentally friendly transportation systems.

As part of the Embedded Electrical and Electronic Systems Engineering program, and the Physics for Engineering Sciences project, we will undertake an approach to study, design, and develop a prototype of a scaled-down autonomous vehicle. This approach will allow us to explore and test existing technologies necessary for the realization of fully autonomous vehicles while providing a controlled and secure environment for development. Our efforts will focus on optimizing the perception, decision-making, and control systems of the prototype.

## Vehicle Chassis
Regarding the vehicle chassis, we have conducted 3D printing to make the steering fully operational.

![image](https://github.com/Kadnat/SPI-Project-Connected-Autonomous-Car/assets/126003868/d59d99ff-e19d-4597-a546-eee270283822)


## Speed Control
Concerning motor speed control, we have opted to use a PID controller. In order for the car to move at the same speed on both motors, we conducted a study on the motors' response to this type of control.

![image](https://github.com/Kadnat/SPI-Project-Connected-Autonomous-Car/assets/126003868/4420d0f0-6b31-47e5-ba2f-cbbde7241561)


### Development of Control Function
To implement this control function, we have acquired the following hardware:
- STM32F334R8 Microcontroller, which will serve as the brain to control our motors.
- Speed sensor with encoder wheel, to detect holes in the encoder wheel and determine the current speed of the motors.
- DG01D Motor, a DC motor.
- LN298N, the module that allows us to control the motors using PWM signals.
During one revolution of the motor, the speed sensor will generate 20 rising and falling edges. By setting an interrupt triggered at each transition of the encoder wheel and executing a function to calculate the period duration, we can determine the current speed of the corresponding motor.

![image](https://github.com/Kadnat/SPI-Project-Connected-Autonomous-Car/assets/126003868/2bcf730c-5f1f-4c56-b680-537a7a9f6dac)


Now that we obtain the motor speed, the PID control function needs to be executed at regular intervals. Here, the function will be executed every 20 ms (50 Hz).

## Position Control

To ensure precise line tracking, we have integrated position control using a Proportional controller, similar to the motor speed control.

### Development of Control Function

To implement this control function, we utilize the following hardware:
- STM32F334R8 Microcontroller, serving as the central control unit for directing the vehicle.
- QTR-8RC Position Sensor, featuring 8 reflection sensors, enabling precise positioning of the robot in relation to the line.
- MG996R Servomotor, responsible for aligning the car accurately.

In our approach to line tracking, each sensor in the QTR-8RC module is assigned a predefined score (1000 for the leftmost sensor and 8000 for the rightmost one), associated with a servomotor angle. When the center of the sensor array aligns with the line, we send a 90° signal to the servomotor. If the car deviates to the right, the leftmost sensor detects the line, and if it deviates to the left, the rightmost sensor detects the line. This information has enabled us to establish a linear equation that represents the correction to apply based on the sensor positions on the line:

Correction Equation:
$\Angle = 0.0171x + 13.2$

Where \(x\) ranges from 1000 to 8000, and the angle falls between 30° and 150°.

By implementing this correction equation, we ensure precise alignment with the line, enhancing the overall performance and stability of our autonomous vehicle.

![image](https://github.com/Kadnat/SPI-Project-Connected-Autonomous-Car/assets/126003868/b4a29126-2eee-4973-b963-4440aeda8b5c)


## Machine Learning

In order to enable the server, which processes images from the camera, to recognize predefined objects, we conducted training of the YOLOv5s model on annotated images. These annotations, generated using the label-studio tool, encompass figurines representing group members in various poses, as well as traffic signs indicating actions for the vehicle (STOP, END OF COURSE, TURN RIGHT).

To ensure robust object detection, we collected a diverse dataset comprising numerous photos taken from different angles and under varying lighting conditions.

Subsequently, utilizing this annotated dataset, we trained our model on Google Colaboratory. Leveraging Google's extensive computational resources facilitated swift model training, significantly enhancing efficiency.

To execute the object detection and decision-making process in real-time, our server, powered by an Orange Pi, runs the trained YOLOv5 model. This setup enables the server to process images captured by the camera and send commands to the microcontroller based on the detected objects.

Through the utilization of the YOLOv5 model and the Orange Pi server, our system achieves accurate and efficient recognition of predefined objects, including pedestrians and traffic signs. Upon detection, the server orchestrates the appropriate actions, ensuring the autonomous vehicle's adherence to traffic regulations and safe navigation.

![image](https://github.com/Kadnat/SPI-Project-Connected-Autonomous-Car/assets/126003868/2c1110ca-ec37-48e0-8253-53d1e3d0970b)

By leveraging the computational capabilities of the Orange Pi, we achieve seamless integration between machine learning-based object detection and control of the vehicle's operations, enhancing its overall functionality and reliability.

## Command Transmission

Upon detection of specific objects such as pedestrians or traffic signs by the server running the YOLOv5 model, corresponding actions are transmitted to the vehicle's microcontroller. For instance, the vehicle may slow down in pedestrian zones or come to a complete stop at a stop sign.

To facilitate this communication, the microcontroller is connected to an ESP01 module. The ESP01 module receives commands from the server and transmits them via USART, ensuring seamless integration between the decision-making process and the vehicle's control system.

By establishing this communication pathway, our system ensures timely and accurate execution of actions based on object detection, enhancing the vehicle's navigation capabilities and overall safety.

## Conclusion
This project has been extremely enriching for our group, particularly due to its multidisciplinary aspect. We have developed our knowledge in computer science, mechanics, energy, control systems, and electronics. We have covered a large part of the subjects taught in the S3E program offered at CESI, which has contributed to strengthening our skills.

## Project Video and Team Members

To witness our project in action, we invite you to watch the demonstration video: [Link to Project Video](https://www.youtube.com/watch?v=doNMiKrKpR8).

Meet the team behind this innovative endeavor:

- [Nathanaël BLAVO BALLARIN](https://www.linkedin.com/in/nathanael-blavo-ballarin/)
- [Clément BALSAN](https://www.linkedin.com/in/cl%C3%A9ment-balsan-068358234/)
- [Clément LARANJEIRA](https://www.linkedin.com/in/cl%C3%A9ment-laranjeira-11a389206/)
- [Aymeric MEROTTO](https://www.linkedin.com/in/aymeric-merotto-gibert-8b7bb41b2/)

Thank you for your interest in our project!


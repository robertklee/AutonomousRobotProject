# Autonomous Cable-Running Robot Project

This code was designed and written by Robert Lee for use in the ENGR 120 Spring 2017 autonomous cable-running robot project.

Robert Lee, Calder Staude, Kyle Jarvis, Kyra Teetzen

*University of Victoria*

*January-April 2017*

## Client Background
**This was a hypothetical project for a real-life UVic initiative**

Established in 2007, Ocean Networks Canada (ONC) is a UVic research initiative that is globally recognized for its leading-edge ocean observatories. ONC conducts vital research on the effects of climate change on ocean ecosystems, and protects the public by monitoring underwater seismic activities. ONC has equipped scientists with indispensable data to analyze complex Earth processes in pioneering new ways.

## Problem Definition 
Currently, ONC lacks a safe method to connect and run cables between nodes for its VENUS and NEPTUNE ocean observatories. A preliminary goal is to design a proof-of-concept dry-land prototype. This prototype should run the cable from a source to a target. To lessen damage to the environment, it should minimize wheel drag, and sense and avoid obstacles in its path. It should quickly locate a beacon in a confined area and approach it via a direct route. Each cycle must cost under $20, and the prototype must be fully autonomous. In addition, tests must be completed by March 21, 2017. The entire robot must cost under $800 and abide by CSA regulations. 

## Design
In teams of four, we developed dryland prototype robots to meet the client's need. We were all significantly involved in the mechanical, electrical, or software aspects of the project. 

### Algorithm Overview
Please see the ![Finite State Machine Diagram]("Milestone4 FSM diagram.pdf") for a detailed description of FSM.
The robot began its cycle in Target Acquisition State, where the robot rotated 360° and determined the direction of the strongest IR signal. During Approach State, it drove towards the beacon while performing slight trajectory adjustments by triangulating using the difference between its two front IR sensors. Periodically, it paused and entered Signal Revalidation State, pivoting 45° to each side and measuring signals from a 90° field of view to identify obstacles and recalculate the most efficient route. Once the robot was positioned for cable attachment, limit switches triggered and its magnetic connection mechanism lowered.

### Movement Mechanism
The robot used a skid-steer four-wheel drive mechanism. Two motors independently controlled each pair of wheels, enabling precise adjustments to either motor’s power to correct for route deviations. Its zero turning radius allowed it to carry the cable while maneuvering around obstacles. 

### Sensors and Controls
The robot utilized the following sensors to locate and approach the target:
* two limit switches: these ensured Marlin took corrective measures upon collision with obstacles
* an ultrasonic range finder (URF): this enabled Marlin to sense and avoid obstacles and control its approach to the beacon
* two IR phototransistors: these triangulated signal strength, ensuring a direct route, and if the left and right sensor deviance was too large, Signal Revalidation State was triggered

An integrated Vex computer combined input from these sensors to ensure that Marlin’s approach was direct, efficient, and reliable. 

### Material and Structure
The prototype featured a square frame and a small footprint, improving maneuverability in confined areas. It expends only a set of magnets per cycle.

## Final Design

After placing first in our lab, we significantly redesigned the project to use 8 infrared phototransistors instead of two. The placement of the **long-range** sensors were as follows:
* one each on left and right side
* one each on front left corner and front right corner
* one each on front middle left and front middle right

The placement of the **short-range** sensors were as follows:
* one each on front middle left and front middle right

By sensing the direction of the strongest IR signal, the robot can rotate either clockwise or counterclockwise towards the signal. The robot would use all long-range sensors to determine the direction of the strongest IR signal.

During rotation, the robot continuously monitors sensor values on the front corner IR sensors. As they cross a threshold, the robot rotation speed slows down proportionately, to account for angular inertia and reduce overshooting.

After identifying the direction, the robot drives at full speed towards the beacon, performing trajectory adjustments at over 10 Hz. As the long-range sensors (which have a high gain) saturated, the robot switched over to its short range sensors and ultrasonic rangefinder. By confirming its sensor values across both IR and ultrasonic sensors, it can greatly increase the confidence of its approach.

### Known Issues with Final Code
* The final code is not fully commented as the timeline for the redesign was very tight. 
* The robot behaves erratically if sunlight shines directly into its phototransistors

## Testing Criteria

Using ONC’s Request for Proposal, along with our own research into ONC, we have determined the following order of criteria for the ideal solution:
1.	**Consistency of task completion**: If the ideal solution only worked intermittently, it would introduce uncertainty into the already complicated process of cable-laying, potentially costing ONC time as well as money.
2.	**Environmental disturbance**: Since an important component of ONC is to conduct research on the ocean floor and monitor the health of the aquatic ecosystem, preserving the integrity of the ocean floor is very important. It would be counterproductive if the robot harmed the environment it was servicing.
3.	**Cycle Speed**: The robot should make the connection within a reasonable amount of time to reduce opportunities for object collisions or cable tangling.
4.	**Locomotive ability (forward motion straightness and turning radius)**: Cable-running robots should be nimble, precise, and predictable.
5.	**Detection of edge of arena**: The ideal solution should either sense or predict a collision and immediately perform corrective measures.

## Final Results
During the lab tests, the robot consistently and accurately passed all tests. All tests, even the long range test, were completed with minimal time loss due to an inefficient route. The average time was approximately 15-20 seconds to complete the task.

The final design with 8 phototransistors reduced this time to an average of 3-5 seconds. 
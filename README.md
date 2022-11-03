# DescendereSat

DescendereSat is the tethered CanSat (can-sized satellite model)  created for participation in the 2022 Annual CanSat Competition organized by American Astronautical Society (AAS) in United States of America. Developed by high school students, the design won the first place out of forty university teams from various countries.

DescendereSat is created to simulate the tether satellite, consists of a container and a payload. The payload is attached to the container by a 10 meter long tether. The DescendereSat is launched to an altitude of 700 meters above the launch site and deployed near apogee. Once the DescendereSat is ejected, the first parachute will be deployed reducing the descent rate to 5 m/s. At 300 meters, the DescendereSat will release a tethered payload to a distance of 10 meters in 20 seconds. During that time, the payload will maintain the orientation of a video camera pointing in the south direction. The video camera will be pointed 45 degrees downward to assure terrain is in the video.

## Table of contents
* [Casing Design](#casing-design)
* [Mechanism Design](#mechanism-design)
* [Electronics Design](#electronics-design)
* [Communcation and Data Handling](#communication-and-data-handling)
* [Flight Software](#flight-software)
* [Post Flight Analysis]((#post-flight-analysis)
## Casing Design
All mechanics and casing were designed in Fusion 360. The 3D model of the DescendereSat is shown in this link: 

### Container
The container is separated of three circular ribs due to the mass condition. They are connected to one another with carbon fiber rods forming a long cylinder. Each ribs stores different components; the upper part is the area for parachute storage, the middle located the circuits and the payload deployment mechanism, and the tethered payload is stored in the lower part. The gaps between the ribs are enclosed by plastic sheet to prevent small particles from entering the electronics.

### Payload
For the tethered payload, it is designed to be a slightly smaller cylinder than the container and its surface is designed to have hexagonal close packed pattern on it. With those tiny holes, the payload can reduce a considerable amount of weight (about 50% of the cylinder with same size) and also dissipating heat which generated from the electronics. The cameral gimbal is located at the lowest part of the tethered payload protruding from the bottom

## Mechanism Design

### Dual Deployment System
According to the mission, the CanSat needs to descend with different descent rates when reaching different altitudes. DescendereSat has two parachutes for different altitudes. Two parachutes are sewn to each other. The second parachute is stowed between the lids of the CanSat. The first parachute will be deployed immediately after ejected from the rocket. When the CanSat reaches 400 meter, the upper lid will be opened by a servo and t he second parachute will be deployed. The first parachute will be deflated spontaneuosly.

![image](https://user-images.githubusercontent.com/117327184/199677697-bb5db88a-7ee7-4721-9a2e-4563fe496820.png)

### Brake System
The tethered payload will be deployed by the _brake system_. This deploy system consists of two cylinders controlled by a servo
This mechanism can control the spooling of the tether by creating the friction between the surface of cylinders and the tether.
To stow the payload, the servo will rotate the cylinders and fold the tether. When the CanSat reaches 300 meters, the servo will be triggered, rotate the cylinders to unfold the tether, and deploy the payload.

![image](https://user-images.githubusercontent.com/117327184/199678757-d9de0f6c-d7aa-4a04-bcf5-9a1a24006fdc.png)





The videos below are the testing of the brake system


https://user-images.githubusercontent.com/117327184/199721815-442f8235-5298-4e6a-8ff4-740be9966ab5.mp4

https://user-images.githubusercontent.com/117327184/199721893-004fccd4-d25b-4e10-a86a-2ae3d51828ed.mp4



### Camera Gimbal
The camera gimbal uses 2 axes for better video quality. It has two servos and a rotation sensor mounted on it. The components is controlled by the payload's Teensy.

![image](https://user-images.githubusercontent.com/117327184/199683427-2868a688-fb1b-4a89-ae9a-7c806ab500a9.png)


## Electronics Design
### Sensors
DescendereSats collects 5 types of data, including altitude, air temperature, rotational motion, position and video. Here is the table showing sensors used to collect those data. 
![image](https://user-images.githubusercontent.com/117327184/199681950-76a323c5-1183-4da2-b535-cfaf7d12b91e.png)

### Container PCB

![image](https://user-images.githubusercontent.com/117327184/199683858-576ba486-14d9-4530-806b-2ea8415a3a2b.png)

### Payload PCB
![image](https://user-images.githubusercontent.com/117327184/199684308-458ba3e5-bac7-4a5e-ba4f-12d1c68c08f2.png)

***The container and payload PCB can be viewed in 3D through this link:*** 

### Power
For the container, 16650 2000 maH Li-ion is used. Here is the container electrical block diagram.
![image](https://user-images.githubusercontent.com/117327184/199684942-51590388-349d-4517-bb64-57f91565de36.png)
![image](https://user-images.githubusercontent.com/117327184/199685175-07a10db4-8777-49c2-badc-6eed6f74bc4b.png)

For the payload, 18350 1400 maH Li-ion is used. Here is the payload electrical block diagram.
![image](https://user-images.githubusercontent.com/117327184/199685247-b134850e-ec59-49ba-bd63-0b6ea949d823.png)
![image](https://user-images.githubusercontent.com/117327184/199685299-d8c31599-7b31-4b7f-812f-24f4d734048f.png)

**All container and payload power budget had been calculated. They were made to operate up to at least 4 hours.**

![image](https://user-images.githubusercontent.com/117327184/199685635-2c1f71ee-bce1-46ef-afcd-8d15c091c8cb.png)

## Communication and Data Handling

### Container CDH

![image](https://user-images.githubusercontent.com/117327184/199687476-058ff25c-dbaf-4df8-af9c-17b6c002b7c2.png)

### Payload CDH 

![image](https://user-images.githubusercontent.com/117327184/199687675-1af8238e-3d03-4b16-b7ad-af0083c88d4e.png)

## Flight Software
Overview of DescendereSat Flight Software Design
* The CanSat container will collect sensor data, save them to SD card, and send them to the ground station via XBee. 
* The CanSat payload sensor data will be requested by the container and sent to ground station via XBee of the container. 
* A self-rotating camera is included on the payload which will correct itself to point to the South.

C and C++ is the progamming lauguage used for both the container and payload. 

### Container FSW State Diagram

![image](https://user-images.githubusercontent.com/117327184/199689090-9888f3f5-f78f-4c95-8143-e31fa9376a14.png)

![image](https://user-images.githubusercontent.com/117327184/199689153-1b22bed3-4721-4b0b-8b7a-8ba8a20bce66.png)

### Payload FSW State Diagram 

![image](https://user-images.githubusercontent.com/117327184/199689220-cae1f7d9-7e24-4bfc-a794-c2ba3c407d01.png)

### Ground Station setup

## Post Flight Analysis
DescendereSat was lauched in Blacksburg Virginia on 11th June 2022 with the rocket provided by the competition. 

![rocket](https://user-images.githubusercontent.com/117327184/199715500-9df989a2-b200-451f-8b37-ee1e01780cdd.png)

The data are shown in the following graph.

![timealt](https://user-images.githubusercontent.com/117327184/199715614-ab3195b3-8aeb-44f4-a0b8-8ef356837814.png)

![fittedline](https://user-images.githubusercontent.com/117327184/199715632-58fe51b4-35a8-466e-8700-afd19a8153e2.png)

![altlonglatitude](https://user-images.githubusercontent.com/117327184/199715651-dd63860b-89f0-4a3a-a284-7ae9485186cd.png)

![Xacc](https://user-images.githubusercontent.com/117327184/199715750-397e7224-5450-4ec5-bfab-4e5e92726547.png)

![Yacc](https://user-images.githubusercontent.com/117327184/199715764-bc95a0e6-2827-4e01-a057-08b3ca394bf8.png)

![Zacc](https://user-images.githubusercontent.com/117327184/199715784-b46aebd7-7d95-4afd-b29b-ddefc2042be1.png)

Overall, 

Welcome to IndiN (Indoor Intelligent Navigation)
===================


**Hello World!** This is our prototype for **United By HCL Hackathon 2017**.  This repository contains content  for Phase 2 Submission of the hackathon. We hope you find it awesome, as we did while writing it. <i class="icon-heart"></i>

>- **Note** - We have separate descriptions and screenshots inside each of the modules you see here. If you wanna skip the introduction here,  jump right into code, But we **strongly recommend** you to go through this page first, as it provides a clear introduction to our project and its capabilities. Do check it out!
>- You will find our Android Submission here, **don't worry we've got iOS also covered**, But just for the sake of brevity. We'll talk about Android here.


----------

Title - IndiN (Indoor Intelligent Navigation)
===================

![WorkFlow Diagram](https://lh3.googleusercontent.com/-kKH7G_lTGRA/WXRAYR0RL0I/AAAAAAAAK-o/waRnnrT-cKI5a3vDblcrIvQbcdVvSZVQQCE0YBhgL/s0/UnitedByHCL1.png "UnitedByHCL1.png")

2.	Contextual Information & Workflow  
-------------
The Global Navigation Satellite Systems (GNSS) suffer from accuracy deterioration and outages in dense urban canyons and are almost unavailable for indoor environments. Nowadays, developing indoor positioning systems has become an attractive research topic due to the increasing demands on ubiquitous positioning. As smartphones and other mobile devices become ubiquitous, applications that are able to harness contextual information such as position become increasingly powerful. Uses for indoor localization systems include context-based targeted advertising, emergency response and assisted living, robotics applications, and indoor navigation in places such as airports, malls, and campuses. 

Indoor localization research has garnered a good deal of interest from both academia and industry. It has been presented in numerous ways with different levels of accuracy and feasibility, but has still been sibylline and has not leveraged the full potential of the existing infrastructure. 

Recent models use a single wireless technology for mapping the user in space as using either Wi-Fi, Bluetooth, RFID or Infrared. These solutions do not quite hit the mark, due to limitations of individual technologies in indoor space.

It is known that Wi-Fi signals diffuse in space and have greater coverage on the other hand, RFID and Bluetooth only work in a very small limited range. Due to requirement of significant infrastructural changes and dedicated sensors, these systems incur a heavy cost of deployment. The associated cost makes it feasible only to deploy a minimum number of such sensors in the premise, resulting errors in positioning. Lastly, the Infrared based positioning systems suffer from limitations such as low data rate and strict directionality, which are decisive for the performance of an indoor positioning system. 
 
Our prototype concocts the best of above stated methods along with technologies such as NFC and On-Device Pedometer (Accelerometer + Gyroscope) to improve performance and quality of the resulting navigation system.

It is based on ‘Fingerprinting’ approach of localisation to locate the user in space utilising a nearest neighbour in signal space. Localization systems that use a nearest neighbour in signal space approach require collection of data points throughout the room or building they will be deployed in. To predict a position, a new set of attributes constituting a new data point is compared with every point in the classified dataset. Depending on the implementation of the k-Nearest Neighbour algorithm, the coordinates of the closest point are used as the coordinates for the new point or an average of k closest points can be used with different weights. These instance-based machine learning approaches can achieve accuracies up to 2 meters on average, but current research is limited in that and only one or few algorithms are considered and even they don’t take into account many of the sensors available in most modern mobile devices. Further, these algorithms are limited by the size of the dataset. A very large dataset will require a substantial amount of time to predict a position, hindering real-world deployment. 

we have examined a large number of machine learning algorithms for indoor localization based on the sensors readily available in smartphones. We have found algorithms giving an accuracy up to 0.76 meters on average in a real- world environment without the need for dedicated hardware or changes to infrastructure, outperforming algorithms considered in previous research.

In the next section, we discuss the operation of our prototype model.


----------
![Block Diagram](https://lh3.googleusercontent.com/-KFJ821R-Jp8/WXRAnQKXJgI/AAAAAAAAK-0/rtw73-1poVIP1QSFlMER1feajrb2pR4CACLcBGAs/s0/BlockDiagramHCL.png "BlockDiagramHCL.png")

3.	Procedure  
-------------
AIM: To deploy a cost-efficient Indoor Positioning System for multi-storey building using Wi-Fi, Bluetooth, Phone's Accelerometer

Using MapWize SDK to map the building.

1.	First of all, we require the initial position of user, for that we can use
NFC (Near Field Communication) in the smart phone (if present) to detect entry in the building OR we can use last GPS reading on the device. Advantage of NFC is that it can detect entry location, eliminate the use of ID card and speeding up the process.

2. Once the user is inside the building, we employ Wi-Fi Fingerprinting using Wi-Fi’s RSSI and MAC address for our base localization. Accuracy of the Wi-Fi is approx. 15m so it is not a standalone viable option, but can be used to determine the floor, or pinpoint the subsection. Only Wi-Fi is required to be enabled on the user’s mobile device and doesn’t need to be connected, so no security threats. Today, mostly all organisations already have Wi-Fi infrastructure, so no additional costs are involved.

3. To improve the accuracy we utilise Bluetooth technology, inexpensive Bluetooth beacons must be installed in the facility for the same. These beacons send out unique signals using which the app determines position relative to access points. Advantages of Bluetooth indoor positioning system is that it uses the UUID and RSSI values of the Bluetooth beacon to pinpoint the location of that device by the accuracy of 1m. Besides that, it is extremely energy efficient. The problem here arises that each detection requires a minimum of 3 beacons and there are only so many devices we could deploy in a building. Further, the average range of these beacons is only 30 meters so, it might not work in a large hall or an open space. To overcome these shortcomings we would be using data from On-device Accelerometer and Gyroscope, serving as a digital Pedometer.

4. This enhances resilience of the system as, even when there is insufficient data from Bluetooth, we can rely on the pedometer (Accelerometer + Gyroscope) data from the last known location to track the user movement. until the connection with one of the Bluetooth beacons could be established again. This technique works fine for small distance and also overcomes the limitations of the previously mentioned techniques such as tracking of direction and orientation of the user.  

To take things further, we integrate our custom-designed ‘Phone Position’ module, which can detect the position of the phone with respect to the human body, i.e., in hand, in bag, in pocket etc. This results in greater accuracy in calculation of user position based on data received from on-device sensors.


----------


Additional Implementation details
-------------
> -	To accomplish this, a CMS (Content Management System) will be deployed on the Local servers to communicate with each mobile device. Even though the above processing can work on client device, it is highly power consuming and could use too much computation power which might not be available on devices such as smart watches. 

> -	To minimise the computation on client device, we will offload the computationally intensive work loads to the local server which will provide the client device with processed navigational information.

> - It will relay RSSI values to a Real-time Database, query the real-time database for its calculated position and will receive contextual information relating to its position inside the building where beacons have been setup. 

> - Bluetooth discovery is moved to the Bluetooth hotspots. When a hotspot detects a device in its range, it sends information to the server. To reduce traffic and computation, the server side database is updated only when a device enters or leaves the range of a hotspot.



----------


Advantages:
--------------------
•	An advantage of this model is its ability to increase the scanning frequency on the Bluetooth hotspots. Usually, mobile devices cannot operate with a high frequency of Bluetooth scanning, which is recommended to be as high as once each 10 or 14 seconds, making the system power efficient.

•	The system is highly modularized with low level of coupling, this allows multiple modules present to work on top of each other enhancing accuracy and performance. All modules (Bluetooth module, Wi-Fi Fingerprinting module and Phone position module) work on top of the foundational Pedometer module and are optional in nature, i.e. presence of these modules enhances accuracy and quality whereas absence doesn’t halt the navigation.

•	The Scanning for position change is done very frequently, whereas data transmission between server and device takes place after a certain fixed interval, this results in data saving and less congestion on the network.

•	Unprecedented level of accuracy (up to 0.5 m) achieved using combination of several on device sensors and Machine Learning algorithms on the server.

•	Over the complete system, we assume that Bluetooth and Wi-Fi scanning are performed independently and asynchronously. Also this system will only work when there is a movement detected through accelerometer reading, reducing unnecessary computations and improving power efficiency even further.

•	The system is built on top of common infrastructural facilities such as Wi-Fi and fully leverages the power of multiple on-device sensors. Except for use of Bluetooth beacons, which also are used in quite less number than in case of existing architectures. The result is an overall system which is inexpensive, performant and adaptive.

•	The application would be available for Android and iOS with support for Smart watches.

Technology Stack  
-------------

•	Hardware and Services
		>-	Bluetooth Beacons
		>-	Wi-Fi 
		>-	Smartphone & Smart Watch

•	Android 
		>-	Android Studio 3 (Java/Kotlin)
		>-	MapWize SDK for Android
		>-	WEKA
		>-	Volley
		>-	NFC module
		>-	Google Analytics

•	iOS
		>-	Xcode 9, Swift 4 and Frameworks - 
			Mapwize SDK for iOS
			SwiftLocation
			Hydra 
			Alamofire etc.
		>-	Realm Mobile Platform for Real-time Database and Synchronisation
		>-	Google Cloud Platform/ Heroku for Test Deployment


Concluding Remarks  
-------------
We are pleased to see you here! We sincerely Hope you like our submission. Its **100% Working**, We dearly look forward to Phase 3, where we can show you **IndiN** in all its might upon integration of all its modules presented above. We also made a brief video to show you how it works! Its here #Link.
We've seen it and it is surely <i class="icon-heart"></i>. We are very confident that you'll love it too.

See you at Old Trafford! (If you let us : ) )

Best Wishes!
**Team VisionArray**
**INDIA**

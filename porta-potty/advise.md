# (Advise) Smart Porta-Potty

> Title: Smart Porta Potty Design <br>
> Date: 2026-05-6
> Author: Clark Miller <br>
> Version: V1 <br>
> Client: Mayor Matts Otten <br>
> Company: City VoidVille <br>

# 1. Table of Contents
- [(Advise) Smart Porta-Potty](#advise-smart-porta-potty)
- [1. Table of Contents](#1-table-of-contents)
- [2. Introduction](#2-introduction)
  - [2.1 Context](#21-context)
  - [2.2 Target Audience](#22-target-audience)
  - [2.3 Main Question](#23-main-question)
    - [Sub Questions](#sub-questions)
- [3. Creating a new instance of the porta potty](#3-creating-a-new-instance-of-the-porta-potty)
  - [3.1 Chapter Introduction](#31-chapter-introduction)
  - [3.2 Explanation](#32-explanation)
- [4. The commands available to the porta potty](#4-the-commands-available-to-the-porta-potty)
  - [4.1 Chapter Introduction](#41-chapter-introduction)
  - [4.2 setOccupancy command](#42-setoccupancy-command)
- [5. The data returned from GET](#5-the-data-returned-from-get)
  - [5.1 Chapter Introduction](#51-chapter-introduction)
  - [5.2 Explanation](#52-explanation)
- [6. Conclusion](#6-conclusion)
- [6. Recommendations](#6-recommendations)
- [7. References](#7-references)

# 2. Introduction
## 2.1 Context
Our city has a smart porta-potty. However, it has no backend integration and has a lot of data which the backend system could benefit from.

## 2.2 Target Audience
This document is for the backend engineers of smart city who can use the data collected from the sensors and the overall state to predict future occupancy and where more toilets should be installed.

## 2.3 Main Question
How can a new porta potty be created, interacted with via commands and what data is accessible via a GET request?

### Sub Questions
- How can a new porta potty be created?
- What are the commands to interact with the porta potty?
- What data is accessible via the GET method of the porta potty?

# 3. Creating a new instance of the porta potty
## 3.1 Chapter Introduction
In this chapter the required fields needed to create a POST request to instantiate a new porta potty in memory on the ESP32.

## 3.2 Explanation
Firstly the structure of the embedded device needs to be known. It requires the same context any module needs which is the displayName. The ID value is generated when the device is created. Each of the pin values are the exact pins the device uses. The required fields are as seen in figure 3.1
**Code Snippet 3.1: GET Request Example for Porta-Potty**
```json
{
    "displayName": "Porta Potty",
    "ldrPin": 18,
    "laserPin": 41,
    "statusLED": {
        "redPin": 47,
        "greenPin": 48,
        "bluePin": 45
    }
}
```

Secondly, a POST request is made to the embedded device at http://DEVICE_IP_ADDRESS/module/PortaPottyModule

Finally in conclusion, by creating the correct JSON document and sending it as a post request to the ESP32. A new porta potty can be created on the device.

# 4. The commands available to the porta potty
## 4.1 Chapter Introduction
In this chapter we explore the command options for the porta-potty.

## 4.2 setOccupancy command
Firstly, the porta-potty only has a single command "setOccupancy". This is because of the simplicity of the module which has limited I/O options.

Secondly the command has one single field in the JSON body "occupancyStatus" which can take three different values: "OCCUPIED", "VACANT", "OUT_OF_SERVICE".

Thirdly if the OUT_OF_SERVICE occupancy is set, then the porta-potty will start flashing orange to signal to workers that service is needed and will not change states until the setOccupancy command is sent again with either "VACANT" or "OCCUPIED".

Finally in conclusion, while there is only one command available to the porta potty, it's good enough for now to drive the main state.

# 5. The data returned from GET
## 5.1 Chapter Introduction
In this chapter we explore the data available for the porta potty via a GET request.

## 5.2 Explanation
Firstly, as seen in figure 5.1 the module boilerplate methods are present. Which are id, displayName, moduleType.

**Code Snippet 5.1: GET Request Example for Porta-Potty**
```json
{
    "id": 2,
    "displayName": "Porta Potty",
    "moduleType": "PortaPottyModule",
    "occupancy": "OCCUPIED",
    "laserPin": 41,
    "ldrPin": 18,
    "statusLED": {
        "redPin": 47,
        "greenPin": 48,
        "bluePin": 45
    }
}
```

Secondly there are the fields for each pin being used including each pins which maps to the RGB LED. 

Thirdly, the most important value for the backend system asides from the module values is the occupancy value. This value determines if the porta potty has a person inside, doesn't have a person, or is out of service.

Finally in conclusion the GET request provides a complete summary of every pin used by the porta potty, the module values and the occupancy.

# 6. Conclusion
The smart porta-potty system is easy to set up, control, and monitor. With a simple API and clear data structure, it provides all the information needed for backend integration and future expansion. This approach helps the city manage public toilets more efficiently and improves the experience for everyone.


# 6. Recommendations
I reccomend that you create an endpoint in the backend to create these porta-potties, but also store their location so that a map could be created to show real-time availability and to pretend hot spots which could need more accomodations. 

# 7. References
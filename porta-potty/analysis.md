# (Analysis) Smart Porta-Potty

> Title: Smart Porta Potty Analysis <br>
> Date: 2026-04-23
> Author: Clark Miller <br>
> Version: V1 <br>
> Client: Mayor Matts Olts <br>
> Company: City VoidVille <br>

# 1. Table of Contents
- [(Analysis) Smart Porta-Potty](#analysis-smart-porta-potty)
- [1. Table of Contents](#1-table-of-contents)
- [2. Introduction](#2-introduction)
	- [2. Context](#2-context)
	- [2.2 Target Audience](#22-target-audience)
	- [2.3 Main Question](#23-main-question)
		- [Sub Questions](#sub-questions)
- [3. Porta potty definition](#3-porta-potty-definition)
	- [3.1 Chapter Introduction](#31-chapter-introduction)
	- [3.2 Explanation](#32-explanation)
- [4. Detecting Occupancy](#4-detecting-occupancy)
	- [4.1 Chapter Introduction](#41-chapter-introduction)
	- [4.2 Sensor Research](#42-sensor-research)
- [5. Alerting Occupancy](#5-alerting-occupancy)
	- [5.1 Chapter Introduction](#51-chapter-introduction)
	- [5.2 Displaying Occupancy Status: Research and Choices](#52-displaying-occupancy-status-research-and-choices)
- [6. Conclusion](#6-conclusion)
- [7. Recommendation](#7-recommendation)
- [8. References](#8-references)

# 2. Introduction
## 2. Context
Every city needs toilet facilities accessible to the public. However, the current solutions aren't very smart. Often a person who needs to use the washroom can waste time walking to a facility only to find out it's occupied or out of service. 

## 2.2 Target Audience
Mayor Matts Olts.
## 2.3 Main Question
What is a porta-potty, how can I detect if a porta potty in an available, occupied or out of service state and alert users visually of that state.
### Sub Questions
- What is a porta-potty?
- How can I detect if the porta potty is occupied?
- How can I indicate if the porta potty is available, occupied, or out of service using a visible signal?

# 3. Porta potty definition
## 3.1 Chapter Introduction
In this chapter we explore the definition of a porta-potty and why they're used.

## 3.2 Explanation
Firstly a porta-potty is "a toilet inside a small light building that can be moved from place to place (Oxford Learner's Dictionaries, n.d.).".

Secondly they're used because they because they "play a crucial role in addressing global sanitation needs at events, construction sites, disaster areas, and remote locations (Maczukin et al., 2026).".

Finally in conclusion, porta-potties are toilets inside a small portable light building which play a crucial role for sanitation needs for different venues like construction sites, events etc.

# 4. Detecting Occupancy
## 4.1 Chapter Introduction
In this chapter, we explore how to detect whether a toilet is occupied. The goal is to find a sensor solution that fits the scale and constraints of a model porta-potty.

## 4.2 Sensor Research
Firstly, I began by researching the different sensors commonly used for detecting a person. The most popular solutions were the PIR sensor and the Ultrasonic sensor as seen here (Arduino: 39 free guides for sensors and modules .n.d). However, these sensors are not ideal for the small scale of the porta-potty.

Secondly, considering the limitations of the above sensors, I explored alternative approaches. My intuition led me to try a laser tripwire, which is both fun and uniquely suited to the scale of this project. This method uses two small, affordable components from the provided kit and solves the scale issue effectively.

Thirdly, I found many existing solutions for building a laser tripwire online. One helpful resource was Miller (2014), "How to build a laser tripwire with Arduino" (Envato Tuts+). I will use his solution with some adaptions to power the tripwire logic.

Finally in conclusion even though there are more popular methods for occupancy detection, the best approach that fits the scale of the porta-potty is the laser tripwire.

# 5. Alerting Occupancy
## 5.1 Chapter Introduction
In this chapter, we examine how to display the occupancy of the toilet in a way that helps prevent people from wasting time walking to a facility only to find it occupied. The goal is to use a simple and effective method to show the different occupancy states.

## 5.2 Displaying Occupancy Status: Research and Choices
Firstly, I researched different output components that could be used to show occupancy, as seen in this article (Arduino: 39 free guides for sensors and modules, n.d.). My initial thought was to use an OLED screen to display text such as "OCCUPIED", "UNOCCUPIED", or "NEEDS SERVICE". However, this approach has drawbacks: if a tourist does not speak English, they may not understand the message, and in real-world use, screens are expensive and prone to damage.

Secondly, I considered using an RGB LED as an alternative. The colors green and red are globally recognized for "go" and "stop" or "Red is for danger, green for hope. (Kress & Van Leeuwen, 2002).", making them easy to understand regardless of language. However, this solution needed to account for more than just occupied and unoccupied states. For example, a "needs service" state could be triggered if the detector fails, occupancy is detected for too long, or the sensor is obstructed.

Thirdly, after weighing the options, I determined that an RGB LED is the best fit for this application. It is simple, affordable, and provides clear, recognizable signals for all necessary states.

Finally in conclusion, the best solution for easy recognition of state, simplicity, and affordability is to use an RGB LED with recognizable colors.

# 6. Conclusion
Non-smart toilets often fail to alert users about occupancy, leading to wasted time and frustration. By combining a laser tripwire for reliable occupancy detection with a clear RGB LED indicator, this solution provides a simple, affordable, and effective way to visually communicate toilet status at a distance. This approach should significantly improve user experience by saving time and reducing uncertainty.

# 7. Recommendation
I reccomend that you roll out smart porta-potties for the city and that you pass off the design documentation to the embedded engineers of the city to implement the porta-potties.

# 8. References
Santos, S. (2023, September 7). Arduino: 39 free guides for sensors and modules | random nerd tutorials. https://randomnerdtutorials.com/arduino-free-guides-sensors-modules/
Miller, B. (2014, June 27). How to build a laser tripwire with Arduino | Envato Tuts+. tutsplus.com. https://code.tutsplus.com/how-to-build-a-laser-tripwire-with-arduino--cms-21485t 
(Porta-Potty Noun - Definition, Pictures, Pronunciation and Usage Notes | Oxford Advanced Learner’s Dictionary at Oxfordlearnersdictionaries. Com, n.d.)
Maczukin, J., Yazıcıoğlu, A., & Ciesielski, S. (2026). The Future of Portable Sanitation: From Harmful Chemicals to Sustainable Green Cleaning Technologies. Sustainability, 18(6), 2828. https://doi.org/10.3390/su18062828
Kress, G., & Van Leeuwen, T. (2002). Colour as a semiotic mode: Notes for a grammar of colour. Visual Communication, 1(3), 343–368. https://doi.org/10.1177/147035720200100306
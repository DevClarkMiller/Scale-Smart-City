# (Analysis) Smart Gates Analysis

> Title: Smart Gates Analysis <br>
> Date: 2026-05-19
> Author: Clark Miller <br>
> Version: V1 <br>
> Client: Mayor Mats Otten <br>
> Company: City VoidVille <br>

# 1. Table of Contents
- [(Analysis) Smart Gates Analysis](#analysis-smart-gates-analysis)
- [1. Table of Contents](#1-table-of-contents)
- [2. Introduction](#2-introduction)
  - [2. Context](#2-context)
  - [2.2 Target Audience](#22-target-audience)
  - [2.3 Main Question](#23-main-question)
    - [Sub Questions](#sub-questions)
- [3. Payments Methods](#3-payments-methods)
  - [3.1 Chapter Introduction](#31-chapter-introduction)
  - [3.2 Contents](#32-contents)
  - [3.3 Chapter Conclusion](#33-chapter-conclusion)
- [4. Pricing Models](#4-pricing-models)
  - [4.1 Chapter Introduction](#41-chapter-introduction)
  - [4.2 Contents](#42-contents)
  - [4.3 Chapter Conclusion](#43-chapter-conclusion)
- [5. Conclusion](#5-conclusion)
- [6. Recommendation](#6-recommendation)
- [7. References](#7-references)

# 2. Introduction
## 2. Context
Globally, many cities are moving toward smart infrastructure and cashless payment systems to manage traffic, reduce congestion, and create new revenue streams.

At the City VoidVille level, the municipal budget is under pressure and there is growing interest in leveraging city assets to generate sustainable income.

The specific problem to solve is how to implement a smart gate toll system that provides a reliable payment method and pricing model, while integrating with the city’s embedded systems for transaction verification.

## 2.2 Target Audience
The mayor of City Voidville Matts Otten, he is the primary decision maker of the city and decides what should be implemented depending on if it solves a
genuine problem and makes sense as a solution.

## 2.3 Main Question
How can I generate revenue for the city using toll booths?

### Sub Questions
- Which payment methods could be used?
- Which pricing model should the city use?

# 3. Payments Methods
## 3.1 Chapter Introduction
This chapter explores the different possible cash-less payments methods the toll booth could use.

## 3.2 Contents
Firstly there are contact payments which require the toll payer to interact with a system before they're granted entry. 
In the EU things are mostly cashless using credit. 
However, in the Dutch Market other payment methods are used like iDeal and Tikkie.

Secondly Tikkie is "a digital payment application in the Netherlands that enables users to send payment requests directly to others through messaging platforms like WhatsApp, making it easy to settle personal transactions. The app also allows payments via QR code (Nyakurukwa et al., 2025)". This platforms focus is primarily on simplifying payments which friends, but also empowers businesses to create payments.

![Figure 1: Tikkie on a mobile phone](https://res.cloudinary.com/cb-media/image/upload/f_avif,w_auto:300:800,q_auto:eco:sensitive/cmsmedia/prod/binaries/content/gallery/cbhippowebsite/tests/betaalrekening/afbeeldingen/tikkie-app-eerste-indruk.jpg)

*Figure 1: Tikkie on a mobile phone. (betaalrekeningen, et al., 2026)*

Thirdly there are also contactless payments methods which are "admission-fee payment at the toll gate of an expressway without stopping (Hanaoka et al., n.d.)". Big toll highways use a computer vision system as as seen in figure 2 called "Automatic License Plate Recognition (ALPR) is also known as License Plate Recognition or License Plate Recognition (Uday et al., 2023)" where the license plate read can then be "used in various applications such as electronic payment gateway systems (Uday et al., 2023)".

![Figure 2: Barrier-free tolling](https://www.e-consystems.com/blog/camera/wp-content/uploads/2025/07/Barrier-free-tolling.jpg)

*Figure 2: Barrier-free tolling. (Kumar, D., 2025)*

## 3.3 Chapter Conclusion
Finally in conclusion we have several payment methods to choose from.

Firstly we can use credit which is a heavily used solution in the EU.

Secondly there is Tikkie and that is used frequently in the Dutch market.
  
Thirdly Computer Visions solutions can be used to avoid physical contact all together.

These the first two payment methods are scoped to different markets and the computer visions systems can be used to avoid slowing down traffic.

# 4. Pricing Models
## 4.1 Chapter Introduction
This chapters explains the different pricing models which the toll payment system could use.

## 4.2 Contents
Firstly the simplest payment model is the flat-fee payment. This is typically seen on linear roads where "motorists travelling in either direction paying a flat fee either when they enter or when they exit the toll road (Wikipedia contributors 2026)". This pricing model is most typically used in combination with contact payment systems. 

Secondly a more complex pricing model can be used which is the distance based (DB) model. "DB pricing relies on users paying the toll according to their effective distance of motorway travel, i.e., the number of kilometers traveled between toll gates. (Glavić et al., 2021)". This is often used in conjunction with Automatic License Plate Recognition (ALPR) utilized systems.

Thirdly "Instead, of paying for the product or service each time the customer uses it, the subscription business model allows users to register and use the product or the service at regular intervals. (Sandaruwan et al., 2020)". This system is also often combined with an ALPR to remove friction points.

## 4.3 Chapter Conclusion
This chapter reviewed three viable pricing models for the City VoidVille smart gate.

Firstly flat-fee entry charges are straightforward to implement and work well for low-frequency users.

Secondly distance-based tolling is fairer for varying trip lengths and is a good fit for ALPR or electronic toll collection systems.

Thirdly subscription-based access is convenient for regular commuters and can reduce transaction friction.

Each model has a role depending on the desired balance between simplicity, fairness, and recurring revenue.

# 5. Conclusion
The main question is: How can City VoidVille generate revenue using toll booths? This document shows that the city can do this by combining a modern payment method with a pricing model that fits the local market and the goals of the smart gate.

Firstly some of the payment methods we have available are Credit, Tikkie, and a Contact-less Computer Vision solution.

Secondly we have multiple options available for the pricing model including: Flat-Fee, Distance-Based, and Subscription Based.

These payment methods and pricing models work together to fulfil the requirements of different use cases. There isn't one method which fulfil all different cases.

# 6. Recommendation
Due to the scope of the project and the need for a simple, locally relevant payment flow, Tikkie should be used as the primary payment method for the smart gate. Tikkie is already familiar in the Dutch market and supports mobile, cashless payments that can be integrated with a toll booth interface or QR-based entry system.

For pricing, the flat-fee model is the recommended starting point. It is easy to understand for users, simple to implement, and can be administered through a single entry charge at the gate. This approach minimizes transaction complexity while still allowing City VoidVille to generate revenue from private-road access.

If the project expands, the architecture should remain open to later support additional payment options (such as iDeal or credit cards) and more advanced pricing schemes (distance-based or subscription access). However, for the current smart gate design, the combination of Tikkie and a flat-fee toll best fits the scope and local user expectations.

# 7. References
Uday, S., Patil, U., Mane, S., Gangurde, N., Hasabe, A., Sutar, A., Kale, M., Shrivas, S., & Patkar, U. (2023). Recognition of vehicle number plate for collection of toll. Research paper, 1334–1341. 

HANAOKA, G., NISHIOKA, T., ZHENG, Y., & IMAI, H. (n.d.). An optimized credit-payment system for expressway toll ... - cdn. wpmucdn.com. https://bpb-us-w2.wpmucdn.com/sites.uab.edu/dist/a/68/files/2020/01/CrypTec99-ETC.pdf 

Sandaruwan, L. A. C. A. (2020). A STUDY ON SUBSCRIPTION BASED TOLL COLLECTION SCHEME FOR SRI LANKAN EXPRESSWAYS.

Nyakurukwa, K., Seetharam, Y., & Chipeta, C. (2025). The role of acquaintances' characteristics in shaping digital payment technology. Finance Research Letters, 76, 106976.

betaalrekeningen, I. Z.-E. (2026, January 26). Tikkie: Hoe Werkt Het?. Consumentenbond. https://www.consumentenbond.nl/betaalrekening/tikkie 

Kumar, D. (2025, November 7). Role of AI-powered ALPR cameras in automated toll collection and traffic flow management. e-consystems.com. https://www.e-consystems.com/blog/camera/applications/role-of-ai-powered-alpr-cameras-in-automated-toll-collection-and-traffic-flow-management/ 

Wikipedia contributors. (2026, March 28). Toll road. In Wikipedia, The Free Encyclopedia. Retrieved 12:41, May 21, 2026, from https://en.wikipedia.org/w/index.php?title=Toll_road&oldid=1345819869

Glavić, D., Mladenović, M. N., Milenković, M., & Malenkovska Todorova, M. (2021). User perspectives on distance- and time-based road tolling schemes: European case study. Journal of Transportation Engineering, Part A: Systems, 147(9), 05021005. https://doi.org/10.1061/JTEPBS.0000558
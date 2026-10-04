# (Advise) Smart Gates Advise

> Title: Smart Gates Advise <br>
> Date: 2026-05-21
> Author: Clark Miller <br>
> Version: V1 <br>
> Client: Mayor Mats Otten <br>
> Company: City VoidVille <br>

# 1. Table of Contents
- [(Advise) Smart Gates Advise](#advise-smart-gates-advise)
- [1. Table of Contents](#1-table-of-contents)
- [2. Introduction](#2-introduction)
  - [2.1 Context](#21-context)
  - [2.2 Target Audience](#22-target-audience)
  - [2.3 Main Question](#23-main-question)
    - [Sub Questions](#sub-questions)
- [3. Contact Payment](#3-contact-payment)
  - [3.1 Chapter Introduction](#31-chapter-introduction)
  - [3.2 Contents](#32-contents)
  - [3.3 Chapter Conclusion](#33-chapter-conclusion)
- [4. Flat-Fee Pricing](#4-flat-fee-pricing)
  - [4.1 Chapter Introduction](#41-chapter-introduction)
  - [4.2 Contents](#42-contents)
  - [4.3 Chapter Conclusion](#43-chapter-conclusion)
- [5. Conclusion](#5-conclusion)
- [6. Recommendations](#6-recommendations)
- [7. References](#7-references)

# 2. Introduction
## 2.1 Context
Globally, many cities are moving toward smart infrastructure and cashless payment systems to manage traffic, reduce congestion, and create new revenue streams.

At the City VoidVille level, the municipal budget is under pressure and there is growing interest in leveraging city assets to generate sustainable income.

The specific problem to solve is how to implement a smart gate toll system that provides a reliable payment method and pricing model, while integrating with the city’s embedded systems for transaction verification.

This advice document draws directly from the findings in `docs/gate/analysis.md` and recommends the best payment and pricing choices for City VoidVille’s smart gate within the current technical and local market context.

## 2.2 Target Audience
The target audience is Mayor Mats Otten and the City VoidVille smart-city implementation team, including embedded systems engineers and decision makers who need a practical, low-risk gate payment design.

## 2.3 Main Question
How should City VoidVille implement a smart gate payment solution that is simple, reliable, and locally appropriate?

### Sub Questions
- Should the  smart gate use Tikkie as the primary payment method?
- Is flat-fee pricing the best model for the first deployment?

# 3. Contact Payment
## 3.1 Chapter Introduction
This chapter evaluates contact payment approaches and explains why one method is most suitable for City VoidVille. It draws directly from section 3 of `docs/gate/analysis.md`, which compared contact payments, mobile app solutions, and contactless alternatives.

## 3.2 Contents
Firstly contact payment methods require the user to actively complete a transaction before gate access is granted. In City VoidVille’s context, the most relevant option is a mobile payment request displayed as a QR code.

Secondly, Tikkie is a strong fit because it is widely used in the Netherlands and easy for local residents to adopt. It also supports QR-code payments, which align with the city’s embedded hardware plan for displaying payment requests on an OLED screen.

Thirdly the `analysis.md` document already identified Tikkie as the most locally relevant cashless option for the Dutch market, compared with generic card payments and more complex ALPR systems.

Fourthly compared to credit-card terminals or full ALPR solutions, Tikkie is lower risk and simpler to integrate. It avoids additional hardware and leverages a payment flow that is already familiar to Dutch users.

## 3.3 Chapter Conclusion
Tikkie should be used as the payment provider for our city.

Firstly the relevant payment option for our city is a mobile payment request display on a QR Code.

Secondly Tikkies widely used in the Netherlands with QR Code support, this fits into the simple scope of our city.

Thirdly Tikkie is the most simple relevant Dutch market solution for our city.

Fourthly Tikkie is a lower risk and simpler to integrate compared to complex ALPR systems.

# 4. Flat-Fee Pricing
## 4.1 Chapter Introduction
This chapter explains why flat-fee pricing is the preferred model for the first smart gate deployment. It builds on the pricing model comparison from section 4 of `docs/gate/analysis.md`, where flat fee, distance-based, and subscription models were evaluated.

## 4.2 Contents
Firstly, flat-fee pricing charges a fixed amount for each gate passage. This method is simple, easy for users to understand, and straightforward to implement.

Secondly for City VoidVille, flat-fee pricing avoids the need for distance-based tracking, subscription management, or per-kilometer calculations. That keeps the first phase of the project focused on a dependable payment flow rather than complex billing logic.

Thirdly a flat fee also aligns well with a Tikkie-based QR flow: the system only needs to generate one payment request per passage and verify one successful payment before opening the gate. This reduces the chance of user confusion and minimizes failure modes.

## 4.3 Chapter Conclusion
Flat-fee pricing is the best option at the moment for our toll gate in our smart city.

Firstly flat-fee pricing is easy to understand and is straightforward to implement.

Secondly flat-fee pricing keeps the payment flow dependable and avoids too much complexiity for the scope of our project.

Thirdly the flat-fee is a good match for a contact payment solution like Tikkie.

# 5. Conclusion
The main question is: How should City VoidVille implement a smart gate payment solution that is simple, reliable, and locally appropriate? This document document advised on which solutions should be used.

For City VoidVille’s smart gate project, the recommended solution is to use Tikkie as the contact payment method and a flat-fee pricing model.

Firstly Tikkie should be used as the payment method because of its wide-spread use in the Dutch market along with its ease of use.

Secondly the flat-fee pricing model should be used because it fits into the simple scope of our city and is highly compatible with the Tikkie contact payment method.

# 6. Recommendations
1. Select Tikkie as the primary payment method and implement the gate payment flow around a QR-code payment request.
2. Use a flat-fee charge for each gate passage to keep the billing model simple and predictable.
3. Validate payment status before opening the gate using the embedded system’s transaction verification logic.
4. Design the architecture so that future expansion can support additional payment options or pricing models if needed.

# 7. References
Miller, C. (2026, May 19). [Smart Gates Analysis](analysis.md). City VoidVille.
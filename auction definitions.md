# **Programmatic Auction Definitions**

#### Executive Summary	
The Media Rating Council (MRC’s) set standards for transparency, disclosure and reporting of various aspects and results of digital advertising auctions via their Digital Advertising Auction Transparency working group. In collaboration with these efforts, Tech Lab was asked to provide a primer and glossary about digital auctions. This document will help give all ecosystem participants common vocabulary and understanding of the way a digital auction works.

#### Audience	
The audience of this document is brand and agency leaders, with a desire to better understand programmatic auction mechanics.

#### Overview
A programmatic auction is part of the process to determine how an advertisement is delivered into a relevant ad placement. The programmatic supply chain includes the buy and sell side companies that orchestrate such an opportunity. Programmatic auctions are executed in a variety of ways, but they share common roles and execution flows. In some cases a single company may execute multiple roles described. 

The initial section of this primer provides a simplified description of the ad request and bid response process. Subsequent sections build on the simplified example to provide further detail and real-world use cases.

These terms will help orient the reader through our first simplified auction example:

- **Ad Request:** The information about the ad impression to be auctioned.
- **Ad Inventory Controller:** An entity that has the right of sale for the ad opportunity. 
- **Ad Request Initiators:** The systems that create ad requests, at the instruction of the ad inventory controllers. 
- **Selling Platform:** An entity that routes ad requests from an ad request initiator to participants in the supply chain. 
- **Buying Platform:** An entity that services advertising campaigns by evaluating, based on the information provided in ad requests they receive, if impression opportunities meet campaign requirements and making offers to purchase those that do. 
- **Bid Response:** The information about an ad from a buying platform and the offer that the buyer is willing to make for the impression. 
- **Auction:** The process an entity receiving competing bids uses to qualify, evaluate, and decide which to pursue and which to ignore. Decisions are based on the relative value and fitness of each bid.
- **Final Auctioneer:** The system that determines which bid, if any, is accepted for the impression opportunity.

#### Simplified Example
An ad inventory controller instructs an ad request initiator to send an ad request to selling platforms. The selling platforms in turn send requests to buying platforms. Buying platforms may then reply to the request with bid responses. The collection of bid responses returned to sellers enters into an auction. Winners are determined and the final auctioneer concludes which ads to render in the stated ad environment.


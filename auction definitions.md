# **Programmatic Auction Definitions**

### Executive Summary	
The Media Rating Council (MRC’s) set standards for transparency, disclosure and reporting of various aspects and results of digital advertising auctions via their Digital Advertising Auction Transparency working group. In collaboration with these efforts, Tech Lab was asked to provide a primer and glossary about digital auctions. This document will help give all ecosystem participants common vocabulary and understanding of the way a digital auction works.

### Audience	
The audience of this document is brand and agency leaders, with a desire to better understand programmatic auction mechanics.

### Overview
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


#### Auctions and Value
All stages in the programmatic supply chain may conduct auctions. Some may be simple, and some may be complex, but all of them take a list of bids and determine which, one or many, have the highest relative value to be returned upstream. 

Value is a critical concept in all stages of the flow. Few auctions are executed purely based on price, although price is often a heavily weighed signal. Some other examples of evaluation criteria include:

- Media owners may prioritize campaigns sold directly by their sales teams over programmatic regardless of cost.
- Buying platforms may prioritize bids for campaigns that are not meeting their delivery requirements over higher priced campaigns.
- All parties may prioritize bids based on their business and revenue goals.
- A party may decrease the relative value of a bid due to historical ad retrieval errors with the buyer (e.g., the creative is more likely to have a VAST error occur)
- Meeting competitive separation requirements (e.g., a broadcaster may have a deal with an advertiser to not show ads from competitors in the same ad break).
- Meeting frequency capping requirements (e.g., don't show an ad more than 3 times a day to the same user).
- All parties may filter based on acceptable ad formats, advertisers, etc.

### Auction Workflow
*Steps 0-2 are commonly executed between the ad inventory controller and the ad request initiators.*

#### Step 0) Ad Inventory Setup: 
Ad inventory owners will have configured placement(s) detailing where and when they wish ads to be shown on their website or in app, usually integrated with a final auctioneer. This is generally the ad inventory owner’s ad server. It holds a definitive configuration for the ad slots. It is ultimately responsible for filling the slot with an ad, whether from a campaign the ad server has itself (direct sold), or by reaching out to programmatic partners that may have demand for that opportunity.

The auction process begins when the slot isn’t immediately filled with a direct sold campaign.

#### *Programmatic Demand* 
*In which the ad request initiator requests a selling platform(s) to solicit bids. This very often uses the OpenRTB specification.*

*With programmatic demand it is usually the case that ad request initiators call multiple selling platforms. 
It is also possible that each selling platform may call (n) additional selling platforms in a single ad request initiation. Generally this is called a multi-hop supply chain. This, for example, could be selling platform A selling to selling platform B selling to buying platform A. Thus, this process could happen recursively, with steps 3 - 11 being performed in each successive supply chain hop. In practice, more than 2-3 hops is rare and generally suboptimal.* 

#### Step 1). Ad Request Initiation: 
Ad request initiator will create an ad request for a selling platform, populating various necessary information describing the property where the ad will be shown, the placement type, context, requirements, device, and user or audience attributes.  

#### Step 2) Ad Request Validation: 
A selling platform receives the request and should validate the ad request. There are many steps here including supply chain authorization by the seller (this may include validating ads.txt, sellers.json, and the supply chain object), validation of the device and IDs and other business process checks.
If the ad request is malformed or unauthorized, then processing should stop.

#### Step 3) Ad Request Enrichment: 
A selling platform may enrich the inventory owner’s ad request with additional features, such as audience data based on the relationship of the intended recipient.   
 
#### Step 4) Bid Solicitation: 
Ad requests are sent to eligible demand partners. Not all requests are sent to every demand partner. This could be due to business rules (e.g. a demand partner does not want traffic from a certain geography) or algorithmic decisions (e.g. the sending system predicts no response from the buying system).

#### Step 5) Bid: 
Buying platforms will make their own determinations on how to decide which bid(s) to return. This may include evaluation of multiple campaigns, and the value of the relative value of the impression to the various campaigns. The solicitation step results in four general conditions: You may receive no response, an error, a no-bid response, or a response with bid(s).

Responses that return bids typically include bid price that is most often net of fees, and where applicable, a deal ID. Examples can be found in the OpenRTB specification.

#### Step 6) Validate Returned Bids: 
Returned bids are the bids received from the buying platform(s). They must pass technical validation. Error cases here include:
- received after timeout expired
- unparsable response
- invalid values in response
- missing fields required by the seller

This step will result in zero or more bids that the seller can further evaluate.

#### Step 7) Qualifying Received Bids: 
For the bids that pass the technical validation step, the next step is business rules qualification. This includes checking the bid’s price against pricing rules, verifying the bid’s seat and the advertiser against any seller constraints like allow and block lists (e.g. categories, ad domains, buyer seats, creatives IDs, etc.). The process may also validate that bids with DealIDs conform to the deal terms. This step will result in zero or more bids that the seller has determined are acceptable.

#### Step 8) Competition: 
Each bid may compete within the auction at a determined auction price. Price may incorporate buying platform fees or discounts to establish an auction price that represents the net price for the seller. The price used in an auction varies by participant in the digital supply chain. A winner(s) for this auction is selected.

#### Step 9) Return winning bid(s): 
Intermediary auctioneers may forward more than one accepted bid to upstream partners, some or all of which may be sent to the final auctioneer who chooses the ultimate winner.

Buying platforms may include URLs in their bid responses that sellers can use to signal to losing buyers the loss reason by replacing a URL parameter macro with a standard loss reason code. 

#### Step 10) Waiting for Ad Rendering: 
The final auctioneer performs a final set of validation and qualification steps and makes a winner selection and will attempt to deliver the winning ad to the user.

Even in the case of the final auctioneer choosing to render the ad, the user may have left the page or paused the content, or some other technical reason may prevent the ad from rendering.

At time of delivery, various beacons should fire to notify participants that an ad has been rendered and transactions should be recorded.  

#### *Direct Demand* 
Further commenting on step 10, it should be noted that the selling platform’s winning bid does not equate to the winning bid for the final auctioneer. In many cases, the final auctioneer, e.g. publisher ad server, may receive the winning bid from the selling platform and never render it, as another business rule filled the ad request slot instead. Examples of this may include direct sold demand by the publisher or another programmatic auction triggered subsequently achieving a higher yield for the ad inventory owner. 

#### Step 11) Transaction Recording: 
Once the selling platform receives notifications of rendering and transactions, the bid should be recorded as impressions and transactions. Fees, clearing price, billable price, and other telemetry should be recorded in a ledger or ledger-like system. Notification of such is also returned to the buying platform for record keeping.

#### Step 12) Reconciliation: 
While this document won’t cover this in detail, it's acknowledged that most companies participating in auctions have monthly processes in which numbers between systems match up, and manage discrepancies.

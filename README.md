## Overview
The Digital Asset Management software industry is a highly fragmented market.  There are at least 200 vendors and some estimates place the true number in the thousands.  Although they all have digital assets as a consistent theme, there is little else which unites them and no common standard for exchanging data.  

At the same time as an exponential growth in the number of platforms, there has been a corresponding increase in the range of specialist tools and add-ons which enhance the functionality of DAMs.  It is practically impossible for any DAM developer to not need to utilise one or more third party products now in order to compete with their peers.  

This has created a significant issue for both DAM tool developers and vendors, alike.  In the case of the former, it means taking bets on which vendors are likely to provide them with the widest possible target market and/or developing a wide range of different connectors.  All of these require dedicated maintenance and if the vendor changes their API, the connector has to change also.  This adds a considerable overhead in terms of not only cost but also development staff time (and arguably the latter is a more serious issue).

The situation for DAM vendors is far from ideal also.  If there is particular tool they want to integrate with because customers have asked for it, they either need to persuade the tool provider to develop connectors and/or fund implementation of it themselves.  

One option which a number of tool vendors take is to choose generic fie sharing platforms like Dropbox, Google Drive or Box.  This then requires DAM vendors for whom there is no custom connector to use the aforementioned products as de-facto intermediaries.  This places them at a further disadvantage, especially when they want to highlight the advantages of dedicated DAM solutions as compared with file sharing alternatives.

The fundamental issue at the heart of all this is the lack of any interoperability standards or protocols in DAM.  In terms of what prevents the industry achieving a greater level of enterprise penetration, this is possibly one of the biggest challenges (if not the largest).

## Enter SimpleDAM
Standards and interoperability protocols have been talked about for decades in DAM.  Countless people have repeated the line about what an ‘important’ development it would be, but no one has actually done anything practical in terms of a protocol you can use.  Long-term DAM News readers will no doubt be aware that ‘the leadership’ of the DAM market tend to say very little about this issue.  Whether this is because they don’t care, don’t know (or possibly both) is a question that others can ask of them.

Having grown tired of waiting for the DAM market to do something about an issue which poses an existential threat to itself, we have decided to take matters into our own hands and have developed an API protocol called ‘SimpleDAM’.  This is a very basic REST-based API standard which defines some core common features which nearly all DAM systems offer. 

To demonstrate that the protocol is credible, we have implemented a very simple API-First DAM application which uses it.  You can see this in-action here: https://simpledam.damnews.org/  

An administrator account is available also, to get access to that, you need to join the SimpleDAM Google Group: SimpleDAM - Google Groups - https://groups.google.com/u/2/g/simpledam 

The documentation is here: https://simpledam.damnews.org/docs/   

## Licence
SimpleDAM has a three clause BSD open source licence which is one of the more permissive open source licences.  You don’t need to pay anything to start using it.

## Implementation Details
The code for the application is available on Github [link], but this is just to provide an example application and a test front-end.  Either your DAM (or your tool which connects with it) needs to be able to respond to REST-based calls and process JSON data.  The test application is written in PHP and uses jQuery, but providing you stick to the protocol and serve JSON back to clients, you are free to use whatever implementation technology you choose.

## Simple DAM Compatibility Level
There are currently two levels of SimpleDAM Compatibility: 0 and 1.  To be SimpleDAM compliant, a minimum of level 0 is required.  Using the documentation page, you can filter out features above level 0. 

Level 1 features are not necessary for the basics of getting assets into and out of a DAM.  For the most part, these exist to illustrate how SimpleDAM can be extended in the future without compromising the core input/output requirements.

## Getting started
Having played around with the test application and seen what JSON data it returns, the easiest way to get started is to download the front-end source code and start to implement server-side handlers for processing the calls issued to it.  When your front-end is connected to your implementation of SimpleDAM, it should behave in a more or less identical way to the test application.

If you are a tool vendor, you can use the demo application to build a SimpleDAM connector which should work with any other DAM which follows the same protocol.  We have a testbed/sandbox where it is possible to issue SimpleDAM calls which developers might find useful also, this is [link].

We fully expect problems and issues to come to light.  The place to discuss these is on the SimpleDAM Google Group, which we strongly encourage you to join.

## Issues and Areas for Improvement
This is the first edition of SimpleDAM and, as such, there will almost inevitably be changes and improvements which need to be implemented.  There are three key areas where changes are expected:

 - Authentication
 - Metadata
 - Collections/lightboxes & other advanced functionality

## Authentication
The authentication method in SimpleDAM is too simplistic.  Issuing a username and password in the code to login is potentially insecure and will require an alternative approach.  There are many options, such as using API tokens or other protocols like oAuth.  We are going to take our cue from the DAM development community about which is the best route to take with this.  We’ve done the groundwork for SimpleDAM, but it is up to the DAM development community to define where it goes next.

## Metadata
There is some very basic core metadata which SimpleDAM uses, but this is likely to be insufficient in many cases.  Attempting to define a standardised DAM metadata protocol which covers every single eventuality is a fool’s errand which many have previously attempted (with fairly limited success).  In addition to inertia and apathy, metadata standards are possibly one of the key reasons why no one has yet been able to define a DAM interoperability standard that has gained traction.  Our solution to this is simple.  We have a metadata node in the JSON data which is returned from getasset operations called ‘extension’.  In this, each development team can include their own metadata packet unique to their DAM.  There is an example SimpleDAM extension to illustrate how this might work and in some of the test assets you will also see extensions for EXIF also.

The disadvantage is that there is no standardisation of the extended metadata which is returned from a given provider and this might mean whatever receives it has to uniquely process the metadata fields on a case-by-case basis.  The advantage is that it is at least handled in a consistent fashion so case-specific metadata is easier to deal with.  A further option would be to use one of the pre-existing metadata standard (e.g. Dublin Core, IPTC etc.) instead.  

Metadata standards are outside the scope of SimpleDAM until/unless the community decides it wants to take on this task (don’t hold your breath).

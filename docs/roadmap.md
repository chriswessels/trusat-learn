---
id: roadmap
title: TruSat Roadmap
sidebar_label: Roadmap
---

This is a list of the features and functionality the community envisions for TruSat. To date, the community has identified three broad lines of work for progressing TruSat from a prototype to a valuable resource for the long-term sustainability of spaceflight:
- Accessibility: Making it easier and more enjoyable for more people to make and submit satellite observations, to grow and diversify TruSat’s global “sensor network.” This encompasses efforts ranging from tutorial materials for satellite tracking to hardware and software development to make data generation more efficient, easier, and fun. 

- Orbit determination: Refining the orbit determination algorithms to enhance the accuracy and usability of orbit predictions.

- Decentralized Trust Architecture: Building and integrating the blockchain infrastructure to enable TruSat to function as a decentralized, autonomous orbit determination system providing transparent, trusted orbit predictions.

This roadmap is dynamic and will evolve based on the Contributor capacity and community feedback.
You can see what the community is working on in TruSat’s GitHub.  Anyone is invited to further specify and build features from this list, or propose new ideas on our Discuss or Github. 
If you have an idea for a new feature or initiative and you’re willing to lead its creation, make a Proposal by creating a new issue in the appropriate TruSat repository on GitHub with [Proposal] in the title. More guidelines for submitting Ideas and Proposals can be found in the TruSat [Charter](https://learn.trusat.org/docs/trusat-charter).

For a list of issues in progress, visit the TruSat [project boards](https://github.com/orgs/TruSat/projects) on Github.

# 1. Accessibility
## Automated image processing and IOD extraction from photos
We believe this is the highest-leverage way to increase the accessibility of satellite tracking, and to increase the volume of observations. 

Much of what is needed to integrate automated IOD extraction from digital camera images
appears to be available in Cees Bassa’s sattools/stvid open-source code):
- Receive image frame from a registered user (known location)
- (Repeat) Plate-solving
- Perform feature detection of image/image series, looking for known/expected objects based on user capability profile
- Optionally, perform further algorithmic exploration of unidentified objects (UNIDs)
- Extract position/time information, or verify the efficacy of user-provided IOD/UK/RDE-formatted position observation
- Cross-Correlate existence of IOD object, with database state vectors (TLE, or more detailed internal format)

A waypoint on the path towards a fully automatated image processing pipeline would be a tool that:
- Allows observers to upload their satellite photos
- Plate-solves with the help of the API at http://nova.astrometry.net/
- Provides a web interface for people to mark the x/y pixel coordinates of a satellite within the photo
- Generates an IOD from the extracted above.

[Here is a UX prototype](https://www.figma.com/proto/LEL9dzD9uC3NRstzF26SF7/TruSat---Image-submission-UX?node-id=63%3A3210&scaling=scale-down) of this feature.

![wireframes for image processing queue](/img/trusat-feature-image_processing_queue.jpg)


Note: The person marking the satellite's x/y coordinates does not need to be the photographer. If the web interface provides a [Zooniverse](https://www.zooniverse.org/projects/zookeeper/galaxy-zoo/)-like queue of photos, this could help separate concerns between astrophotographers dumping photos containing satellites, and citizen scientists volunteering time to identify satellites (like with Zooniverse). 
 
## When and where to look? (Pass prediction)
Currently, observers need to use software outside of TruSat to see exactly when and where to look to see a satellite. An observer should have more guidance from TruSat on this. So much of the user experience could be better catered to individual observers if TruSat could account for your location when presenting information.
- Creates a table of upcoming and potentially visible objects based on a  User’s station location and Heaven’s Above pass prediction data.
 
## TruSat Mobile Capture

[This deck](https://docs.google.com/presentation/d/1JCeppogLCg3CWWcW85AEmiAlnRlNtmkuB3gD5xf85eM/edit#slide=id.g745d18b404_0_64) illustrates some broad design concepts for a TruSat mobile app.
- IOS/Android app for location-based mobile observations
- [Desing wireframe sketches](https://www.figma.com/file/ZhuhQePQlZ3TuTbnlvcZjH/TruSat---Capture-Observations-UX?node-id=6%3A2915)

<img style="max-width: 500px;" src="/img/trusat-GalaxyS10_Mock--cropped--200420-0014b.gif" alt="Design concept mockup">
 
## Direct tasking of motorized, software-enabled consumer telescopes or scriptable robotic observatories
- Integration via INIDIHUB or similar application connects a network of observation stations and the data they produce.

## Activity Dashboard Interface (Release 1.1.0)
[In-progress](https://github.com/orgs/TruSat/projects/2)
- A dashboard interface displays the activity (new/all observations from that user, objects contributed) for users on the TruSat platform.
- A dashboard interface displays the activity (new observations, new users, new objects) occurring across the TruSat platform.

## TruSat API Expansion
- Creates command line queriable API endpoints for object TLEs, categories, and their magnitudes within the TruSat database.
 
## Radio generated TLEs
- Integration with SatNOGS
- Presence tags, verification of frequency
- TLE submission via command-line scripts

## Object Search
- A search box in the TruSat Catalog page that allows a user to query specific objects by their NORAD number or name

# 2. Orbit Determination 

## Roadmap for the trusat-orbit repository code:
 
### Near Term (next few weeks)
[in-progress]
1. [x] Pull out loop-intensive functions into accelerated module
1. [ ] Set up Travis Continuous Integration Testing
1. [ ] Publish pypi trusat (trusat-orbit?) module
1. [ ] Expand documentation for using trusat.tle and trusat.iod modules
1. [ ] Create jupyter notebook for development, experimentation, visualization
1. [ ] Restore functionality of local IOD file processing with satfit. [Issue #8](https://github.com/consensys-space/trusat-orbit/issues/8)
1. [ ] Fix satid/elfind compatibility with python-skyfield
1. [ ] Incorporate XF functionality into TLE processing scripts (See tle_util.py header comments)
1. [ ] Transition python-skyfield dependencies to native python-sgp4 calls
 
### Mid Term (next few months)
1. [ ] Extend satfit functionality in PyQT module
1. [ ] Write verison of TLE Retrieve in PyQT, utilizing trusat.tle_util
1. [ ] Merge trusat-orbit and trusat-backend into a common repo and package
1. [ ] API access to all data (after SeeSat-L user opt-in/opt-out)
1. [ ] Secure compute for SITE data - allow geocentric (ICRS) observation vectors / observer location
 
### Long Term
1. [ ] Transition to modules compatible with OREKit and [UT-Austin orbdetpy](https://github.com/ut-astria/orbdetpy)
1. [ ] Full automation with user rank/trust, object priority and object confidence
1. [ ] Parallelized processing for super-compute applications

# 3. Decentralized Trust Architecture
Read [here](roadmap-decentralization) for more notes on decentralizing TruSat.
 
## Ethereum Mainnet Features
- On-chain transactions for (up to) every observation block, and associated TLE prediction update.
- On-chain stores of value (reputation, incentives, NFTs, etc.).
- State-channel object storage (TLEs, algorithms, meta-data, etc.).

## Database IPFS integration
- Provides a decentralized storage layer for:
- TruSat catalog of TLE’s object images submitted for processing

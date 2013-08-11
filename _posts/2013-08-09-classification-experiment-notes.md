---
layout: post
title: Classification Experiment Notes
tags: [cultural transmission, classification, coarse graining, simulation, ctpy, dissertation, experiments]
category: coarse grained model project
---
### Setup and Raw Simulations ###

**8/9/13** -- _Setup and Simulations_

Completed the code for classification experiments, at least to the point that an analysis script can run through classifications without parallelization and identify `individual_samples` to their classes given each classification in the database.  All of this is tagged "v1.0" in github, and was pulled to an EC2 `m3.xlarge` instance to do the raw simulation output.  

Raw simulations were done by using `neutral-kn-sweep.py`.  This took about 5 hours, costing about 5 dollars (for a total of 8 so far this month), and filled about 13GB given the current configuration of parameter space and sampling interval of 100 generations (for 10K generations after stationarity).  

Am working on expanding and reattaching the EBS volume with the MongoDB database, so I can do the subsampling, which ought to balloon the database by a factor of maybe 10x?  Will finish that tomorrow, delete the old snapshots and volumes, and run the subsampling script overnight, with the goal to be running the classification script while traveling.  Then I can shut everything down and analyze when I get back from the trip.  Might try to move the compressed DB back locally at that point, but will need to do it a the office on a fast connection.  

**8/10/13** -- _Subsampling and Start of Classification Identification_

Cleaned up my instances and resized the EBS volume to have 200GB to work with.  This probably will be enough, but we'll see.  I ran the subsampling program and the raw data collection grew to about 19GB.  I started the classification script, which runs each classification serially, and it's going strong.  I expect it to generate about 42MM individual documents by the time it's done, and that could be a day or two.  

**8/11/13** -- _Second Resizing_

Overnight, the classification script generated about 12MM observations, and about 50GB in database, which means that database is going to overflow the EBS volume and stop.  So I killed the process, nuked the postclassification database, and stopped the instance.  I'm starting a second resize now.  

Snapshot creating is underway.  Next step when I pick it up again is volume creation, swapout on the instance.


java c
ECE5550: Applied Kalman Filtering 
KALMAN FILTER APPLICATIONS 
10.1: Examples of Kalman ﬁlters 
■ To wrap up the course, we look at several of the applications introduced in notes chapter 1, but in more detail.
■ My students and I have been directly involved with these examples.
Tracking marker dots on actors 
■ State: x , y position and velocity of dots in frame.
Observation: x , y positions of dots in frame. (unlabeled).
Issues: Data association, tracking when dots are obscured.
■ Images containing actors with relective marker dots arrive for processing at 30 frames per second.  

■ Dennis’ ﬁrst challenge was detecting targets in a 2D camera ﬁeld in an efﬁcient way.
■ The standard NTSC scan order for when pixels arrive is shown to the right.

■ Dennis created an efﬁcient centroid
calculation algorithm that worked in real time as the pixels arrived (in scan order), and can handle up to a pre-speciﬁed maximum number of simultaneous targets.
■ The following is an example illustrating some of the issues

■ After scanning row 5, there are three centroid candidates; after scanning row 6, two are joined, to leave only two candidates.
■ The next issue was the target dynamic model to use. Dennis tried both NCV and NCA models;
Sensor noise was determined to be on the order of 1/2 pixel;
Σ was selected by evaluating the statistics of accelerations and jerks in a database of typical motion capture scenarios.
■ The next issue was how to associate centroid position measurements to individual target tracks.
Dennis used a maximum-likelihood association method. That is, for every centroid-target pair, he calculated
where x is the centroid measurement, and x is the target’s present state estimate, and Σx is the target’s present covariance estimate.  He then formed a table of likelihood values

He found the table maximum value, and made that association,
and set all entries in that row and column to zero; he repeated until all measurements were accounted for.
Occluded targets (missing measurements) were handled by skipping measurement updates for those target tracks.
■ Dennis found that the NCV model worked best for this application, and the results were outstanding.  

■ Ongoing challenges in multi-target tracking:
Efﬁciency of the data association process in particular, and of multi-target tracking in general.
For example, there are an estimated 80,000,000 objects 1cm
across or larger orbitin代 写ECE5550: Applied Kalman Filtering KALMAN FILTER APPLICATIONSPython
代做程序编程语言g earth (large enough to disable a satellite). We presently track about 18,000 of the largest ones. Orbit
estimation, collision prediction are hot topics, but very difﬁcult too. Furthermore, beyond assessing where an object is, being able to  say what it is doing and what that means are two very important questions to answer.
Localizing bad guys (or, search and rescue) 
■ State: x , y position and velocity
Observation: Direction (angle) from UAV to target.
Issues: Nonlinear relationship between measurements and position; measurements arriving to KF out-of-sequence.

■ Multiple UAVs search a pre-deﬁned
geographic region for targets of interest.
■ Heterogeneous sensors are used: passive radar, camera, IR.
■ All sensors measure only angle to target (not x , y position, nor range to target).
■ For the targets, a modiﬁed NCV model was used

■ Note (1) that the output equation is nonlinear, and (2) that a baseline continuous-time model is used since measurements are not
necessarily aligned with a pre-deﬁned sample rate.
■ SPKF handles nonlinear output equation, but still needed to be very careful with modulo-2π issues in measurements (a gigantic pain).
■ The state equation, evaluated over a non-constant time interval, is

■ Process noise integrated over a non-constant time interval is incorporated as

■ Initializing the target state using a single measurement of arrival angle was an issue

■ We assume a uniform. distribution on R  ~ U (0, r0), where r0  is the sensor range.
■ We model the sensor reading Θ  = Θ  + Θnoise  where Θnoise  is a  Gaussian distribution with zero mean and standard deviation σv known by the sensor.
■ Then, assuming that R and Θnoise  are independent,

■ Without loss of generality, we can assume that the sensor reading  Θ    0, and then rotate the ﬁnal result by the true sensor reading to compensate. For the above assumptions, the ﬁnal answer is:

■ Using similar reasoning, the covariance matrix (for these two states) may be found to be:

■ Furthermore, measurements from cooperating UAVs arrived to the fusion process out-of-sequence due to communication latencies.
■ Developed “out-of-order SPKF” (O3 SPKF) to handle this issue.

■ Related ongoing challenges:
Knowing UAV (self) position in GPS deprived scenarios.
Target modeling with constraints (e.g., railroad problem), and robust estimation for same.





         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com

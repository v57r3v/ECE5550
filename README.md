java c
ECE5550: Applied Kalman Filtering 
SIMULTANEOUS STATE AND PARAMETER ESTIMATION USING KALMAN FILTERS
9.1: Parameters versus states 
■ Until now, we have   assumed that the   state-space   model   of the   system whose state we are estimating is known   and   constant.
■ However, the system   model   may   not be entirely   known:   We   may wish   to adapt   numeric values within the   model to better   match the   model’s   behavior. to the true system’s behavior.
■ Also, certain values within the system may change very   slowly   over      the   lifetime of the system—it would be good to track those   changes.
■ For example, consider a battery cell.   Its   state-of-charge can   traverse   its entire   range within   minutes.   However, its   internal   resistance   might   change as little as 20%   in   a   decade   or   more   of   regular   use.
• The quantities that tend to change quickly   comprise the state of   the system,   and
• The quantities that tend to change slowly   comprise the
time-varying parameters of the system.
■ We know that   Kalman ﬁlters   may be   used to estimate the   state   of   a dynamic system given known parameters and   noisy   measurements.
■ We   may also use   (nonlinear)   Kalman ﬁlters to estimate parameters   given a known state   and   noisy   measurements.
■ In this section of   notes we ﬁrst   consider   how to   estimate   the   parameters of a system   if   its   state   is   known.
■ Next, we consider how to simultaneously estimate both the state   and   parameters of the system using two different approaches.
The generic approach to parameter estimation 
■ We denote the true parameters of a   particular   model   by θ   .
■ We will use   Kalman ﬁltering techniques to estimate the parameters
much like we have estimated the state.   Therefore, we   require a   model   of the dynamics of the   parameters.
■ By assumption, parameters change very slowly, so we   model them   as   constant with some small   perturbation:
θk = θk−1   + rk−1   .
■ The small white   noise   input rk is ﬁctitious, but   models the   slow   drift   in      the parameters of the system plus the inﬁdelity   of the   model   structure.
■ The output equation   required for   Kalman-ﬁlter system identiﬁcation   must be a   measurable function of the system parameters.   We   use
dk = hk (xk, uk,θ   , ek ),
where h(·) is the output equation of   the   system   model   being               identiﬁed, and ek models the sensor   noise and   modeling   error.
■ Note that dk is usually the same   measurement   as zk ,   but we   maintain
a distinction here in case separate outputs   are   used.   Then,
Dk = {d0, d1   , . . . , dk }.   Also,   note   that ek and   vk often   play   the   same role, but are   considered distinct   here.
■ We also slightly   revi代 写ECE5550: Applied Kalman Filtering SIMULTANEOUS STATE AND PARAMETER ESTIMATION USING KALMAN FILTERS
代做程序编程语言se the   mathematical model of system   dynamics
xk = fk−1(xk−1   , uk−1,θ,wk−1)
z k = hk (xk, uk,θ,vk ),
to explicitly include the   parameters θ in the   model.
■ Non-time-varying numeric values   required by the   model   may   be   embedded within f (·) and h(·), and are   not   included   in θ   .
9.2: EKF for parameter estimation 
■ Here, we show how to   use   EKF   for   parameter   estimation.
■ As always, we proceed by deriving the   six   essential steps   of   sequential inference.
EKF step 1a: Parameter   estimate time   update.
■ The parameter prediction step   is approximated   as

■ This makes sense, since the parameters   are assumed constant. EKF step 1b: Error covariance time   update.
■ The covariance prediction step is accomplished by first computing θ˜k−.k— .

■ We then directly compute the desired covariance

■ The time-updated covariance has additional uncertainty due to the   ﬁctitious   noise “driving” the parameter values.
EKF step 1c: Output   estimate.
■ The system output is   estimated to   be
d(^)k = E[h(xk, uk,θ   , ek )   |   Dk —   1]
≈ hk (xk , uk ,   θ(^)k— , e-k ).
■ That is,   it   is assumed that propagatingθ(^)k— and   the   mean   estimation
error is the best approximation to   estimating   the   output.
EKF step 2a: Estimator   gain   matrix.
■ The output prediction error   may then be   approximated

using again a Taylor-series expansion on the ﬁrst   term.

■ From this, we can compute such necessary   quantities   as

■ These terms may be combined to   get the   Kalman gain

■ Note, by the   chain   rule   of   total   differentials,


■ But,

■ The derivative calculations are   recursive in   nature, and   evolve   over   time as the state   evolves.
■ The term dx0/dθ   is   initialized to zero unless side   information gives   a   better estimate of   its value.
■ To calculateC(^)k(θ) for any speciﬁc   model structure, we   require   methods
to calculate all of the above the   partial   derivatives   for   that   model.
EKF step 2b: State estimate measurement   update.
■ The ﬁfth step   is to compute the a posteriori state estimate by
updating the a priori estimate using the estimator gain and   the   output   prediction error dk −   d(^)k 

EKF step 2c: Error covariance measurement   update.
■ Finally, the   updated covariance is   computed   as

■ EKF for parameter estimation   is   summarized   in   a   later table.
Notes: 
■ We   initialize the parameter estimate with our best   information   re. the   parameter   value:   θ(^)0(十)   = E[θ0].
■ We   initialize the parameter estimation error covariance   matrix:

■ We also   initialize dx0   /dθ   = 0   unless side   information is   available.



         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com

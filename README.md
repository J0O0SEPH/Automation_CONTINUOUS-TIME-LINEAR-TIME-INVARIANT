**Automation**

*Laboratory Exercise 2*

**Identification and Discrete-Time Control of A Heating System**

1) Connect the control loop with a real heating system and familiarize yourself
with the monitoring and control software "WCONTROL".

2) Measure the step response of the controlled system when changing the
manipulated variable (input to the controlled system) by 20% (the system is
supposed to be linear). Recommended area of the measurement is from 50% to 70%
of the maximum power. Archive the obtained step response with a suitable period.

3) Approximate the measured step response (by using the least squares method)
and construct a continuous time mathematical model (transfer function) of the
controlled system, specify the parameters including the physical units.

4) Compare the step response of the obtained (identified) model with the
measured characteristic (in one chart).

5) Compute discrete-time transfer function (Z-model) of the system under
assumption of the zero-order hold. Select the sampling period so that the
transient process will be covered by 8-14 samples.

6) Specify the differential equation for calculated discrete-time transfer
function.

7) Perform the calculation of discrete-time step response and compare it with
the continuous-time one.

8) Design a discrete-time PID controller by using Desired Model Method (formerly
known as Inverse Dynamics Method) for control behavior without overshoot (choose
appropriate size of sampling period). Perform the real control experiment.

9) Simulate the control experiment from the previous point in Matlab + Simulink
environment and compare the simulation result with the real measurement.

For points 8 and 9 assume the following general shape of the reference signal
*w*  
(typically *w*2-*w*1=20°C):

1.  From measured data graph, it has been assumed that the heater behavior could
    be described with second order deferential equation. Represented in the
    S-plane with the following equation:

$$
G\left( s \right) = \frac{K}{(T1*S + 1)(T2*S + 1)}
$$

\- getting the step response using inverse laplace transform:

$$
H\left( t \right) = \mathcal{L}^{- 1}\left\lbrack \frac{G\left( s \right)}{S} \right\rbrack = \left\lbrack \frac{K}{S\left( T1*S + 1 \right)\left( T2*S + 1 \right)} \right\rbrack
$$

$$
H\left( t \right) = K*\left\lbrack 1 + \frac{T1}{T2 - T1}{*e}^{\frac{- t}{T1}} + \frac{T2}{T2 - T1}*e^{\frac{- t}{T2}} \right\rbrack
$$

\-Using LSM to get values (K, T1, T2) and plug it in the step response equation
H(t), then compare the results with the acquired data:

| T1 | 100.0554279 |
|----|-------------|
| T2 | 4.488164455 |
| K  | 1.709       |

[CHART]

1.  Z-Model:

Assumptions:

\- Zero Relative shift

\- Zero-order hold.

$$
T\left( \text{Sampling\ time} \right) = \frac{\text{Readings\ count}}{\text{restricted\ numer\ of\ samples}} = \ \frac{100}{8} = 12.5\ seconds
$$

$$
G\left( s \right) = \frac{1.7}{(100S + 1)(4.5S + 1)} = \frac{1.7}{450{*S}^{2} + 104.5*S + 1}
$$

\- Using Z-transform table

$$G\left( z \right) = \frac{0.13*Z + 0.05}{Z^{2} - 0.94*\ Z + 0.05} = \
\frac{Y(z)}{U(z)}$$

1.  Difference Equation:

\- Applying inverse Z-transform:

$$
Y\left( z \right)*\left\lbrack Z^{2} - 0.94*\ Z + 0.05 \right\rbrack = U\left( z \right)*\left\lbrack 0.13\ Z + 0.05 \right\rbrack
$$

$$
\frac{Y\left( z \right)*\left\lbrack Z^{2} - 0.94*\ Z + 0.05 \right\rbrack}{Z^{2}} = \frac{U\left( z \right)*\left\lbrack 0.13\ Z + 0.05 \right\rbrack}{Z^{2}}
$$

$$
Y\left( Z^{- 1} \right)*\left\lbrack 1 - 0.94{*Z}^{- 1} + 0.05*Z^{- 2} \right\rbrack = U\left( Z^{- 1} \right)*\left\lbrack 0.13*Z^{- 1} + 0.05*Z^{- 2} \right\rbrack
$$

$$
Z^{- 1}\left\lbrack Y\left( Z^{- 1} \right)*\left\lbrack 1 - 0.94{*Z}^{- 1} + 0.05*Z^{- 2} \right\rbrack \right\rbrack = Z^{- 1}\left\lbrack U\left( Z^{- 1} \right)*\left\lbrack 0.13*Z^{- 1} + 0.05*Z^{- 2} \right\rbrack \right\rbrack
$$

$$
y\left( k \right) - 0.94*y\left( k - 1 \right) + 0.05*y\left( k - 2 \right) = 0.13*u\left( k - 1 \right) + 0.05*u(k - 2)
$$

$$
\mathbf{y}\left( \mathbf{k} \right)\mathbf{= 0.94*y}\left( \mathbf{k - 1} \right)\mathbf{- 0.05*y}\left( \mathbf{k - 2} \right)\mathbf{+ 0.13*u}\left( \mathbf{k - 1} \right)\mathbf{+ 0.05*u(k - 2)}
$$

1.  Desired Model Method:

$$
G\left( z \right) = r0*\left\lbrack 1 + \frac{T}{\text{TI}}\frac{Z}{Z - 1} + \frac{\text{TD}}{T}\frac{Z - 1}{Z} \right\rbrack
$$

$$
Tw(feedback\ time\ constant) = \ \frac{T}{0.286} = \frac{12.5}{0.286} = 44\ seconds
$$

$$
C1 = e^{\frac{- T}{T1}} = e^{\frac{- 12.5}{100}} = 0.88
$$

$$C2 = \ e^{\frac{- T}{T2}} = e^{\frac{- 12.5}{4.5}} =$$ 0.06

$$
Cw = e^{\frac{- T}{\text{Tw}}} = e^{\frac{- 12.5}{44}} = 0.75
$$

T1= 100

T2= 4.5

K= 1.7

$$
r0\ \left( \text{proportional} \right) = \ \frac{\left( 1 - Cw \right)T1}{\text{KT}} = \ \frac{\left( 1 - 0.75 \right)*100}{1.7*12.5} = \ 1.17
$$

$$
\text{TI\ }\left( \text{integral} \right) = \ \frac{C1 + C2 - 2C1C2}{1 - C1 - C2 + C1C2}*T = \ \frac{0.88 + 0.06 - \left( 2*0.88*0.06 \right)}{1 - 0.88 - 0.06 + \left( 0.88*0.06 \right)}*12.5 = 92.46
$$

$$
\text{TD\ }\left( \text{Derivative} \right) = \ \frac{C1C2}{C1 + C2 - 2C1C2}*T = \ \frac{0.88*0.06}{0.88 + 0.06 - \left( 2*0.88*0.06 \right)}*12.5 = 0.79
$$

$$
q0 = r0\left\lbrack 1 + \frac{T}{T1} + \frac{\text{TD}}{T} \right\rbrack = 1.17*\left\lbrack 1 + \frac{12.5}{100} + \frac{0.79}{12.5} \right\rbrack = 1.39
$$

$$
q1 = \  - r0\left\lbrack 1 + \frac{2TD}{T} \right\rbrack = \  - 1.17*\left\lbrack 1 + \frac{2*0.79}{12.5} \right\rbrack = - 1.31
$$

$$
q2 = r0\left\lbrack \frac{\text{TD}}{T} \right\rbrack = 1.17*\left\lbrack \frac{0.79}{12.5} \right\rbrack = 0.073
$$

$$
\text{Gr}\left( z \right) = \frac{q0 + q1Z^{- 1} + {q2Z}^{- 2}}{1 - Z^{- 1}} = \ \frac{1.39 - 1.31Z^{- 1} + 0.07Z^{- 2}}{1 - Z^{- 1}}
$$

![](media/dcdbdc0314404ee76fd3c3ade5f4b92f.jpg)

\- Using T(Sample Time)= 1 second, results shows;

No overshoot, and good reference tracking.

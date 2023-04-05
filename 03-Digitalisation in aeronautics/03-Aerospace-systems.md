# introduction
[SOUND] Hello, my name is Dirk Zimmer. I'm from the German Aerospace Center or Deutsches Zentrum fur Luft- und Raumfahrt, in short, simply DLR. More precisely, there I'm located at the Institute of System Dynamics and Control at Oberpfaffenhofen, near Munich. Here we engage in a lot of multidisciplinary activities, such as the modeling and simulation and control of robots. The design of Mars rovers, the optimization of electric vehicles. But also there is aviation, and this is going to be today's topic. If you look at a conventional aircraft of today, we find that it is mostly driven by free domains of power. There is the pneumatic power that is taken directly from the engines. And mostly used to drive the environmental control system. There is the hydraulic power, which is mostly used to drive the actuation system for the control surfaces. And there is electric power used for almost everything else. The cabin lighting, the galley ovens, the avionics, you name it.
Play video starting at :1:18 and follow transcript1:18
There's a certain trend, due to the advancement in power electronics, to go towards a more electric aircraft. So to reduce or get rid completely of the pneumatic power. And to use the hydraulic power and make more electric power. The Boeing 787 is such an example, but is this really a better aircraft?
Play video starting at :1:41 and follow transcript1:41
It's difficult to tell, because there is also the Airbus A350 XWB. And this is still a quite conventional aircraft, but it is comparative. So in order to really say how you should build a future aircraft, we have to look at all the systems in total. So the electrical system, the climate and cooling system, the actuations. Also the engines, the landing gear, and many other systems. And we have to create one common methodology to model and simulate these systems. And bring them together for a flight performance evaluation that tells us how to design the system optimally.
Play video starting at :2:23 and follow transcript2:23
Well, I want to give you a short glance at what we do. And our modeling and simulation activities regarding these highlighted areas.
Play video starting at :2:32 and follow transcript2:32
So for instance, there is an electric system. Here is an example of a classic single-aisle aircraft with two engines. And each engine has two generators, and there is the APU. You see there is an AC bus bar and a DC bus bar for the essential avionics. We can use such models to, for instance, model a failure case. So when the engine is failing, the two generators will fail, and the corresponding bus bars need to reconfigure.
Play video starting at :3:7 and follow transcript3:07
This here is an example model of something that is on board of almost every aircraft since about 70 years. This is an air cycle, when you're flying a plane you like to have a good climate around you. You prefer probably to have 21 degrees of Celsius. The point is the air that you breathe is the one that is taken from the engines. And that enters the fuselage with roughly 250 degrees of Celsius and 2.5 bars. A little too hot for you as a human being. So it needs to be cooled, and for this outside air is being used. This is our device called the rammer channel that's typically situated beneath the wings. Then the hot air from the engine is coming in, it's going through the heat exchangers, a compressor, heat exchanger again. Odor is being extracted and finally it can be brought to the mixing unit and later on to the cabin. Such a model can be integrated into an overall aircraft model. Where we model the complete cabin air recirculation and also other aspects.
Play video starting at :4:21 and follow transcript4:21
This year, our components used for the modeling of electric mechanical actuators. There are motors, electrical motors, inverters, gear models, ball screw elements. All what you need to model an electric mechanical actuator. We'll come back to that in a few minutes. These models can also be validated using for instance a test rig here.
Play video starting at :4:50 and follow transcript4:50
Last but not least, and we shall not forget that all these systems need to be integrated into a flight performance simulation. Here you see an aircraft flying over Munich. The blue surfaces represent the loads on the wings and on the fuselage. And there are two aileron surfaces modeled as well. [SOUND]

# Modeling of Aerospace Systems
[MUSIC] Instead of studying the dry theory and history behind this language. I think it is best learned by jumping right into practice and look in a example, and since we are from aviation, let us look at a fitting example of a hydraulic driven activation surface.
Play video starting at ::24 and follow transcript0:24
This here would be the corresponding modeling diagram and the program that you're seeing is one of the tools for model a car that is available. Since it is a standard, it doesn't really matter that much what tool you use, this diagram will look more or less the same in all of them. Let us go from modeling to simulation and there we can simulate the system for 10 seconds and look at the result. So you see here the activation control surface moving around the hinge line here. Green arrow represents the aerodynamic force, so I'll show once more.
Play video starting at :1:9 and follow transcript1:09
Acting on it.
Play video starting at :1:12 and follow transcript1:12
We can also look at the plots to see the quality of this control. So the blue line represents the control signal and the red line is the actual motion of the system. And you see it follows the control motion quite well.
Play video starting at :1:32 and follow transcript1:32
Also, we can look a detail and mechanics. So this is the hinge line then there are three revolute joints and this red element here represents translational piston causing the actual motion by extending and retracting.
Play video starting at :1:51 and follow transcript1:51
And you see here, this is a kinematic loop and we do find the same loop in this modeling diagram. So this is the hinge line here, this is the revolute joint.
Play video starting at :2:4 and follow transcript2:04
The activation control surface mounted to it, is represented here by the masses. Mostly we care about the inertia and visualized by this box. This here is the prismatic joint extending and retracting causing the actual motion of the system. The aerodynamic force is modeled very simply. Yeah, you could say simplistically, by taking the angle of the control surface. Doing a very simple computation with a few parameters, like ratios for lift and drag and getting the force out of it.
Play video starting at :2:43 and follow transcript2:43
Furthermore, this prismatic joint is driven by an hydraulic piston.
Play video starting at :2:50 and follow transcript2:50
There is a hydraulic fluid coming in and going out. If you look at the model itself, we find a simple hydraulic construction. First of all, there's a double piston element that we can move upwards or downwards. And then there is this construction, where I can switch the piston either upwards or downwards, causing the fluid to flow either and one of these directions. In between the valve is a little bit leaky, so that the fluid flow is damped and in case of a malfunction the piston wouldn't jam. It would still be able to move and give way to the aerodynamic forces. If you look at this element itself, we do find that there are a few basic equations actually modeling it. So there is simply the law that pressure times area equals force. And there is the corresponding law for this energy transformation that the translational motion times the area is the volume flow of the hydraulic fluid.
Play video starting at :4:2 and follow transcript4:02
That is very simple and so does every component has ultimately in the end a few equations. And if you collect the complete system together and we check it, then you see that this complete system has 1355 equations. That seems like quite a lot but please keep in mind, many of these equations are quite trivial and are optimized away, once you generate simulation code out of it. The thing that I haven't mentioned so far, is the controller here. So, the control signal coming from the aircraft is simply assumed to be a timetable. And then I have a simple PID controller trying to get the measured angle in alignment with the set point by opening and closing the hydraulic valve.
Play video starting at :4:56 and follow transcript4:56
I can see for instance, the impact of the pressure level, for instance, if I lower it a little bit.
Play video starting at :5:2 and follow transcript5:02
And simulate again, I will see that with less pressure, I have less control over T and the quality of my result is worsening. So since I talked about the electrification of aircraft systems before, let us do this here in this model and replace the hydraulic actuator with an electromechanical actuator. So, first I have to make place for this electromechanical actuator by deleting the hydraulic parts. Well, then I need two components for the electromechanical actuator, which in this case can be found in the standard library. Fortunately many volunteers and smarter people did us a favor and created huge model like a standard library, that contains various domains. And you see there's also an electrical domain and within this, we have machines and within this, I for instance find this simple DC permanent magnet machine. Whether it's suited or not, I'll just take it here because it is simple to control.
Play video starting at :6:25 and follow transcript6:25
Well, I now need to bring the rotational motion of this motor, to transform this into the translational motion that is needed by the piston. So I'll need years for that again. Again, I can look at my libraries, and for instance find here, there's a rotational part in the mechanical libraries.
Play video starting at :6:51 and follow transcript6:51
There's an inertia. Well, I should probably model that because my motor is going to run at high speed, so it will matter.
Play video starting at :7:1 and follow transcript7:01
Then there's a gear, I should move it the other way around, so that I go from high-speed motion at the motor side to a lower speed motion at the load side. And then, I'll need an element to translate the rotational velocity into translational velocity and this would be the corresponding part.
Play video starting at :7:35 and follow transcript7:35
Again, I have to enter a parameter, let us say it takes 200 radians to do a meter.
Play video starting at :7:47 and follow transcript7:47
So, now I have done the mechanical part, I still have to complete the electrical part. So my motor needs power and hence I'm looking for a power source. I find that under the Sources, there's a SignalVoltage. That's just what I need because I also want to control the voltage so that I can control the speed.
Play video starting at :8:16 and follow transcript8:16
Also, I should ground the complete circuit.
Play video starting at :8:23 and follow transcript8:23
Which I can do like this.
Play video starting at :8:27 and follow transcript8:27
And then, I need to adapt my controller. Well, that would actually be quite a job. But I replace the control design here with educated guessing and simply adapted parameters a little bit. So, first of all, I need to allow a higher output, so maybe, I work with 270 volts plus or minus. And hence, I also should increase the gain by a similar factor, let's put a 1000 in here. Then I need to specify also the parameters of my motor.
Play video starting at :9:10 and follow transcript9:10
Well, let us assume I have plus/minus 270 volts, 50 volts in total. 1000 rads per second, 20 arms, that's a bit of a lot, but who cares?
Play video starting at :9:29 and follow transcript9:29
All right, let's see if that works.
Play video starting at :9:38 and follow transcript9:38
And indeed, it does, but you can see we do have now a few problems. The inertia of the motor and the concept of the control is causing now and over swinging behavior. Where we had the lagging behavior in front of the hydraulic element
Play video starting at :10: and follow transcript10:00
with an electromechanical actuator, I really need to care about the inertia of the system.
Play video starting at :10:8 and follow transcript10:08
So, that would for instance then, be the job of a control engineer to device a better control scheme for this motor than the one that I've presented here. Maybe I can play around a little bit.
Play video starting at :10:24 and follow transcript10:24
Reduce, let's see if it does have a little impact.
Play video starting at :10:31 and follow transcript10:31
Maybe I'm making things worse.
Play video starting at :10:37 and follow transcript10:37
I improved it a little bit, but sure, there's a lot of work to do. And this is for instance, what you can need such models for.

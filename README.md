<img width="1602" height="1295" alt="image" src="https://github.com/user-attachments/assets/d6b234ac-b982-4dbd-972c-df54520e969a" />


SOLAR PROGRAM
 
Created by: Matthew Taraschke - 2026
“I’m a massive fan of NASA and the 1979 arcade classic Lunar Lander.”

# PLAY NOW!
https://behelit2.github.io/Solar-Program/



QUICK START - ONE FILE
===

Solar Program is a complete persistant simulation in a single `index.html` file. There is
nothing to install or build, and there are no packages or separate audio files.

With Python 3 installed, open a terminal in the directory containing
`index.html` and run:

```bash
python -m http.server 8000
```

Then open:

http://localhost:8000/

That is the entire local launch process. Python only serves the file; the game,
styles, programmatic artwork, Instruction Manual, and audio are contained in
the HTML.

On Windows, if `python` is not available as a command, use:

```powershell
py -m http.server 8000
```


===
WHAT IS IT?

The most accurate description is:

A persistent 2D n-body spaceflight and rocket-construction sandbox that is the spiritual successor to Lunar Lander (1979).

More specifically, it combines several genres:

# Orbital-mechanics sandbox

* It scientifically models the entire solar system from a top down perspective along the plane of the ecliptic. It has NASA grade gravitational reference bodies, osculating orbits, maneuver nodes, high time warp, Lambert-seeded transfers, and n-body correction… all true to real life scale.

# Spaceflight simulation

* Orbital velocity, escape velocity, thrust, staging, drag, heating, landing, docking, and transfer planning all matter.


# Engineering/construction sandbox

* Players assemble rockets from command modules, engines, tanks, aerodynamic surfaces, decouplers, docking ports, power systems, antennas, recovery equipment, and utility hardware (42 parts total).

# Persistent mission-management game

* Vessels, debris, astronauts, flags, docking assemblies, resources, maneuvers, and celestial states are persisted.

# Educational “serious game”

* It demonstrates real concepts such as thrust-to-weight ratio, delta-v, specific impulse, dynamic pressure, periapsis, apoapsis, line-of-sight communications, eclipse power management, and atmospheric entry.

===
ABOUT THE SIMULATION ENGINE

Solar Program represents a bespoke, self contained, scientific grade simulator and game engine that is written entirely in vanilla html, css, and javascript. As such, it’s able to do everything using a single CPU core and is not heavily dependent on the GPU for rendering. Nearly everything is procedurally drawn using vector canvas elements, a hypercharged descendant of how graphics were generated in the original Lunar Lander.

Very large rocket designs will start to push the envelope of what one CPU can do. After about 400~500 parts or so, the simulation will start slowing down due to the more complex physics frames. This is usually only an issue at launch, as separating from heavy stages will cause the simulation speed to recover. The absolute limit is 2,500 parts for one rocket, though it may be possible to exceed that limit by docking two enormous rockets.

I did my best to get everything working perfectly on iPhone and Android, but the learning curve for building and using rockets is definitely steeper than desktop browsers. Users should use a desktop/laptop browser to learn how to play initially, then everything on the mobile interface will make more sense. It can also be useful to build rockets on a desktop/laptop and export the design to your phone.

===
Below is a full accounting of everything Solar Program accurately simulates.

===
CELESTIAL MECHANICS AND ORBITAL SCIENCE

Consistent physical foundations
Gravity, propulsion, radiation, and orbital calculations use established physical constants and a consistent internal unit system. Simulation time connects elapsed seconds, Julian dates, calendar displays, and time-warp multipliers.

Newtonian gravitational interaction
Designated gravity-source bodies attract one another through paired inverse-square gravitational forces. Symmetric force updates reflect Newton’s third law and support system momentum conservation.

A moving solar-system barycenter
The Sun participates in the simulation rather than remaining fixed at the origin. Mass-weighted initial positions and velocities establish a barycentric frame, allowing Jupiter and other massive bodies to influence the Sun’s motion.

Keplerian orbital initialization
Elliptical orbits are constructed from semimajor axis, eccentricity, mean anomaly, and longitude of periapsis. A numerical Kepler solver establishes initial orbital states, with support for prograde and retrograde motion in the simulation plane.

Hierarchical planet-and-moon motion
Moons inherit their parent planet’s velocity, creating coherent moving planetary systems from the start.

Second-order orbital integration
Celestial bodies use kick–drift–kick integration, a velocity-Verlet/leapfrog-style method well suited to orbital motion and long-term dynamical behavior.

Efficient test-particle dynamics
Selected low-mass objects respond to gravitational sources through a test-particle model, supporting extensive populations of small celestial bodies.

Comprehensive orbital analysis
Instantaneous position and velocity provide specific orbital energy, angular momentum, eccentricity, semimajor axis, periapsis, apoapsis, bound-orbit period, circular speed, escape speed, and radial and tangential velocity.

Rotating worlds
Surface motion follows rigid-body rotation in the equatorial plane. Prograde and retrograde rotation carry landed spacecraft, facilities, astronauts, flags, and settled debris around their worlds.

Rotational launch assistance
Launching spacecraft inherit local surface velocity, connecting planetary rotation directly to ascent and orbital insertion.

Physical diagnostics
Source-system diagnostics track kinetic energy, pairwise gravitational potential energy, and planar angular momentum.

===
A LIVING SOLAR SYSTEM

Recognizable astronomical scale
Planetary order, orbital distances, mass relationships, rotation periods, and orbital eccentricities draw on real solar-system characteristics.

Direct gravitational perturbations
Massive planets and selected moons, dwarf planets, and asteroids interact dynamically within a flattened n-body system.

Extensive celestial populations
Major planets, moon systems, dwarf planets, named asteroids, comets, and generated belt populations create a broad exploration environment.

Distinctive celestial presentation
Irregular asteroid shapes, Sun-opposed comet tails, planetary rings, atmospheric glows, and rotation details give different worlds clear visual identities.

Context-aware reference bodies
Local gravitational influence, proximity, and selection stability guide the reference body used for flight information and orbital analysis.

Analytical high-warp coasting
Eligible spacecraft follow analytical two-body trajectories during high-speed orbital coasting, supporting time acceleration up to 5,000,000×.

===
SPACECRAFT PHYSICS AND PROPULSION

Force-based flight
Spacecraft acceleration combines gravity with thrust, aerodynamic forces, lift, and RCS translation using the vehicle’s current mass.

Torque-based rotation
Engine gimbals, aerodynamics, reaction wheels, and RCS contribute physical torque. Angular acceleration follows torque divided by moment of inertia.

Part-based mass properties
Every part contributes dry mass and resource mass. Center of mass and rotational inertia update as propellant is consumed or the spacecraft configuration changes.

Geometry-aware inertia
Vehicle inertia combines rectangular-part inertia with the parallel-axis theorem, connecting component placement to handling characteristics.

Physically grounded propellant consumption
Engine mass flow follows:

mass flow = thrust / (specific impulse × standard gravity)

Thrust, efficiency, and fuel consumption therefore remain directly connected.

Changing acceleration during burns
Engines consume actual tank resources. As vehicle mass decreases, the same thrust produces greater acceleration.

Rocket-equation performance estimates
Vehicle and staged delta-v estimates use the Tsiolkovsky rocket equation:

delta-v = specific impulse × standard gravity × ln(initial mass / final mass)

Pressure-dependent engine performance
Liquid-engine specific impulse transitions between sea-level and vacuum values, with corresponding thrust changes.

Distinct propulsion behavior
Liquid engines support throttling and available gimbal control. Solid boosters provide sustained full-power operation after ignition until their propellant is exhausted.

Geometry-aware engine gimbaling
Gimbal control calculates torque around the vehicle center of mass and accounts for engine lever arms and the relationship between gimbal direction and rotational response.

Coordinated attitude actuators
Engine gimbals address requested torque first, while reaction wheels and RCS respond to the remaining demand.

Delivered delta-v tracking
Automated maneuvers operate active engines, consume accessible propellant, and accumulate delivered delta-v from directional thrust and changing vehicle mass.

===
LAUNCH, GUIDANCE, AND FLIGHT OPERATIONS

Thrust-driven liftoff
Rockets begin on a rotating launch site and release when fueled thrust provides sufficient outward acceleration to overcome local gravity.

Authentic orbital fundamentals
Successful ascent requires building horizontal velocity. Closed orbits, orbital insertion, escape trajectories, and interplanetary flight emerge from the underlying flight mechanics.

Multi-stage spacecraft
Engines, decouplers, separators, parachutes, solar panels, and antennas can be assigned to activation stages. Separated components continue as independent craft or debris.

SAS attitude modes
Hold, prograde, retrograde, radial-in, radial-out, target, and anti-target modes translate desired orientation into angular-rate targets and physical torque requests.

Powered reaction wheels
Reaction wheels provide electrically powered attitude control, with modeled torque availability and energy demand.

Propellant-driven RCS
RCS supports planar rotation and body-relative translation for precision maneuvers, rendezvous, and docking.

Automated maneuver execution
The spacecraft aligns for a burn, returns to real-time simulation, operates its engines, and ends the maneuver when the target delivered delta-v is reached. Execution also responds to thrust and propellant availability.

Extensive flight telemetry
Instruments report altitude, radar altitude, surface-relative speed, vertical and horizontal velocity, Mach number, dynamic pressure, acceleration, g-load, thrust, local thrust-to-weight ratio, orbital elements, estimated remaining delta-v, target range, and relative speed.

===
ATMOSPHERES, AERODYNAMICS, AND THERMAL SYSTEMS

World-specific atmospheres
Atmospheric properties distinguish dense Venusian conditions, thin Martian air, cold Titan, Earth’s familiar environment, and the deep atmospheres of giant planets.

Altitude-dependent pressure and density
Scale-height models create exponentially thinning atmospheres, with additional temperature layering for Earth.

Rotating atmospheric frames
Atmospheres rotate with their worlds. Aerodynamic calculations use velocity relative to the surrounding air.

Dynamic pressure and drag
Aerodynamic forces use the established relationships:

dynamic pressure = 0.5 × atmospheric density × air-relative speed²
drag force = dynamic pressure × drag coefficient × effective area

Orientation-sensitive aerodynamics
Effective drag area changes with spacecraft attitude. A transonic drag-rise model adds characteristic behavior around Mach 1.

Temperature-dependent sound speed
Local sound speed follows ideal-gas relationships using temperature, molar mass, and heat-capacity ratio. Mach number follows from air-relative velocity.

Fin stability and control
Fins provide restoring torque, controllable surfaces add steering authority, and aerodynamic damping shapes rotational behavior.

Entry heating
Convective heating follows a Sutton–Graves-style relationship involving atmospheric density, nose radius, and velocity cubed. Leading surfaces, sheltered components, and shield orientation influence heat distribution.

Heat shields and ablation
Properly oriented shields reduce heat transferred to the vehicle and consume ablator during atmospheric entry.

Thermal exchange
Parts exchange heat through conduction and radiation. Radiative cooling includes the Stefan–Boltzmann relationship:

radiated power = emissivity × Stefan–Boltzmann constant × area
× (temperature⁴ − environment temperature⁴)

Managed parachute deployment
Parachutes can be armed for automatic deployment when atmospheric conditions become suitable. Reefing manages canopy opening according to dynamic pressure and acceleration loads.

Deployment-aware hardware
Solar-panel and antenna deployment responds to dynamic-pressure conditions.

Gas-giant exploration
Descents into giant planets encounter progressively demanding pressure and thermal environments.

===
TERRAIN, LANDING, AND SURFACE EXPLORATION

Deterministic planetary terrain
Solid worlds feature repeatable terrain profiles with slopes, roughness, and flatter landing areas. Earth includes distinct land and ocean regions.

Shared visual and physical surfaces
Terrain rendering, local surface normals, radar information, and contact detection use a common procedural surface representation.

Part-aware landing contact
Contact calculations evaluate individual part geometry and deployed landing legs against the local surface.

Detailed touchdown assessment
Landing behavior considers surface-relative velocity, slope, vehicle tilt, support geometry, landing legs, and impact speed.

Landing-leg support
Deployed legs widen the support footprint and improve landing tolerance.

Splashdown recovery
Earth’s oceans provide dedicated capsule splashdown behavior and water effects.

Small-body landings
Specialized reference selection, approach stepping, local gravity handling, and swept-contact detection support landings on small moons, asteroids, and comets.

Swept collision detection
Small-body contact checks examine the spacecraft’s path through each substep and refine the earliest surface crossing.

Dynamic impact debris
Major impacts can separate spacecraft into individual components carrying inherited translational and rotational motion.

Active debris environments
Debris responds to gravity, atmospheric drag, surface contact, friction, bouncing, and debris-to-debris collisions.

Persistent surface attachment
Settled spacecraft, astronauts, flags, and debris retain body-relative positions and follow planetary rotation.

===
ELECTRICAL POWER AND COMMUNICATIONS

Distance-dependent solar generation
Solar output follows inverse-square distance scaling relative to the Sun.

Geometric eclipses
Line-of-sight checks between spacecraft and the Sun determine full-light and full-shadow conditions in the two-dimensional environment.

Fixed and tracking solar arrays
Panel types provide distinct orientation-dependent generation behavior.

Balanced electrical accounting
Generation and demand are evaluated together. Surplus charges batteries, while stored energy supplies remaining demand.

Integrated electrical loads
Probe systems, antennas, and attitude-control equipment draw from available electrical resources.

Connected probe operations
Uncrewed control integrates electrical power, antenna operation, line of sight, and a valid communication route to Earth.

Relay networks
Relay-capable spacecraft extend network reach through graph-based routing and antenna-range compatibility.

Planetary signal occultation
Celestial bodies block radio paths, and ground connections respect the local horizon.

Rotating ground infrastructure
The Earth ground endpoint rotates with the planet, making communication geometry change over time.

Light-travel-time reporting
Communication delay is calculated from path distance divided by the speed of light, with delays summed across relay hops.

Local crew command
Crewed spacecraft retain onboard command capability.

===
CONSTRUCTION, RESOURCES, AND STAGING

A full Vehicle Assembly Building
Construct spacecraft from parts with physical dimensions, attachment nodes, orientation, dry mass, resources, and stage assignments.

Powerful editing tools
Undo and redo, blueprints, section copying, mirrored copies, graph validation, and support for up to 1,000 parts enable ambitious designs.

Engineering summaries
Design feedback includes wet and dry mass, propellant mass, thrust, thrust-to-weight ratio, specific impulse, electrical capacity, antenna range, center of mass, center of pressure, and staged delta-v.

Stage-aware fuel access
Engines draw from tanks according to fuel-stage assignments and valid resource connections.

Directional fuel ducts
Fuel ducts provide explicit source-to-destination routing for compatible resources.

Crossfeed-aware structures
Structural crossfeed settings shape ordinary fuel access, while directed ducts enable deliberate routing around barriers.

Mixture-aware resource consumption
Engines consume resources according to mixture requirements, with available supply determining delivered operation.

Resource-preserving separation
Resources stay attached to their physical parts during staging and separation, supported by conservation checks.

Validated fuel transfers
Manual transfers require compatible resources and valid routing. Transaction checks protect resource accounting.

Safe structural copying
Copied sections receive remapped internal attachments and fuel connections, with validation before integration into a vehicle.

Built-in Pioneer I trainer
A ready-made multi-stage orbital vehicle provides an accessible starting point for launch, staging, orbit, and recovery.

===
DOCKING, CREW, AND MISSION CONTINUITY

Precision docking requirements
Docking evaluates port compatibility, separation distance, relative speed, and angular alignment.

Unified docked assemblies
Connected spacecraft form a shared assembly with graph-based resource access and crew transfer.

Mass-weighted docking velocity
Docking combines translational motion using mass-weighted velocity accounting.

Validated undocking
The docking connection is identified and checked before separation, preserving each component’s parts, resources, crew, and staging state.

Balanced separation impulses
Separating components receive equal-and-opposite impulses scaled to their masses.

Capacity-aware crew management
Crew transfers verify cabin capacity and maintain unique astronaut assignments through validated transactions.

Surface EVA
Landed astronauts can leave their spacecraft, walk across local terrain, plant persistent flags, and board nearby cabins.

Earth recovery
Recovery completes a spacecraft’s return and records its crew as recovered.

===
MANEUVER PLANNING AND TIME WARP

Planar maneuver nodes
Plan burns using prograde, retrograde, radial-in, and radial-out delta-v components.

Worker-based trajectory prediction
Selected-source n-body propagation supports updated maneuver placement and trajectory previews.

Advanced transfer planning
Transfer calculations combine Lambert-solution seeds, departure-window sampling, selected-body numerical propagation, finite-duration thrust modeling, and numerical departure corrections.

Capture and correction planning
Transfer workflows can include capture maneuvers and post-departure correction nodes.

Context-sensitive warp protection
Burns, EVA, docking, nearby terrain, periapsis conditions, maneuver timing, and small-body approaches guide time-warp reductions.

High-speed mission progression
Analytical orbital coasting makes long-duration missions practical while preserving the connection between orbital state and elapsed simulation time.

===
PERSISTENCE, PRESENTATION, AND INTERACTION

Extensive save-state coverage
Saves preserve celestial states, spacecraft, parts, resources, temperatures, crew, flags, debris, maneuvers, blueprints, settings, transfer plans, and camera state.

Validated imports
Save imports include validation and rollback handling to protect mission continuity.

Automatic saving
Autosave and page-hide saving help preserve progress.

Physics-independent visibility controls
Display settings determine which objects are drawn while their underlying simulation continues.

Strict visual-scale mode
An optional shared world-to-screen scale represents celestial radii and distances consistently.

Mission-aware camera behavior
Following a vehicle breakup, the camera can track the central debris cloud to maintain visual continuity.

Responsive desktop and mobile controls
Touch flight controls, pinch and drag interaction, assembly drawers, coordinated panels, and safe-area handling support a wide range of screens.

Integrated audio architecture
Audio support includes looping music, separate music and effects levels, thrust-responsive engine loops, camera-distance attenuation, explosion effects, and mobile audio unlocking.

Consistent operational rules
Stage 0 activates first, armed parachutes deploy automatically when conditions permit, flags remain body-fixed, and debris follows a defined one-simulated-day lifecycle.

===
FROM LUNAR LANDER TO A SOLAR SYSTEM OF POSSIBILITIES


“Solar Program celebrates the precision, discovery, and engineering ambition that make spaceflight compelling. If you made it this far, you should hit me up on Facebook and tell me what you think of this application.” - Matthew Taraschke

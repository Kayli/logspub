# notes on aerodynamics and related topics [1]

## basics

- aerodynamics
  - branch of dynamics
  - deals with the motion of air and the way that it interacts with objects in motion
    - such as an aircraft

- flight envelope (also service envelope, or performance envelope)
  - applied to an aircraft or spacecraft
  - refers to the capabilities of a design in terms of 
    - airspeed
    - altitude (sometimes unpacked as load factor or atmospheric density)
  - pushing the envelope
    - when aircraft being taken to or beyond its designated altitude and speed limits
    - for instance by diving it at high speeds, it is said to be flown "outside the envelope"
      - something considered rather dangerous
  - may refer more generally to the predictable behavior of a given phenomenon or situation, and hence, its "flight envelope"

- stall speed
  - fixed-wing aircraft have a minimum speed at which they can maintain level flight

- top speed
  - power needed varies almost linearly with altitude
  - but nature of drag means that it varies with the square of speed

- service ceiling
  - maximum altitude
  - additional speed will not result in increased altitude
  - zero rate of climb
    - is caused by the lift of the aircraft getting smaller at higher altitudes, until it no longer exceeds gravity
    - caused by lower atmospheric density at higher altitudes

- wing
  - tip
  - root: place where wing attached to fuselage
  - span: distance between both wing tips
  - wing area
    - area of shape of the wings, when viewed from above looking down onto the wings
    - includes area of the fuselage between the wings
  - taper ratio: the ratio of the root and tip chord lengths of a wing
  - sweep angle: angle that the quarter chord line makes with the lateral axis of the aeroplane [3]
  - winglets
    - vertically angled tips of the wing
    - reduces vortices at the tips
  - other: aspect ratio, rigging angle, dihedral/anhedral

- stalling
  - happens when friction becomes a dominant force while we keep increasing angle of attack
  - due to increase in drag components
    - form drag at the bottom plane of the wing
    - flow separation that increases pressure at the top of the wing

- stall speed
  - minimum speed at which an airplane must fly to produce lift
  - if an airplane flies slowly, it will require a greater angle of attack to produce lift
    - eventually, the required angle of attack will be so excessive that the airplane won’t generate lift
  - dropping landing gear makes stalling speed go up

- skin of an aircraft
  - is the outer surface which covers much of its wings and fuselage
  - most commonly used materials are aluminum and aluminium alloys

- contamination
  - anything that disturbs airflow around flight surfaces by modifying shape or texture of the skin
  - types
    - foreign object debris (fod): bolts, bird strike, oil, dirt, etc
    - bad weather
      - frost: on the surface of the aircraft, water vapor in the air
      - rime ice: forms on the leading edge of flight surfaces, fast freeze
      - clear ice: same as rime, but slower freeze


## controls

- main flight control surfaces
  - ailerons (рули крена, элероны): roll
  - elevators (руль высоты́): pitch, horizontal axis
  - rudder (руль направления): yaw, vertical axis

- yoke (control wheel or a control column)
  - is a device used for piloting some fixed-wing aircraft
  - pilot uses the yoke to control the attitude of the plane, usually in both pitch and roll
    - rotating the control wheel controls the ailerons and the roll axis
    - fore and aft movement of the control column controls the elevator and the pitch axis
      - when the yoke is pulled back, the nose of the aircraft rises
      - when the yoke is pushed forward, the nose is lowered

- flaps: increase coefficient of lift, which allows us to fly at slower speed


## drag

- aerodynamic force that opposes an aircraft's motion through the air
- force that opposes our direction of travel
- types
  - induced drag: happens when lift is generated, by wing tip vortices
  - parasite drag
    - form drag: arises because of the shape of the object
      - interference drag: caused by the mixing of airflow streams
        - this mixing can cause eddy currents, turbulence, or restrict smooth airflow.
    - skin friction drag

- minimum drag speed: speed at which minimum drag is experienced

- efficiency of flight [4]
  - objective: to stay airborne as long as possible
    - we want to minimise the energy consumption per unit of time
  - objective: to fly as far as possible
    - we want to minimise the energy consumption per unit of distance traveled
    - is found when the thrust and thus drag is lowest


## lift

- wing types
  - symmetric wings don't produce any lift at 0° AOA whereas cambered wings do

- more lift is created at wing's roots than at the tips
  - as there are stronger vortices of air that change direction of a lift vector [2]

- lift equation: L = ρ * v^2 / 2 * S * Cl = q * S * Cl
  - L: lift force, opposes weight of an aircraft
  - ρ: density of the air at all points of the packet (rho)
  - v: air flow speed
  - q: dynamic pressure
  - S: planform
    - shape of the wing, when viewed from above looking down onto the wing
    - is also called planform/projected wing area
    - often simply a square
    - extending flaps will increase planform area
  - Cl: lift coefficient at the desired angle of attack, mach number and reynolds number (turbulence)

- aerofoil: streamlined body that is capable of generating significantly more lift than drag
  - leading edge
  - trailing edge
  - chord: straight line between leading and trailing edge
  - relative airflow velocity: vector describing direction of airflow before reaching an aerofoil
  - angle of attack: angle between chord and relative velocity (flight path)
  - mean camber line (or mean line)
    - is the locus of points midway between the upper and lower surfaces
    - extending flaps will change mean line
  - resultant force: is a sum of all forces acting on a wing from a center of pressure point
    - lift and drag can be interpreted as 2 components of the resultant force


## airflow

- types of airflow
  - streamline/laminar
  - turbulent
  - vortex

- mass flow
  - mass of a substance which passes per unit of time
  - unit: kg/sec

- streamlines
  - used to indicate flow of air in one direction
  - don't split
  - never cross each other
  - closer streamlines indicate higher speed


## bernoulli's principle

- total pressure is composed of static and dynamic pressure
- increase in the speed of a fluid occurs simultaneously with a decrease in static pressure (the fluid's potential energy)

- applicable only for incompressible fluids (works at lower mach number)

- formula: v^2/2 + g * z + p / rho = constant
  - v: fluid flow speed
  - g: acceleration due to gravity
  - z: elevation of the point above the reference plane
  - p: pressure at the chosen point
  - rho: density of the fluid at all points

- dynamic pressure: q = rho * v^2 / 2


## international standard atmosphere (isa, i.s.a)

- used to standardise assumptions and simplify calculations
  
- temperature at sea level = 15C

- pressure at sea level = 101 325 Pa
  - 1.01325 bars, 760 mm Hg (ртутного столба), 14.696 psi (pound / inch^2)

- density at sea level = 1.225 kg/m^3

- temperature lapse rate = 9.8C/km
  - measures how temperature reduces as we gaining in altitude
  - valid until we reach a tropopause (12km above the surface)

- temperature above tropopause = -56.5C


## relevant physics, air properties

- hierarchy of measures
  - density ∝ pressure        (highest influence)
  - density ∝ 1 / temperature
  - density ∝ 1 / humidity    (lowest influence)

- symbol 'proportional to': ∝

- temperature
  - measurement of kinetic energy of molecules
  - unit of measure: kelvin
    - it is a base unit
  - celsius: -273C = 0K
  - farenheit: C * 1.8 + 32
  - as altitude increases, temperature decreases
    - until it reaches a tropopause
      - entry point from troposphere to stratosphere (12km above the surface)

- density
  - mass of all the molecules per unit volume
  - unit: ρ (rho) = kg/m^3
  - as altitude increases, density decreases
    - because earth atmosphere is denser closer to earth
  - when temperature increases, density decreases in an elastic volume
  - density reduces as humidity increases

- pressure
  - force imparted by molecules per unit area
  - units: p = N / m^2 = Pa (pascal)
    - psi: pounds per square inch
    - Hg: inches of mercury
    - mb: millibars
    - atm: atmospheres
  - p = F/A
    - p: pressure
    - F: magnitude of normal force
    - A: area of the surface on contact
  - as altitude increases, static pressure decreases
  - static or stagnation pressure
    - can exist in the absence of fluid velocity creating a potential energy component
  - dynamic pressure
    - exists when there is bulk fluid motion creating a kinetic energy component

- humidity
  - as humidity increases, density reduces
    - because water molecules (h2o) are lighter than oxygen (O2) or nitrogen (N2)

- viscosity
  - measure of fluid's resistance to deformation at a given rate
  - units: N * seconds / m^2, or pascal-seconds
  - air is considered 
    - fluid (described with same equations of fluid dynamics)
    - viscous

- masses
  - atomic
  - molar (g/mole)
    - measures weight of fixed number of particles defined by avogadro's number
    - relevant molar masses
      - H   = 1
      - H2  = 2
      - O   = 16
      - O2  = 32
      - N   = 14.01
      - N2  = 28.02
      - H20 = 18

- avogadro's number
  - number of elementary particles (molecules, atoms, compounds, etc.) per mole of a substance
  - it is equal to 6.022×10^23 mol^-1

- mach number
  - fraction/multiplier of a speed of sound in a medium for local conditions
  - e.g. 'mach 2' means 2 times speed of sound
  - depends on
    - temperature
    - atmospheric density/altitude
  - speed of sound at sea level is about 340 m/s



## references

[1]: https://www.youtube.com/watch?v=6xIsYcNHeZg&list=PLncfeagBRbBf-B-731Cp_a5wE_zxye0OP
[2]: https://youtu.be/jFk5UO6XgnQ?si=gZCOQTgkiK86llQi
[3]: https://aviation.stackexchange.com/questions/92450/taper-sweep-angle
[4]: https://aviation.stackexchange.com/questions/98084/why-does-an-aircraft-require-less-power-when-it-is-flying-slower-than-the-most-e
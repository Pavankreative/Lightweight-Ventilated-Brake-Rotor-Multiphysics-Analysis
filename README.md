**Design and Multiphysics Simulation of a Lightweight Ventilated Brake Rotor for Electric Vehicles**

This repository documents the complete development of an engineering CAE project focused on the design and multiphysics simulation of a lightweight ventilated brake rotor for electric vehicles.

The project investigates how a brake rotor for a representative electric two-wheeler can be designed with reduced mass while maintaining a rational basis for thermal, structural, and dynamic performance.

The development workflow begins with the vehicle braking scenario and proceeds through analytical calculations, material-selection strategy, preliminary ventilated rotor geometry, frictional heat-flux derivation, thermal boundary-condition modelling, CAD generation, meshing, and transient thermal analysis in ANSYS Workbench 2026 R1.

## Project Objective

During braking, the kinetic energy of the vehicle must be dissipated primarily as heat. A brake rotor must therefore manage rapid frictional heating, transient temperature gradients, heat conduction, convective cooling, thermal expansion, possible thermal stress, and repeated thermal cycles.

The primary engineering question is:

> How can the geometry of an electric-vehicle brake rotor be modified to reduce mass while maintaining acceptable thermal, structural, and dynamic performance under representative braking conditions?

## Project Workflow

```text
Engineering Requirements
        |
Analytical Calculations
        |
Material Selection
        |
Parametric CAD
        |
Transient Thermal Analysis
        |
Thermo-Structural Analysis
        |
Modal Analysis
        |
Design Study and Optimization
```

## Project Phases

```text
Phase 1
|
|-- Engineering Design Basis
|   |-- Reference vehicle
|   |-- Braking load cases
|   |-- Kinetic energy
|   |-- Braking force
|   |-- Front-brake energy allocation
|   |-- Wheel braking torque

Phase 2A
|
|-- Material Selection and Preliminary Rotor Geometry
|   |-- Material comparison
|   |-- Ventilated rotor architecture
|   |-- Rotor dimensions
|   |-- Friction track
|   |-- Effective braking radius

Phase 2B
|
|-- Brake Contact Geometry and Heat-Flux Derivation
|   |-- Annular friction area
|   |-- Rotor energy input
|   |-- Heat distribution
|   |-- Average heat flux
|   |-- Time-dependent heat flux
|   |-- Energy consistency verification

Phase 2C
|
|-- Thermal Boundary Conditions and Cooling Model
|   |-- Initial temperature
|   |-- Ambient temperature
|   |-- Convection
|   |-- Internal cooling model
|   |-- Edge cooling
|   |-- Hub thermal sink
|   |-- Radiation model
|   |-- Transient simulation timeline

Phase 3A
|
|-- CAD and ANSYS Transient Thermal Simulation
    |-- Geometry creation
    |-- Material assignment
    |-- Mesh development
    |-- Thermal boundary conditions
    |-- Transient solution
    |-- Temperature contours
    |-- Total heat flux
    |-- Temperature-probe response
```

The Phase 1 to Phase 2C design basis defines the original engineering model, including a 195 kg vehicle-plus-rider system, 80 km/h emergency stop, 70% front-brake allocation, 90% rotor heat partition, 240 mm ventilated rotor, and a 4-second braking event.

## 1. Engineering Design Basis

### 1.1 Reference Vehicle

| Parameter | Symbol | Value |
| --- | --- | --- |
| Vehicle mass | $m_v$ | 120 kg |
| Rider mass | $m_r$ | 75 kg |
| Total mass | $m$ | 195 kg |
| Maximum analysis speed | $v_0$ | 80 km/h |
| Final speed | $v_f$ | 0 km/h |
| Wheel rolling radius | $r_w$ | 0.30 m |
| Emergency braking duration | $t_b$ | 4 s |
| Front braking distribution | $\beta_f$ | 0.70 |
| Rear braking distribution | $\beta_r$ | 0.30 |
| Number of front rotors | $N_r$ | 1 |

These parameters form the baseline design case.

### 1.2 Braking Load Cases

| Load Case | Description | Initial Speed | Braking Time | Purpose |
| --- | --- | --- | --- | --- |
| LC-1 | Urban braking | 40 km/h | 3 s | Normal operation |
| LC-2 | Highway braking | 60 km/h | 4 s | Primary comparison |
| LC-3 | Emergency braking | 80 km/h | 4 s | Severe baseline thermal case |

The severe LC-3 case was selected as the baseline thermal scenario.

## 2. Analytical Braking Calculations

### 2.1 Speed Conversion

The baseline initial speed is:

$$
v_0 = 80 \text{ km/h}
$$

Conversion to SI units:

$$
v_0 = 80 \times \frac{1000}{3600}
$$

$$
v_0 = 22.22 \text{ m/s}
$$

### 2.2 Vehicle Kinetic Energy

The translational kinetic energy is:

$$
KE = \frac{1}{2}mv_0^2
$$

Substituting:

$$
KE = \frac{1}{2}(195)(22.22)^2
$$

$$
KE \approx 48,150 \text{ J}
$$

$$
KE \approx 48.15 \text{ kJ}
$$

This represents the total translational kinetic energy available for dissipation during the emergency braking event.

### 2.3 Front-Brake Energy Allocation

A preliminary front-brake distribution of 70% was adopted.

$$
\beta_f = 0.70
$$

$$
E_f = \beta_f \times KE
$$

$$
E_f = 0.70 \times 48.15
$$

$$
E_f = 33.70 \text{ kJ}
$$

Since the baseline configuration contains one front rotor, this front-brake energy forms the basis for the subsequent rotor heat-partition calculation.

### 2.4 Rotor Heat Partition

Not all braking energy is assumed to enter the rotor. A preliminary rotor heat-partition factor was defined as:

$$
\eta_h = 0.90
$$

$$
Q_{rotor} = \eta_h E_f
$$

$$
Q_{rotor} = 0.90 \times 33.70
$$

$$
Q_{rotor} = 30.33 \text{ kJ}
$$

This is the total modelled thermal energy assigned to the rotor during the braking event.

### 2.5 Average Rotor Thermal Power

The braking event lasts:

$$
t_b = 4 \text{ s}
$$

$$
P_{avg} = \frac{Q_{rotor}}{t_b}
$$

$$
P_{avg} = \frac{30,330}{4}
$$

$$
P_{avg} = 7,582.5 \text{ W}
$$

$$
P_{avg} \approx 7.58 \text{ kW}
$$

### 2.6 Vehicle Deceleration

$$
a = \frac{v_f - v_0}{t_b}
$$

$$
a = \frac{0 - 22.22}{4}
$$

$$
a = -5.56 \text{ m/s}^2
$$

The negative sign indicates deceleration.

### 2.7 Total Braking Force

The equivalent braking force is:

$$
F_b = ma
$$

Using the magnitude of deceleration:

$$
F_b = 195 \times 5.56
$$

$$
F_b \approx 1,084 \text{ N}
$$

The front-wheel braking force is:

$$
F_{b,f} = \beta_f F_b
$$

$$
F_{b,f} = 0.70 \times 1,084
$$

$$
F_{b,f} \approx 759 \text{ N}
$$

### 2.8 Equivalent Front-Wheel Braking Torque

The wheel rolling radius is:

$$
r_w = 0.30 \text{ m}
$$

$$
T_w = F_{b,f} r_w
$$

$$
T_w = 759 \times 0.30
$$

$$
T_w \approx 228 \text{ N.m}
$$

This is the equivalent wheel-level braking torque. Future structural analysis can convert this into an equivalent contact-region or tangential loading condition based on the effective friction radius.

## 3. Material Selection Strategy

The material-selection stage considered the requirements of both the current thermal model and future structural simulations.

| Criterion | Grey Cast Iron | Martensitic Stainless Steel | High-Carbon Steel |
| --- | --- | --- | --- |
| Thermal conductivity | Good | Moderate | Moderate |
| Wear resistance | Excellent | Good | Good |
| Corrosion resistance | Poor | Excellent | Poor |
| Typical brake relevance | Very common | Common in motorcycles/lightweight discs | Application dependent |
| Baseline project suitability | High | Very high | Medium |

The recommended baseline material was:

**AISI 420-type martensitic stainless steel**

The exact material-property dataset used in ANSYS should be traceable and recorded with its applicable temperature range.

## 4. Ventilated Rotor Architecture

The baseline design uses a two-plate ventilated rotor rather than a conventional single 5 mm solid disc.

The architecture consists of:

- Top friction plate
- Bottom friction plate
- Internal ventilation gap
- Radial connecting vanes
- Central mounting region
- Annular friction track

The purpose of this configuration is to provide:

- Lower mass potential
- Increased cooling surface area
- Internal heat-transfer paths
- Separation of the friction plates
- A basis for future design optimization

## 5. Preliminary Rotor Geometry

| Parameter | Symbol | Baseline Value |
| --- | --- | --- |
| Rotor outer diameter | $D_o$ | 240 mm |
| Friction track inner diameter | $D_f$ | 150 mm |
| Central mounting bore | $D_c$ | 70 mm |
| Mounting PCD | $D_{PCD}$ | 100 mm |
| Number of mounting holes | $N_h$ | 6 |
| Mounting-hole diameter | $d_h$ | 8 mm |
| Total rotor thickness | $t_{total}$ | 12 mm |
| Top friction plate thickness | $t_{top}$ | 3 mm |
| Bottom friction plate thickness | $t_{bottom}$ | 3 mm |
| Ventilation gap | $g_v$ | 6 mm |
| Preliminary vane count | $N_v$ | 24 |
| Preliminary vane thickness | $t_v$ | 2 mm |

The total thickness is:

$$
t_{total} = t_{top} + g_v + t_{bottom}
$$

$$
t_{total} = 3 + 6 + 3
$$

$$
t_{total} = 12 \text{ mm}
$$

## 6. Friction Track and Effective Radius

The outer friction radius is:

$$
r_o = \frac{240}{2} = 120 \text{ mm} = 0.120 \text{ m}
$$

The inner friction radius is:

$$
r_i = \frac{150}{2} = 75 \text{ mm} = 0.075 \text{ m}
$$

For a uniformly loaded annular surface, the area-weighted effective radius is:

$$
r_{eff} = \frac{2}{3}\frac{r_o^3-r_i^3}{r_o^2-r_i^2}
$$

Using the baseline dimensions:

$$
r_{eff} \approx 0.099 \text{ m} = 99 \text{ mm}
$$

## 7. Initial Design Optimization Variables

| Variable | Symbol | Preliminary Range |
| --- | --- | --- |
| Friction plate thickness | $t_p$ | 2.5 to 4 mm |
| Ventilation gap | $g_v$ | 4 to 7 mm |
| Vane count | $N_v$ | 18 to 30 |

These variables directly influence rotor mass, thermal capacity, cooling surface area, and structural stiffness.

## 8. Thermal Loading Representation

In an actual braking system, the brake pads contact localized sectors of the rotor. In the Version 1 model, explicit rotor rotation and a moving heat source were not modelled.

Instead, frictional heating was represented as:

> A circumferentially smeared, time-dependent heat flux applied over the annular friction track on both rotor faces.

This approximation preserves the total modelled energy while simplifying the transient analysis.

## 9. Brake Contact Geometry and Heat-Flux Derivation

### 9.1 Annular Friction Area

The friction area per rotor face is:

$$
A_f = \pi(r_o^2-r_i^2)
$$

Substituting:

$$
A_f = \pi(0.120^2-0.075^2)
$$

$$
A_f \approx 0.02757 \text{ m}^2
$$

Therefore:

$$
A_f \approx 275.7 \text{ cm}^2
$$

### 9.2 Heat Distribution Between Rotor Faces

The total rotor thermal energy is:

$$
Q_{rotor} = 30.33 \text{ kJ}
$$

Assuming equal distribution between the two friction surfaces:

$$
Q_{face} = \frac{Q_{rotor}}{2}
$$

$$
Q_{face} = \frac{30.33}{2}
$$

$$
Q_{face} = 15.165 \text{ kJ}
$$

Similarly:

$$
P_{avg,face} = \frac{P_{avg}}{2}
$$

$$
P_{avg,face} = \frac{7.5825}{2}
$$

$$
P_{avg,face} \approx 3.791 \text{ kW}
$$

### 9.3 Constant Average Heat Flux

The average heat flux per friction surface is:

$$
q''_{avg} = \frac{P_{avg,face}}{A_f}
$$

Substituting:

$$
q''_{avg} = \frac{3791}{0.02757}
$$

$$
q''_{avg} \approx 137,500 \text{ W/m}^2
$$

This is the energy-equivalent constant heat-flux reference for a 4-second braking event.

### 9.4 Time-Dependent Heat Flux Model

Under constant deceleration, vehicle speed decreases approximately linearly. If braking force is approximately constant, braking power also decreases with vehicle speed. Therefore, a linearly decreasing heat-flux profile was adopted.

The heat flux is defined as:

$$
q''(t)=q''_{max}\left(1-\frac{t}{4}\right)
$$

For:

$$
0 \leq t \leq 4 \text{ s}
$$

To preserve the total modelled rotor energy, the initial heat flux must be twice the average heat flux.

### 9.5 Maximum Braking Power

The maximum total thermal power is:

$$
P_{max,total} = \frac{2Q_{rotor}}{t_b}
$$

$$
P_{max,total} = \frac{2(30,330)}{4}
$$

$$
P_{max,total} = 15,165 \text{ W}
$$

The maximum power per rotor face is:

$$
P_{max,face} = \frac{15,165}{2}
$$

$$
P_{max,face} = 7,582.5 \text{ W}
$$

### 9.6 Maximum Heat Flux

The maximum heat flux per friction surface is:

$$
q''_{max} = \frac{P_{max,face}}{A_f}
$$

$$
q''_{max} = \frac{7582.5}{0.02757}
$$

$$
q''_{max} \approx 275,000 \text{ W/m}^2
$$

The final theoretical heat-flux equation is:

$$
q''(t)=275,000\left(1-\frac{t}{4}\right) \text{ W/m}^2
$$

For:

$$
0 \leq t \leq 4 \text{ s}
$$

### 9.7 Complete Heat-Flux Table

| Time (s) | Heat Flux (W/m²) |
| --- | --- |
| 0.0 | 275,000 |
| 0.5 | 240,625 |
| 1.0 | 206,250 |
| 1.5 | 171,875 |
| 2.0 | 137,500 |
| 2.5 | 103,125 |
| 3.0 | 68,750 |
| 3.5 | 34,375 |
| 4.0 | 0 |

The heat flux is applied to both annular friction surfaces.

### 9.8 Energy Consistency Verification

For a linearly decreasing heat-flux profile, the average heat flux is:

$$
\frac{q''_{max}}{2}
$$

The total energy input across both friction surfaces is:

$$
Q = 2A_f\left(\frac{1}{2}q''_{max}t_b\right)
$$

Substituting:

$$
Q = 2(0.02757)\left(\frac{1}{2}(275,000)(4)\right)
$$

$$
Q \approx 30.33 \text{ kJ}
$$

Thus, the transient heat-flux boundary condition is energy-consistent with the rotor heat input derived from the braking event.

### 9.9 Equivalent Tangential Force at the Rotor

The equivalent tangential force is estimated using:

$$
F_t = \frac{T_w}{r_{eff}}
$$

Substituting:

$$
F_t = \frac{228}{0.099}
$$

$$
F_t \approx 2,303 \text{ N}
$$

Assuming first-order equal distribution between the two friction faces:

$$
F_{face} \approx 1,152 \text{ N per face}
$$

This value is retained as a preliminary input for future structural modelling.

## 10. Thermal Boundary Conditions and Cooling Model

### 10.1 Original Design-Basis Simulation Timeline

| Time Interval | Condition |
| --- | --- |
| $t=0$ | Rotor initially at 25 °C |
| 0 to 4 s | Braking heat input |
| 4 to 60 s | Heat input removed and cooling |
| Total | 60 s |

The original Phase 2C design basis used:

$$
T_{initial}=25^\circ C
$$

$$
T_\infty=25^\circ C
$$

### 10.2 Cooling Mechanisms

The full theoretical baseline included:

- Convection
- Thermal radiation
- Equivalent heat transfer into the mounting/hub region

The convection equation is:

$$
q_{conv}=hA(T_s-T_\infty)
$$

The radiation equation is:

$$
q_{rad}=\varepsilon\sigma A(T_s^4-T_{sur}^4)
$$

For physical radiation calculations, temperatures must be expressed in absolute units.

### 10.3 Original Convection and Thermal-Sink Model

| Region | Boundary Representation | Baseline Value |
| --- | --- | --- |
| External friction/exposed surfaces | Convection | 50 W/m².K |
| Internal vane/channel surfaces | Convection | 80 W/m².K |
| Outer edge surfaces | Convection | 60 W/m².K |
| Mounting interface | Equivalent thermal sink | 20 W/m².K |

The hub-side value was defined as an effective thermal-sink approximation rather than literal external convection.

### 10.4 Original Radiation Model

The theoretical Phase 2C model also defined:

$$
\varepsilon = 0.60
$$

$$
T_{sur}=25^\circ C
$$

This emissivity was treated as an assumed effective baseline value.

### 10.5 Complete Theoretical Heat-Flux History

$$
q''(t)=
\begin{cases}
275,000\left(1-\frac{t}{4}\right), & 0 \leq t \leq 4 \text{ s} \\
0, & 4 < t \leq 60 \text{ s}
\end{cases}
$$

The heat flux is applied to both annular friction surfaces.

### 10.6 Recommended Time Resolution

| Interval | Recommended Time Increment |
| --- | --- |
| 0 to 4 s | 0.1 to 0.25 s |
| 4 to 60 s | Approximately 1 s or automatic stepping |

### 10.7 Material Properties Required in ANSYS

| Analysis | Required Properties |
| --- | --- |
| Transient Thermal | Density, specific heat capacity, thermal conductivity |
| Thermo-Structural | Young's modulus, Poisson's ratio, coefficient of thermal expansion, yield strength |
| Advanced Model | Temperature-dependent thermal and mechanical properties |

## 11. Final Theoretical Baseline Model Specification

| Item | Baseline Definition |
| --- | --- |
| Vehicle-plus-rider mass | 195 kg |
| Critical braking event | 80 km/h to 0 in 4 s |
| Vehicle kinetic energy | 48.15 kJ |
| Front-brake allocation | 70% |
| Front-brake energy | 33.70 kJ |
| Rotor heat partition | 90% |
| Modelled rotor heat input | 30.33 kJ |
| Rotor architecture | 240 mm two-plate ventilated rotor |
| Friction area per face | 0.02757 m² |
| Peak heat flux per face | 275,000 W/m² |
| Original initial/ambient temperature | 25 °C / 25 °C |
| External convection | 50 W/m².K |
| Internal convection | 80 W/m².K |
| Edge convection | 60 W/m².K |
| Hub equivalent thermal sink | 20 W/m².K |
| Radiation emissivity | 0.60 |
| Braking phase | 0 to 4 s |
| Cooling phase | 4 to 60 s |

## 12. CAD Development

The geometry was subsequently created in ANSYS SpaceClaim 2026 R1 based on the preliminary ventilated rotor architecture.

The design basis specified:

- 240 mm rotor outer diameter
- Two 3 mm friction plates
- 6 mm ventilation gap
- Preliminary 24 radial vanes
- Six mounting holes
- Parametric dimensions for future optimization

The resulting CAD model was transferred to ANSYS Mechanical as a single solid body for the baseline thermal simulation.

## 13. Actual Implemented ANSYS Transient Thermal Model

The completed ANSYS model should be distinguished from the original full theoretical Phase 2C specification. During implementation, the simulation model was simplified to produce a stable, solvable baseline.

The completed model included:

- Transient Thermal Analysis
- 60-second analysis duration
- Heat flux applied to the top friction surface
- Heat flux applied to the bottom friction surface
- Convection applied to the selected outer cooling region
- Initial temperature of 22 °C
- Ambient temperature of 22 °C
- Automatic transient time stepping
- Temperature result
- Total Heat Flux result
- Temperature Probe

The implemented simulation represents:

> Baseline Version 1 of the multiphysics project.

The internal cooling surfaces originally proposed in Phase 2C were not included in the completed ANSYS model. Radiation and the hub equivalent thermal sink were also not part of the implemented baseline.

## 14. Mesh Development

The initial mesh generated for the model contained:

| Mesh Parameter | Value |
| --- | --- |
| Nodes | 623,036 |
| Elements | 407,894 |

The initial high-resolution mesh created solver difficulties. The mesh was subsequently simplified to obtain a computationally manageable and successfully solved baseline transient model.

The final baseline therefore prioritizes a successful solution within the available computational/license environment. A formal mesh-convergence study remains future work.

## 15. Implemented Heat-Flux Loading

The ANSYS model used the transient heat-flux concept derived analytically from the braking event.

The principal values entered during implementation included:

| Time | Heat Flux |
| --- | --- |
| 0 s | 275,000 W/m² |
| 1 s | 206,250 W/m² |
| 4 s | 0 W/m² |
| 60 s | 0 W/m² |

These values are consistent with the analytical linearly decreasing heat-flux model derived from the braking event.

## 16. Simulation Results

The completed transient solution was evaluated over:

$$
0 \leq t \leq 60 \text{ s}
$$

The following results were extracted:

- Temperature distribution
- Total Heat Flux
- Temperature Probe

Temperature contours were evaluated at:

- 10 seconds
- 30 seconds
- 60 seconds

### 16.1 Temperature Distribution at 10 Seconds

| Parameter | Value |
| --- | --- |
| Maximum Temperature | 33.117 °C |
| Minimum Temperature | 21.997 °C |

By 10 seconds, the intense braking heat-input period had already ended and the rotor was undergoing thermal redistribution and cooling.

### 16.2 Temperature Distribution at 30 Seconds

| Parameter | Value |
| --- | --- |
| Maximum Temperature | 28.161 °C |
| Minimum Temperature | 22.003 °C |

The temperature field continued to decay toward ambient conditions.

### 16.3 Temperature Distribution at 60 Seconds

| Parameter | Value |
| --- | --- |
| Maximum Temperature | 26.512 °C |
| Minimum Temperature | 22.136 °C |

The final temperature rise above the implemented ambient temperature is:

$$
\Delta T = 26.512 - 22
$$

$$
\Delta T = 4.512^\circ C
$$

### 16.4 Temperature Probe Results

| Time (s) | Temperature (°C) |
| --- | --- |
| 0.1 | 32.339 |
| 0.2 | 36.993 |
| 0.437 | 42.485 |
| 0.937 | 48.443 |
| 1.437 | 51.188 |
| 1.937 | approximately 52 |
| 2.437 | 51.438 |
| 2.937 | 49.541 |
| 3.437 | 47.117 |
| 4.013 | 43.661 |
| 4.892 | 40.392 |
| 5.392 | 39.056 |
| 6.392 | 37.022 |
| 7.392 | 35.557 |
| 8.392 | 34.445 |
| 9.392 | 33.565 |
| 10.392 | 32.851 |
| 20.392 | 29.447 |
| 30.392 | 28.124 |
| 40.392 | 27.368 |
| 50.392 | 26.865 |
| 60.000 | 26.512 |

### 16.5 Peak Temperature

The highest recorded temperature at the probe was approximately:

$$
T_{peak} \approx 52^\circ C
$$

The peak occurred at approximately:

$$
t_{peak} \approx 1.94 \text{ s}
$$

This result is important because it occurred before the first contour snapshot at 10 seconds. Therefore, the 10-second maximum temperature should not be interpreted as the maximum temperature experienced during the complete braking event.

The probe shows the actual early transient thermal spike.

### 16.6 Thermal Response Stages

The transient response can be divided into three stages.

| Stage | Approximate Time Range | Description |
| --- | --- | --- |
| Stage 1: Rapid Heating | 0 to 2 s | Temperature rapidly increased because of the applied frictional heat flux. |
| Stage 2: Rapid Cooling | 2 to 10 s | After the braking heat input decreased and reached zero, the local temperature dropped rapidly. |
| Stage 3: Gradual Cooling | 10 to 60 s | Cooling rate progressively decreased as the rotor approached ambient temperature. |

Overall response:

```text
Rapid frictional heating
        |
Local temperature peak approximately 52 °C
        |
Rapid thermal relaxation
        |
Progressive cooling
        |
26.512 °C at 60 s
```

### 16.7 Total Heat Flux Result

The post-processed Total Heat Flux result produced:

| Parameter | Value |
| --- | --- |
| Maximum Total Heat Flux | 2546.6 W/m² |
| Minimum Total Heat Flux | approximately 0.163 W/m² |

The applied surface heat flux and the resulting Total Heat Flux should not be confused.

| Quantity | Meaning |
| --- | --- |
| Applied Heat Flux | Prescribed thermal boundary condition |
| Total Heat Flux | Resulting heat-flow field associated with thermal gradients in the solved model |

## 17. Key Results Summary

| Parameter | Result |
| --- | --- |
| Vehicle mass + rider | 195 kg |
| Critical braking speed | 80 km/h |
| Braking duration | 4 s |
| Vehicle kinetic energy | 48.15 kJ |
| Front-brake allocation | 70% |
| Front-brake energy | 33.70 kJ |
| Rotor heat partition | 90% |
| Rotor thermal input | 30.33 kJ |
| Rotor outer diameter | 240 mm |
| Rotor total thickness | 12 mm |
| Ventilation gap | 6 mm |
| Vane count | 24 |
| Friction area per face | 0.02757 m² |
| Average heat flux | 137,500 W/m² |
| Peak heat flux | 275,000 W/m² |
| Peak probe temperature | approximately 52 °C |
| Time of peak | approximately 1.94 s |
| Maximum temperature at 10 s | 33.117 °C |
| Maximum temperature at 30 s | 28.161 °C |
| Maximum temperature at 60 s | 26.512 °C |
| Final temperature rise above 22 °C | 4.512 °C |
| Maximum post-processed Total Heat Flux | 2546.6 W/m² |
| Total simulation duration | 60 s |

## 18. Assumptions and Limitations

The original Phase 1 to Phase 2C design record identifies the following assumptions:

- Rotor rotation and a physically moving pad heat source are not explicitly modelled.
- Heat input is circumferentially smeared over the friction track.
- The 70% front-brake allocation is a preliminary assumption.
- The 90% rotor heat partition is a preliminary assumption.
- Convection coefficients in the theoretical model are equivalent baseline parameters and are not CFD-derived.
- Wheel hub, caliper, brake pads, and detailed thermal contact resistance are not explicitly modelled.
- Temperature-dependent material properties are future refinements.
- Temperature-dependent friction behaviour is not included.
- The project is an engineering simulation case study and is not a certified production brake design.

For the actual implemented ANSYS baseline, additional simplifications occurred:

- Internal cooling surfaces were not included.
- The implemented initial/ambient temperature was 22 °C rather than the original 25 °C design-basis value.
- Radiation was not included.
- The hub thermal-sink boundary was not included.
- The mesh was simplified to obtain a solvable baseline.

## 19. Future Multiphysics Development

The current project has completed the first major CAE simulation stage.

### Phase 3B: Thermo-Structural Analysis

Transfer the temperature field into a structural model to investigate:

- Thermal deformation
- Equivalent stress
- Thermal stress concentration
- Rotor distortion

### Phase 4: Static Structural Analysis

Use the derived equivalent tangential braking load to investigate:

- Equivalent stress
- Total deformation
- Safety factor
- Stress concentration

### Phase 5: Modal Analysis

Investigate:

- Natural frequencies
- Mode shapes
- Vibration behaviour
- Potential resonance regions

### Phase 6: Design Optimization

The initial optimization variables are:

- Friction plate thickness
- Ventilation gap
- Vane count

Potential optimization objectives include:

- Minimizing mass
- Reducing peak temperature
- Reducing thermal stress
- Maintaining structural stiffness
- Improving dynamic behaviour

## 20. Repository Structure

```text
Lightweight-Ventilated-Brake-Rotor-Multiphysics-Analysis/
|
|-- README.md
|
|-- 01_Engineering_Design_Basis/
|   |-- Phase1_to_Phase2C_Engineering_Record.pdf
|   |-- Design_Calculations/
|
|-- 02_CAD_Geometry/
|   |-- Geometry_Files/
|   |-- Geometry_Images/
|
|-- 03_ANSYS_Transient_Thermal/
|   |-- ANSYS_Project/
|   |-- Mesh/
|   |-- Boundary_Conditions/
|   |-- Results/
|   |   |-- Temperature_10s.png
|   |   |-- Temperature_30s.png
|   |   |-- Temperature_60s.png
|   |   |-- Total_Heat_Flux.png
|   |   |-- Temperature_Probe.png
|   |
|   |-- Data/
|       |-- Temperature_Probe_Data.csv
|
|-- 04_Project_Documentation/
|   |-- Project_Report.pdf
|
|-- Images/
    |-- Geometry.png
    |-- Mesh.png
    |-- Friction_Surface.png
    |-- Heat_Flux.png
    |-- Convection.png
```

## 21. Software Used

- ANSYS Workbench 2026 R1
- ANSYS SpaceClaim
- ANSYS Mechanical
- GitHub

## 22. Project Status

| Phase | Status |
| --- | --- |
| Phase 1: Engineering Design Basis | Completed |
| Phase 2A: Material Selection | Completed |
| Phase 2A: Preliminary Geometry | Completed |
| Phase 2B: Heat-Flux Derivation | Completed |
| Phase 2C: Thermal Boundary Conditions | Completed |
| Phase 3A: CAD Development | Completed |
| Phase 3A: Transient Thermal Analysis | Completed |
| Phase 3B: Thermo-Structural Analysis | Planned |
| Phase 4: Static Structural Analysis | Planned |
| Phase 5: Modal Analysis | Planned |
| Phase 6: Design Optimization | Planned |

## Author

**Pavan Kumar Karisanapu**

Mechanical Engineering | CAE | FEA | CFD | Thermal Analysis | Engineering Research

GitHub: [Pavankreative](https://github.com/Pavankreative)

## Final Statement

This repository documents the complete engineering development of a lightweight ventilated brake rotor concept, beginning with vehicle braking physics and analytical energy calculations, progressing through material-selection strategy and ventilated rotor geometry, and culminating in a successfully solved transient thermal simulation.

The analytical design basis predicts a modelled rotor heat input of:

$$
\boxed{30.33 \text{ kJ}}
$$

during an emergency braking event from:

$$
\boxed{80 \text{ km/h} \rightarrow 0 \text{ km/h in } 4 \text{ s}}
$$

The corresponding energy-consistent peak heat flux is:

$$
\boxed{275,000 \text{ W/m}^2}
$$

per friction surface.

The completed ANSYS transient model captured a local thermal peak of approximately:

$$
\boxed{52^\circ C}
$$

at approximately:

$$
\boxed{1.94 \text{ s}}
$$

followed by progressive cooling to:

$$
\boxed{26.512^\circ C}
$$

at the end of the 60-second simulation.

This completed thermal baseline forms the foundation for the remaining multiphysics stages: thermo-structural analysis, static structural analysis, modal analysis, and design optimization.

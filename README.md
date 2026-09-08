#**Design and Multiphysics Simulation of a Lightweight Ventilated Brake Rotor for Electric Vehicles**#

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

## 17. Static Structural Analysis

A standalone Static Structural analysis was performed to evaluate the mechanical response of the lightweight ventilated brake rotor under the calculated severe-braking torque.

The structural analysis was developed independently from the transient thermal analysis. The transient thermal temperature field was **not transferred** into the Static Structural model. Therefore, the results presented in this section represent a **mechanical-only Static Structural baseline**, not a coupled thermo-structural analysis.

### 17.1 Objective

The main objectives of the Static Structural analysis were:

- Evaluate the deformation of the brake rotor under the calculated braking torque.
- Determine the equivalent (von-Mises) stress distribution.
- Determine the maximum and minimum principal stresses.
- Evaluate the equivalent elastic strain.
- Assess the baseline structural stiffness of the rotor.
- Establish a structural reference case for future thermo-structural analysis and design optimization.

### 17.2 Structural Analysis Setup

The Static Structural analysis was created in ANSYS Workbench using the developed ventilated brake rotor geometry.

| Parameter | Value |
|---|---:|
| Analysis type | Static Structural |
| Software | ANSYS Workbench / ANSYS Mechanical |
| Material | Structural Steel |
| Rotor outer diameter | 240 mm |
| Friction track inner diameter | 150 mm |
| Central bore diameter | 70 mm |
| Mounting PCD | 100 mm |
| Number of mounting holes | 6 |
| Mounting hole diameter | 8 mm |
| Total rotor thickness | 12 mm |
| Number of ventilation vanes | 24 |
| Vane thickness | 2 mm |
| Applied braking moment | 228 N·m |

### 17.3 Material Definition

**Structural Steel** was assigned to the brake rotor in the Static Structural analysis.

The current structural model uses the material as a baseline structural representation. Temperature-dependent material properties were not included because the thermal temperature field was not successfully coupled to the structural model.

Therefore, the calculated structural results represent the mechanical response under the applied braking torque at the defined baseline material condition.

### 17.4 Structural Mesh

Several mesh sizes were investigated during the structural analysis to obtain a computationally manageable model within the ANSYS Student limitations.

The final structural mesh used a nominal element size of **9 mm**.

| Element Size | Nodes | Elements | Status |
|---|---:|---:|---|
| 5 mm | 274,776 | 182,590 | Exceeded computational limit |
| 8 mm | 130,742 | 85,990 | Exceeded 128k-node limit |
| 9 mm | 114,520 | 75,119 | Accepted and successfully solved |

The final structural mesh contained:

- **114,520 nodes**
- **75,119 elements**
- **9 mm nominal element size**

The 9 mm mesh was selected because it remained within the available ANSYS Student computational constraints and successfully completed the structural solution.

A formal mesh-convergence study has not yet been completed. Therefore, the 9 mm mesh should be considered a **baseline computational mesh** rather than a fully convergence-validated mesh.

### 17.5 Boundary Conditions

A **Fixed Support** was applied to the cylindrical faces of the six mounting holes.

These mounting-hole regions represent the attachment locations of the brake rotor to the hub or wheel assembly.

The fixed support prevents rigid-body motion and provides the structural constraint required for the static solution.

The six mounting-hole cylindrical faces were therefore treated as fixed structural interfaces for the current baseline analysis.

### 17.6 Applied Braking Moment

The equivalent braking torque calculated from the severe braking condition was:

\[
T = 228\ \mathrm{N\,m}
\]

A braking moment of **228 N·m** was applied to the annular friction region of the rotor.

The moment was defined about the central rotational axis of the rotor.

The corresponding equivalent tangential force was calculated using:

\[
F_t = \frac{T}{r_{\mathrm{eff}}}
\]

where:

- \(T = 228\) N·m
- \(r_{\mathrm{eff}} \approx 0.099\) m

Therefore:

\[
F_t \approx 2303\ \mathrm{N}
\]

For the two friction faces, the equivalent force representation is approximately:

\[
F_{\mathrm{face}} \approx 1152\ \mathrm{N}
\]

per friction face.

The ANSYS structural model directly applies the **228 N·m braking moment** rather than explicitly applying separate tangential friction forces.

### 17.7 Structural Result Objects

The following result objects were evaluated in ANSYS Mechanical:

1. **Total Deformation**
2. **Equivalent (von-Mises) Stress**
3. **Maximum Principal Stress**
4. **Minimum Principal Stress**
5. **Equivalent Elastic Strain**

These results were evaluated for the applied 228 N·m braking moment with the six mounting-hole cylindrical faces fixed.

---

### 17.8 Total Deformation

The maximum Total Deformation obtained from the Static Structural analysis was:

**9.1413 × 10⁻⁷ m**

Equivalent value:

**0.000914 mm**

| Result | Maximum Value |
|---|---:|
| Total Deformation | 9.1413 × 10⁻⁷ m |
| Total Deformation | 0.000914 mm |

The calculated deformation is very small compared with the overall dimensions of the rotor.

The result indicates a low mechanical deformation response under the defined braking torque and boundary conditions.

---

### 17.9 Equivalent (von-Mises) Stress

The maximum Equivalent (von-Mises) Stress obtained from the analysis was:

**3.1347 × 10⁶ Pa**

Equivalent value:

**3.135 MPa**

| Result | Maximum Value |
|---|---:|
| Equivalent (von-Mises) Stress | 3.1347 × 10⁶ Pa |
| Equivalent (von-Mises) Stress | 3.135 MPa |

The calculated von-Mises stress represents the mechanical stress response produced by the applied braking torque under the defined structural constraints.

The current result is a baseline mechanical stress value. It does not include thermal stress or other loading effects that may occur during actual braking operation.

---

### 17.10 Maximum Principal Stress

The maximum principal stress obtained from the analysis was:

**1.9152 × 10⁶ Pa**

Equivalent value:

**1.915 MPa**

| Result | Maximum Value |
|---|---:|
| Maximum Principal Stress | 1.915 MPa |

The maximum principal stress provides an additional representation of the tensile stress state within the rotor.

This result complements the von-Mises stress evaluation and provides additional information about the local stress state.

---

### 17.11 Minimum Principal Stress

The minimum principal stress obtained from the analysis was approximately:

**-2.545 MPa**

| Result | Value |
|---|---:|
| Minimum Principal Stress | ≈ -2.545 MPa |

The negative value indicates a compressive principal stress state in portions of the rotor.

Therefore, the structural model contains both tensile and compressive principal stress regions under the applied braking moment.

---

### 17.12 Equivalent Elastic Strain

The maximum Equivalent Elastic Strain obtained from the Static Structural analysis was approximately:

**1.677 × 10⁻⁵**

| Result | Maximum Value |
|---|---:|
| Equivalent Elastic Strain | ≈ 1.677 × 10⁻⁵ |

The small elastic strain is consistent with the low deformation and stress levels obtained from the structural solution.

---

### 17.13 Static Structural Results Summary

| Parameter | Result |
|---|---:|
| Applied braking moment | 228 N·m |
| Structural mesh size | 9 mm |
| Structural nodes | 114,520 |
| Structural elements | 75,119 |
| Maximum total deformation | 9.1413 × 10⁻⁷ m |
| Maximum total deformation | 0.000914 mm |
| Maximum von-Mises stress | 3.135 MPa |
| Maximum principal stress | 1.915 MPa |
| Minimum principal stress | ≈ -2.545 MPa |
| Maximum equivalent elastic strain | ≈ 1.677 × 10⁻⁵ |

### 17.14 Structural Interpretation

The Static Structural baseline indicates that the proposed ventilated brake rotor has a very small deformation response under the defined **228 N·m braking torque**.

The maximum calculated deformation is approximately **0.000914 mm**, which is very small compared with the 240 mm rotor diameter.

The maximum calculated von-Mises stress is approximately **3.135 MPa**, while the maximum principal stress is approximately **1.915 MPa**.

The calculated results indicate a relatively stiff mechanical response for the current rotor geometry, material and loading conditions.

However, these results should be interpreted only within the assumptions of the present model.

The analysis does not yet include:

- Thermal expansion.
- Thermally induced stress.
- Temperature-dependent material properties.
- Temperature gradients.
- Brake-pad contact pressure.
- Frictional contact.
- Rotor-pad contact behavior.
- Bolt preload.
- Hub flexibility.
- Wheel flexibility.
- Manufacturing tolerances.
- Fatigue loading.
- Cyclic braking.
- Detailed local stress-concentration refinement.
- Formal mesh-convergence verification.

Therefore, this analysis is classified as a:

**Static Structural Baseline**

rather than a complete thermo-mechanical structural assessment.

### 17.15 Structural Analysis Status

The Static Structural analysis was successfully solved using the final 9 mm structural mesh.

| Analysis Component | Status |
|---|---|
| Structural geometry | Completed |
| Material assignment | Completed |
| Structural mesh | Completed |
| Fixed Support | Completed |
| 228 N·m braking moment | Completed |
| Total Deformation | Successfully evaluated |
| Equivalent von-Mises Stress | Successfully evaluated |
| Maximum Principal Stress | Successfully evaluated |
| Minimum Principal Stress | Successfully evaluated |
| Equivalent Elastic Strain | Successfully evaluated |
| Thermo-structural temperature transfer | Not completed |

The Static Structural analysis therefore provides a completed **mechanical baseline** for the current brake rotor design.
## 18. Thermo-Structural Coupling Status
The next stage of the project was to combine the transient thermal response of the brake rotor with the Static Structural analysis in order to evaluate the combined thermo-mechanical behavior of the rotor.
The intended objective of the coupling was to transfer the transient temperature field obtained from the thermal analysis into the structural model and evaluate the resulting thermal expansion, thermal stress and combined structural response.

### 18.1 Intended Thermo-Structural Workflow
The planned ANSYS Workbench workflow was:

```text
Transient Thermal Analysis
          |
          | Temperature Field
          v
Static Structural Analysis
          |
          | 228 N·m Braking Moment
          v
Thermo-Structural Response
          |
          +----------------------+
          |                      |
          v                      v
Thermal Stress          Total Deformation
```

The coupled analysis would combine two primary loading contributions:
- Mechanical loading from the calculated 228 N·m braking moment.
- Thermal loading from the transient rotor temperature field.

The resulting structural solution would represent the combined thermal and mechanical response of the brake rotor.

### 18.2 Thermal Analysis Available for Coupling
The transient thermal analysis produced a usable baseline temperature history.
The maximum temperature obtained from the thermal analysis was approximately:
**52°C at approximately 1.94 s**

The rotor subsequently cooled during the remainder of the 60-second transient analysis.
Selected thermal results were:

| Time | Maximum Rotor Temperature |
|---|---|
| ≈ 1.94 s | ≈ 52°C |
| 10 s | 33.117°C |
| 30 s | 28.161°C |
| 60 s | 26.512°C |

The thermal temperature field was intended to provide the thermal loading input for the structural analysis.

### 18.3 Static Structural Analysis Available for Coupling
The Static Structural baseline was successfully developed and solved independently.
The structural model included:
- Structural Steel.
- Six mounting-hole cylindrical faces with Fixed Support.
- 228 N·m braking moment.
- 9 mm nominal structural mesh.
- 114,520 nodes.
- 75,119 elements.

The resulting baseline structural values were:

| Structural Result | Value |
|---|---|
| Applied braking moment | 228 N·m |
| Maximum total deformation | 0.000914 mm |
| Maximum von-Mises stress | 3.135 MPa |
| Maximum principal stress | 1.915 MPa |
| Minimum principal stress | ≈ -2.545 MPa |
| Maximum equivalent elastic strain | ≈ 1.677 × 10⁻⁵ |

These values represent the mechanical loading condition only.

### 18.4 Thermo-Structural Coupling Attempt
An attempt was made to establish the thermal-to-structural data transfer within ANSYS Workbench.
The objective was to connect the transient thermal solution to the Static Structural setup so that the calculated temperature field could be applied as a thermal load in the structural analysis.

The geometry relationship was successfully established, but the complete thermal Model/Setup/Solution transfer required for the coupled analysis was not successfully completed.
As a result, the Static Structural analysis remained an independent mechanical analysis.

The following conceptual workflow was therefore not successfully completed:

```text
Transient Thermal Solution
          |
          | Temperature Field
          v
Static Structural Setup
          |
          | + 228 N·m Mechanical Moment
          v
Coupled Thermo-Structural Solution
```

### 18.5 ANSYS Thermal Update Failure
During further attempts to update and work with the transient thermal system, the ANSYS solver encountered an I/O-related failure.
The solver reported:

```text
An error has occurred writing to file unit = 4
which may imply a full disk.
Random write error on file unit=4
possible full disk.
I/O status error = 22.
```

The available H: drive capacity was checked during troubleshooting.
Approximately **191 GB of 215 GB** was available on the H: drive.
The project scratch directory was also approximately **360 MB**.

Therefore, the available evidence did not support treating the problem simply as a conventional full-disk-capacity issue.
The exact root cause of the ANSYS I/O failure was not established during the current project iteration.
Possible causes may include:
- Solver file handling.
- Temporary-file operations.
- Scratch-directory behavior.
- File-path conditions.
- File permissions.
- Solver-level I/O conditions.
- ANSYS Student computational or environment limitations.

The I/O failure was therefore documented as a solver/workflow issue rather than being conclusively attributed to insufficient physical disk capacity.

### 18.6 Computational Constraints
The project was developed using the ANSYS Student environment.
Computational limitations affected the simulation workflow during the project.
For example, the structural mesh iterations produced the following results:

| Mesh Size | Nodes | Elements | Status |
|---|---|---|---|
| 5 mm | 274,776 | 182,590 | Exceeded computational limit |
| 8 mm | 130,742 | 85,990 | Exceeded 128k-node limit |
| 9 mm | 114,520 | 75,119 | Successfully solved |

The 9 mm structural mesh was therefore selected as the final baseline mesh.
These computational limitations also affected the ability to perform more demanding coupled simulations and extensive mesh refinement.

### 18.7 Current Thermo-Structural Status
The current status of the coupled analysis is:

| Component | Status |
|---|---|
| Brake rotor geometry | Completed |
| Transient thermal model | Completed baseline analysis |
| Thermal temperature history | Obtained |
| Static Structural model | Completed |
| Structural solution | Successfully obtained |
| Thermal-to-structural transfer | Not completed |
| Thermal expansion analysis | Not completed |
| Thermally induced stress | Not calculated |
| Combined thermo-mechanical stress | Not calculated |
| Coupled thermo-mechanical deformation | Not calculated |
| Fully coupled thermo-structural solution | Not completed |

### 18.8 Important Result Classification
The distinction between the completed analyses and the unfinished coupling is important.
The thermal analysis provides: **Transient Thermal Response**
The Static Structural analysis provides: **Mechanical Structural Response**

The project does not currently provide:
**Thermo-Structural Stress** or **Thermo-Mechanical Deformation**
because the temperature field was not successfully transferred into the structural model.

Therefore, the structural results reported in Section 17 must be interpreted strictly as standalone Static Structural results.
They should not be reported as combined thermal-mechanical stresses.

### 18.9 What the Completed Analyses Establish
Although the final coupling was not completed, the two independent analyses establish important baseline information for the rotor design.
The transient thermal analysis established the temperature response of the rotor under the prescribed braking heat input.
The Static Structural analysis established the mechanical response of the rotor under the equivalent 228 N·m braking torque.

Together, these analyses provide two separate baseline datasets that can be used for future coupling and model refinement.

```text
                  CURRENT PROJECT
                        |
          +-------------+-------------+
          |                           |
          v                           v
  Transient Thermal           Static Structural
          |                           |
          v                           v
 Temperature Response          Mechanical Response
          |                           |
          +-------------+-------------+
                        |
                        v
              Future Coupling
                        |
                        v
             Thermo-Structural
                  Analysis
```

### 18.10 Planned Thermo-Structural Development
The next attempt at thermo-structural coupling should focus on establishing a reliable thermal-to-structural data-transfer workflow.
The intended sequence is:

1. Verify transient thermal solution
2. Verify temperature field
3. Transfer temperature field to Static Structural
4. Apply 228 N·m braking moment
5. Apply transferred thermal temperature field
6. Solve combined structural model
7. Evaluate thermal + mechanical stress
8. Evaluate total deformation
9. Compare mechanical-only and coupled results

The completed coupled model should eventually provide:
- Thermal deformation.
- Mechanical deformation.
- Total deformation.
- Thermal stress.
- Mechanical stress.
- Combined von-Mises stress.
- Principal stress.
- Temperature-dependent structural response.

### 18.11 Expected Thermo-Structural Outputs
Once the coupling is successfully established, the following outputs should be evaluated:

| Output | Purpose |
|---|---|
| Temperature | Determine thermal state of the rotor |
| Thermal strain | Evaluate expansion caused by temperature |
| Thermal deformation | Quantify temperature-induced deformation |
| Mechanical deformation | Evaluate deformation from braking torque |
| Total deformation | Combined thermal and mechanical deformation |
| Thermal stress | Evaluate stress caused by temperature gradients |
| von-Mises stress | Evaluate combined equivalent stress |
| Principal stress | Evaluate tensile and compressive stress states |
| Equivalent elastic strain | Evaluate combined elastic response |

The coupled results should then be compared against the standalone Static Structural baseline from Section 17.

### 18.12 Comparison Planned for Future Work
The future study should compare:

| Response | Static Structural Baseline | Thermo-Structural Model |
|---|---|---|
| Mechanical deformation | Available | To be determined |
| Thermal deformation | Not included | To be determined |
| Total deformation | Mechanical only | To be determined |
| Mechanical stress | Available | To be determined |
| Thermal stress | Not included | To be determined |
| Combined von-Mises stress | Not calculated | To be determined |
| Principal stress | Mechanical only | To be determined |
| Temperature-dependent behavior | Not included | To be determined |

This comparison will determine the extent to which thermal loading changes the structural response of the rotor.

### 18.13 Current Project Classification
The current project is classified as:
- Completed Baseline Thermal Analysis
- Completed Standalone Static Structural Analysis
- Thermo-Structural Coupling Under Development

The thermo-structural stage remains an identified future development rather than a completed simulation result. No thermo-structural stress or thermo-mechanical deformation values are claimed in the current project results.

### 18.14 Section Status
**Section 18 Status:** Thermo-Structural Coupling Not Yet Completed
The project currently has two completed baseline analyses:
- Transient Thermal Analysis → Completed Baseline
- Static Structural Analysis → Completed Baseline
- Thermo-Structural Coupling → Not Completed

The next stage is to establish a stable thermal-to-structural data-transfer workflow and then perform the combined thermo-mechanical analysis.

## 19. Key Results Summary
This section summarizes the principal analytical, thermal and structural results obtained during the development of the lightweight ventilated brake rotor.
The current project consists of a completed analytical design basis, a transient thermal baseline and a successfully completed standalone Static Structural baseline.
The thermo-structural coupling has not yet been completed and is therefore not included as a completed result.

### 19.1 Vehicle and Braking Design Basis
The severe braking condition used as the primary design case was:

| Parameter | Value |
|---|---:|
| Vehicle mass | 120 kg |
| Rider mass | 75 kg |
| Total mass | 195 kg |
| Initial speed | 80 km/h |
| Final speed | 0 km/h |
| Braking duration | 4 s |
| Wheel rolling radius | 0.30 m |
| Front brake distribution | 70% |
| Number of front rotors | 1 |

The corresponding vehicle kinetic energy was:
$$
E_k = \frac{1}{2}mv^2
$$
giving approximately: **48.15 kJ**

The calculated front-brake energy was approximately: **33.70 kJ**
Using the defined 90% rotor heat-partition assumption, the estimated rotor thermal energy was: **30.33 kJ**
The corresponding average rotor thermal power over the 4-second braking event was approximately: **7.58 kW**

### 19.2 Braking Torque and Mechanical Loading
The equivalent braking torque used as the structural design load was: **228 N·m**
The effective friction radius was approximately: **0.099 m**

The corresponding equivalent tangential braking force was:
$$
F_t = \frac{T}{r_{\mathrm{eff}}}
$$
giving approximately: **2303 N**
The equivalent force representation per friction face was approximately: **1152 N**
These calculations established the mechanical loading basis for the Static Structural analysis.

### 19.3 Rotor Geometry
The developed ventilated brake rotor uses the following primary geometric parameters:

| Geometry Parameter | Value |
|---|---:|
| Outer diameter | 240 mm |
| Friction track inner diameter | 150 mm |
| Central bore diameter | 70 mm |
| Mounting PCD | 100 mm |
| Number of mounting holes | 6 |
| Mounting hole diameter | 8 mm |
| Total rotor thickness | 12 mm |
| Top friction plate thickness | 3 mm |
| Bottom friction plate thickness | 3 mm |
| Ventilation gap | 6 mm |
| Number of ventilation vanes | 24 |
| Vane thickness | 2 mm |

The geometry was developed as a lightweight ventilated rotor configuration intended to provide both structural functionality and improved thermal management potential.

### 19.4 Thermal Loading Definition
The friction-surface heat flux was defined using a time-dependent braking profile.
The implemented ANSYS heat-flux table was:

| Time | Heat Flux |
|---:|---:|
| 0 s | 275,000 W/m² |
| 1 s | 206,250 W/m² |
| 4 s | 0 W/m² |
| 60 s | 0 W/m² |

The heat-flux profile represents the decreasing heat input during the 4-second braking event.
The thermal loading was applied to the defined rotor friction surfaces.
The theoretical average heat flux per friction face was approximately: **137,500 W/m²**
and the peak heat flux per face was: **275,000 W/m²**

### 19.5 Transient Thermal Results
The transient thermal baseline was evaluated over a 60-second simulation period.
The maximum rotor temperature reached approximately: **52°C** at approximately: **1.94 s**

Selected temperature-history results were:

| Time | Rotor Temperature |
|---:|---:|
| 0.1 s | 32.339°C |
| 0.2 s | 36.993°C |
| 0.437 s | 42.485°C |
| 0.937 s | 48.443°C |
| 1.437 s | 51.188°C |
| 1.937 s | ≈ 52°C |
| 2.437 s | 51.438°C |
| 2.937 s | 49.541°C |
| 3.437 s | 47.117°C |
| 4.013 s | 43.661°C |
| 5.392 s | 39.056°C |
| 6.392 s | 37.022°C |
| 8.392 s | 34.445°C |
| 10.392 s | 32.851°C |
| 20.392 s | 29.447°C |
| 30.392 s | 28.124°C |
| 40.392 s | 27.368°C |
| 50.392 s | 26.865°C |
| 60 s | 26.512°C |

The thermal contour results also showed:

| Simulation Time | Maximum Temperature |
|---:|---:|
| 10 s | 33.117°C |
| 30 s | 28.161°C |
| 60 s | 26.512°C |

The maximum value reported by the Total Heat Flux result was approximately: **2546.6 W/m²**
This value represents the resulting conductive heat-flow field in the ANSYS model and should not be confused with the prescribed friction-surface heat-flux boundary condition.

### 19.6 Thermal Response Interpretation
The transient thermal analysis shows a rapid temperature increase during the braking event followed by progressive cooling after the applied heat input decreases to zero.
The temperature reaches its maximum shortly after the beginning of the braking event and then decreases as the rotor continues to dissipate stored thermal energy.
The rotor reaches approximately 26.5°C by the end of the 60-second simulation under the implemented simplified thermal boundary conditions.

The thermal results therefore establish a useful baseline for future improvements involving:
- Internal ventilation.
- Radiation.
- CFD-derived convection.
- Rotor rotation.
- Detailed frictional heat generation.
- Brake-pad contact.
- More realistic heat partitioning.

### 19.7 Static Structural Results
The standalone Static Structural analysis was successfully solved using:
- Structural Steel.
- Six mounting-hole cylindrical faces with Fixed Support.
- 228 N·m braking moment.
- 9 mm nominal mesh size.
- 114,520 nodes.
- 75,119 elements.

The principal structural results were:

| Structural Result | Value |
|---|---:|
| Maximum total deformation | 9.1413 × 10⁻⁷ m |
| Maximum total deformation | 0.000914 mm |
| Maximum von-Mises stress | 3.135 MPa |
| Maximum principal stress | 1.915 MPa |
| Minimum principal stress | ≈ -2.545 MPa |
| Maximum equivalent elastic strain | ≈ 1.677 × 10⁻⁵ |

### 19.8 Structural Response Interpretation
The calculated maximum deformation of approximately **0.000914 mm** is very small relative to the 240 mm rotor diameter.
The maximum von-Mises stress of approximately **3.135 MPa** is also low for the current Structural Steel baseline.
The results indicate a low mechanical deformation response and a relatively stiff structural behavior under the defined 228 N·m braking torque.
However, the structural result is a baseline mechanical result only. Thermal expansion and thermally induced stress were not included.

### 19.9 Mesh Results
The structural mesh development included multiple computational iterations.

| Mesh Size | Nodes | Elements | Status |
|---|---:|---:|---|
| 5 mm | 274,776 | 182,590 | Exceeded computational limit |
| 8 mm | 130,742 | 85,990 | Exceeded 128k-node limit |
| 9 mm | 114,520 | 75,119 | Successfully solved |

The final 9 mm mesh was selected to remain within the ANSYS Student computational constraints.
A formal mesh-convergence study remains future work.

### 19.10 Overall Results Table
| Category | Key Result |
|---|---:|
| Total braking kinetic energy | ≈ 48.15 kJ |
| Front-brake energy | ≈ 33.70 kJ |
| Rotor thermal energy | ≈ 30.33 kJ |
| Average rotor thermal power | ≈ 7.58 kW |
| Equivalent braking torque | ≈ 228 N·m |
| Effective friction radius | ≈ 0.099 m |
| Equivalent tangential force | ≈ 2303 N |
| Peak prescribed heat flux | 275,000 W/m² |
| Peak rotor temperature | ≈ 52°C |
| Peak temperature time | ≈ 1.94 s |
| Temperature at 60 s | 26.512°C |
| Maximum Total Heat Flux result | 2546.6 W/m² |
| Structural mesh size | 9 mm |
| Structural nodes | 114,520 |
| Structural elements | 75,119 |
| Maximum structural deformation | 0.000914 mm |
| Maximum von-Mises stress | 3.135 MPa |
| Maximum principal stress | 1.915 MPa |
| Minimum principal stress | ≈ -2.545 MPa |
| Maximum equivalent elastic strain | ≈ 1.677 × 10⁻⁵ |

### 19.11 Current Analysis Status
The current analysis status can be summarized as:

```text
Analytical Braking Calculations
            ↓
         COMPLETED
            ↓
Rotor CAD Development
            ↓
         COMPLETED
            ↓
Transient Thermal Analysis
            ↓
   COMPLETED BASELINE
            ↓
Static Structural Analysis
            ↓
   COMPLETED BASELINE
            ↓
Thermo-Structural Coupling
            ↓
     NOT COMPLETED
            ↓
CFD Cooling Analysis
            ↓
      FUTURE WORK
            ↓
Design Optimization
            ↓
      FUTURE WORK
            ↓
Experimental Validation
            ↓
      FUTURE WORK
```

### 19.12 Important Result Classification
The results in this project are divided into three categories.

**Completed Analytical Results**
These include: Vehicle kinetic energy, Front-brake energy, Rotor thermal energy, Equivalent braking torque, Equivalent tangential braking force, Thermal heat-flux basis.

**Completed CAE Baseline Results**
These include: Transient thermal temperature response, Thermal cooling response, Static structural deformation, von-Mises stress, Principal stress, Equivalent elastic strain.

**Future Multiphysics Results**
These include: Thermally induced stress, Combined thermo-mechanical stress, Thermal deformation, Coupled total deformation, CFD-based cooling, Rotational airflow, Fatigue performance, Optimized rotor geometry, Experimental validation.

### 19.13 Key Finding
The current baseline analysis demonstrates that the proposed lightweight ventilated brake rotor can be evaluated through a structured CAE workflow combining analytical calculations, transient thermal analysis and static structural analysis.
The thermal baseline predicts a peak rotor temperature of approximately 52°C under the implemented simplified heat-input model.
The structural baseline predicts a maximum deformation of approximately 0.000914 mm and a maximum von-Mises stress of approximately 3.135 MPa under the calculated 228 N·m braking torque.
These results provide a quantitative baseline for continued development of the rotor design.
The next major technical step is to successfully establish the thermo-structural coupling, followed by more detailed cooling, fatigue and optimization studies.

## 20. Model Assumptions and Limitations
The current CAE investigation uses a set of engineering assumptions and model simplifications to make the brake rotor analysis computationally manageable while establishing a clear baseline for future multiphysics development.
The assumptions and limitations are divided into the analytical design basis, thermal model, structural model, computational model and overall validation.

### 20.1 Analytical Design Assumptions
The braking design case is based on the following assumptions:
- Vehicle mass is assumed to be **120 kg**.
- Rider mass is assumed to be **75 kg**.
- Combined vehicle and rider mass is therefore **195 kg**.
- Initial braking speed is **80 km/h**.
- Final speed is **0 km/h**.
- Braking duration is **4 seconds**.
- Wheel rolling radius is **0.30 m**.
- Front braking distribution is assumed to be **70%**.
- One front brake rotor is considered.
- **90%** of the calculated front-brake energy is assumed to be absorbed as rotor thermal energy.
- The effective friction radius is approximately **0.099 m**.
- The equivalent front braking torque is approximately **228 N·m**.

These assumptions define the baseline severe-braking design case used throughout the current analysis.

### 20.2 Thermal Model Assumptions
The transient thermal model uses a prescribed heat-flux approach to represent braking heat generation.
The implemented heat-flux profile is:

| Time | Heat Flux |
|---:|---:|
| 0 s | 275,000 W/m² |
| 1 s | 206,250 W/m² |
| 4 s | 0 W/m² |
| 60 s | 0 W/m² |

The following assumptions apply to the thermal model:
- Heat input is represented using a prescribed surface heat flux.
- The heat flux is applied to the defined friction surfaces.
- The heat input decreases during the 4-second braking event.
- Heat input is set to zero after the braking event.
- The implemented ANSYS thermal model uses an initial temperature of **22°C**.
- The implemented ANSYS thermal model uses an ambient temperature of **22°C**.
- The transient thermal analysis duration is **60 seconds**.
- External convection is represented using a simplified convection boundary condition.
- The current model does not explicitly model brake-pad contact.
- The current model does not explicitly model a moving frictional heat source.
- Rotor rotation is not explicitly represented in the thermal model.
- Internal ventilation surfaces were not included in the implemented thermal boundary conditions.
- Radiation was not included in the implemented baseline thermal model.
- A hub thermal sink was not included in the implemented baseline thermal model.
- CFD-derived heat-transfer coefficients were not used.
- Temperature-dependent contact behavior was not modeled.

The thermal model is therefore considered a **simplified transient thermal baseline**.

### 20.3 Thermal Boundary Condition Limitations
The prescribed heat-flux method provides a practical way to represent the braking heat input without explicitly modeling the complete brake-pad contact problem.
However, the method does not capture the complete physical behavior of an actual braking system.
In a real brake system, heat generation depends on factors such as:
Contact pressure, Friction coefficient, Relative sliding velocity, Rotor angular velocity, Pad geometry, Pad material, Heat partition between rotor and pads, Brake application history, Rotor cooling conditions.

These effects are not explicitly resolved in the current thermal baseline.
A future model should replace or refine the prescribed heat-flux approach using a more detailed frictional-contact and heat-generation model.

### 20.4 Thermal Cooling Limitations
The current thermal model uses simplified convection rather than a detailed fluid-flow solution.
The theoretical cooling model considered different convection regions, including external surfaces, internal cooling regions, outer edges and hub-related heat transfer.
However, the implemented baseline model did not include all of these mechanisms.
In particular:
- Internal ventilation-surface convection was not implemented.
- Radiation was not implemented.
- Hub thermal conduction/sink behavior was not implemented.
- Rotor-induced airflow was not explicitly modeled.
- CFD was not used to calculate local convective heat-transfer coefficients.

Therefore, the thermal result should be interpreted as a baseline numerical temperature response rather than a complete prediction of real-world rotor cooling performance.

### 20.5 Structural Model Assumptions
The Static Structural analysis uses the following assumptions:
- The rotor material is modeled as Structural Steel.
- The structural analysis is static.
- A braking moment of **228 N·m** is applied.
- The six mounting-hole cylindrical faces are treated as Fixed Supports.
- The applied moment acts about the rotor's central rotational axis.
- The structural model represents the mechanical loading condition independently of the thermal field.
- Linear elastic structural behavior is used as the baseline representation.
- Thermal expansion is not included.
- Thermally induced stress is not included.

The resulting deformation, stress and strain values therefore represent the **mechanical-only structural response**.

### 20.6 Structural Boundary Condition Limitations
The six mounting-hole cylindrical faces were fixed to represent the rotor attachment to the hub or wheel assembly.
This is a simplified representation of the actual mounting condition.
An actual brake rotor assembly may experience:
Bolt preload, Bolt-hole contact, Hub deformation, Wheel deformation, Contact between rotor and hub, Local compliance at mounting interfaces, Manufacturing tolerances, Assembly misalignment.

These effects are not included in the current Static Structural baseline.
Consequently, the fixed-support condition should not be interpreted as an exact representation of the complete rotor-hub assembly.

### 20.7 Mechanical Loading Limitations
The current structural model applies the calculated **228 N·m** braking moment directly.
The model does not explicitly represent:
Individual brake-pad forces, Brake-pad pressure distribution, Friction coefficient variation, Pad contact pressure, Sliding contact, Rotor angular velocity, Dynamic braking effects, Brake-system compliance.

The direct moment representation is therefore an equivalent mechanical loading approach.
It is appropriate for establishing the current structural baseline but should be replaced or supplemented with detailed contact loading in future work.

### 20.8 Mesh Limitations
The structural mesh was developed through several iterations.

| Element Size | Nodes | Elements | Result |
|---|---:|---:|---|
| 5 mm | 274,776 | 182,590 | Exceeded computational limit |
| 8 mm | 130,742 | 85,990 | Exceeded 128k-node limit |
| 9 mm | 114,520 | 75,119 | Successfully solved |

The final structural mesh uses a nominal element size of **9 mm**.
The mesh was selected partly because of the computational limitations of the ANSYS Student environment.
A formal mesh-convergence study has not yet been completed.
Therefore:
- The current structural results should be considered baseline numerical results.
- Local stress concentrations may require finer mesh refinement.
- Results near mounting holes and geometric transitions should be interpreted carefully.
- A finer mesh should be evaluated in future work where computational resources permit.

### 20.9 Thermo-Structural Coupling Limitation
The transient thermal and Static Structural analyses were developed as separate baseline analyses.
The thermal temperature field was not successfully transferred into the structural model.
Therefore, the current structural analysis does not include:
Thermal expansion, Thermal strain, Thermal stress, Combined thermal and mechanical stress, Combined thermal and mechanical deformation, Temperature-dependent structural properties.

The Static Structural results must therefore be reported as:
**Mechanical-only Static Structural results**
and not as thermo-structural results.

### 20.10 ANSYS Student Computational Limitations
The project was developed using the ANSYS Student environment.
Computational limitations influenced the simulation workflow.
The structural mesh exceeded the available computational capacity at 5 mm and 8 mm nominal element sizes, requiring the final 9 mm mesh.
The thermal workflow also experienced solver-related difficulties during later update attempts.
These computational constraints limited the ability to perform:
Extensive mesh refinement, Large-scale parameter studies, Multiple high-resolution transient simulations, Complete thermo-structural coupling, Detailed CFD simulations within the same workflow, Extensive optimization studies.
The current project therefore represents a computationally constrained engineering baseline.

### 20.11 Thermal Solver I/O Limitation
During a later attempt to update the transient thermal analysis, ANSYS reported an I/O-related solver failure:

```text
An error has occurred writing to file unit = 4
which may imply a full disk.
Random write error on file unit=4
possible full disk.
I/O status error = 22.
```

The H: drive was checked during troubleshooting and approximately 191 GB of 215 GB remained available.
The project scratch directory was approximately 360 MB.
Therefore, the failure was not conclusively attributed to insufficient physical disk capacity.
The exact root cause of the I/O failure was not established.
This issue is documented as a limitation of the current simulation workflow and remains an item for future troubleshooting.

### 20.12 Material Model Limitations
The current structural analysis uses Structural Steel as a baseline material.
The present model does not include a detailed temperature-dependent material database.
Consequently, the current structural results do not account for potential changes in:
Young's modulus, Yield strength, Thermal expansion coefficient, Thermal conductivity, Specific heat, Material strength with temperature.
A future thermo-structural model should use appropriate temperature-dependent material properties.

### 20.13 Fatigue Limitation
The current Static Structural analysis evaluates a single braking load case.
Fatigue behavior has not been evaluated.
The model does not currently account for:
Repeated braking cycles, Stress amplitude, Mean stress, Thermal cycling, Brake-cycle frequency, Fatigue strength, Crack initiation, Crack propagation.
A fatigue analysis should be performed in future work if long-term rotor durability is to be assessed.

### 20.14 Experimental Validation Limitation
No physical prototype or experimental brake dynamometer test has been used to validate the current numerical results.
Therefore, the current CAE results are numerical predictions based on the defined assumptions and boundary conditions.
Future experimental validation could compare simulation and experimental measurements for:
Rotor temperature, Cooling rate, Braking torque, Rotor deformation, Stress response, Brake performance.
Experimental validation would significantly improve confidence in the numerical model.

### 20.15 Overall Model Classification
The current project should be classified as:
**Baseline Engineering CAE Study**
with the following completed components:

```text
Analytical Braking Calculations
             ↓
        Completed
             ↓
Rotor CAD Development
             ↓
        Completed
             ↓
Transient Thermal Analysis
             ↓
   Completed Baseline
             ↓
Static Structural Analysis
             ↓
   Completed Baseline
```

The following components remain future development:

```text
Thermo-Structural Coupling
             ↓
        Not Completed
             ↓
CFD Cooling Analysis
             ↓
        Future Work
             ↓
Fatigue Analysis
             ↓
        Future Work
             ↓
Design Optimization
             ↓
        Future Work
             ↓
Experimental Validation
             ↓
        Future Work
```

### 20.16 Overall Limitation Statement
The current results provide a useful engineering baseline, but they should not be interpreted as a fully validated representation of an actual production brake rotor.
The major limitations are:
- Simplified prescribed thermal heat flux.
- No explicit brake-pad contact.
- No explicit rotor rotation.
- No internal CFD-based ventilation analysis.
- No radiation in the implemented thermal model.
- No hub thermal sink in the implemented thermal model.
- No temperature-dependent structural material properties.
- No thermal-to-structural temperature transfer.
- No thermo-structural stress calculation.
- Simplified fixed mounting conditions.
- Direct equivalent braking-moment loading.
- No bolt preload.
- No fatigue analysis.
- No formal mesh-convergence study.
- No experimental validation.
- Computational limitations associated with the ANSYS Student environment.

These limitations define the boundary of the current analysis and provide the basis for the future multiphysics development described in the following sections.

## 21. Future Multiphysics Development
The current project establishes separate transient thermal and Static Structural baselines. The next stage is to increase the physical fidelity of the model by developing a coupled multiphysics workflow.
The primary objective of future development is to evaluate the interaction between:
- Braking energy.
- Rotor temperature.
- Thermal expansion.
- Mechanical braking load.
- Thermally induced stress.
- Structural deformation.
- Ventilation and convective cooling.
- Rotor geometry.

The planned development path is:

```text
Braking Conditions
        ↓
Braking Energy and Torque
        ↓
Rotor Geometry
        ↓
Transient Thermal Analysis
        ↓
Temperature Field
        ↓
Thermo-Structural Analysis
        ↓
Thermal + Mechanical Stress
        ↓
CFD Cooling Analysis
        ↓
Improved Thermal Boundary Conditions
        ↓
Design Optimization
        ↓
Experimental Validation
```

### 21.1 Thermo-Structural Coupling
The highest-priority future development is to successfully transfer the transient temperature field from the thermal analysis into the Static Structural analysis.
The coupled model should include both:
- The calculated 228 N·m mechanical braking moment.
- The transient temperature field obtained from the thermal analysis.

The intended workflow is:

```text
Transient Thermal Analysis
          |
          | Temperature Field
          ↓
Static Structural Analysis
          |
          +---- 228 N·m Braking Moment
          |
          ↓
Thermo-Structural Solution
          |
          +---- Thermal Stress
          +---- Mechanical Stress
          +---- Combined Stress
          +---- Thermal Deformation
          +---- Mechanical Deformation
          +---- Total Deformation
```

The primary objective is to determine how the thermal field changes the structural response compared with the standalone Static Structural baseline.

### 21.2 Temperature-Dependent Material Properties
The current structural baseline uses Structural Steel without a detailed temperature-dependent material model.
A future thermo-structural analysis should incorporate appropriate temperature-dependent properties where required, including:
Young's modulus, Yield strength, Poisson's ratio, Thermal expansion coefficient, Thermal conductivity, Specific heat, Density.
This will allow the structural response to change appropriately with rotor temperature.

### 21.3 Detailed Brake-Pad Contact Model
The current thermal analysis uses a prescribed heat-flux boundary condition.
A future model can explicitly introduce brake-pad geometry and contact.
The detailed contact model can include:
Brake pad geometry, Rotor-pad contact, Contact pressure, Friction coefficient, Relative sliding velocity, Frictional heat generation, Heat partition between rotor and brake pad, Contact pressure distribution.
The frictional heat generation can then be evaluated from the actual contact conditions rather than being represented only by a prescribed surface heat flux.

### 21.4 Moving Heat Source
A more advanced thermal model should account for the movement of the frictional contact region relative to the rotor.
The current baseline applies heat to the defined friction surfaces without explicitly modeling a moving heat source.
Future development can investigate:
Rotational motion, Sliding velocity, Time-dependent frictional heating, Circumferential heat distribution, Local thermal gradients, Repeated pad-track interaction.
This would provide a more physically representative temperature distribution.

### 21.5 Rotor Rotation
The current baseline thermal model does not explicitly model rotor rotation.
Future simulations can incorporate rotor rotational speed and investigate its influence on:
Air movement, Convective cooling, Heat transfer, Temperature distribution, Ventilation performance.
Rotor speed should be linked to vehicle speed and wheel rolling radius where appropriate.

### 21.6 CFD-Based Cooling Analysis
A major future development is CFD analysis of the ventilated rotor.
The objective is to determine the actual airflow and heat-transfer behavior through and around the ventilation geometry.
The CFD model can evaluate:
Air velocity, Pressure distribution, Mass-flow rate, Airflow through ventilation passages, Rotor-induced airflow, Convective heat transfer, Local heat-transfer coefficients, Temperature distribution, Cooling effectiveness.
The CFD results can subsequently be used to improve the convection boundary conditions in the transient thermal model.

### 21.7 Ventilation Passage Analysis
The 24-vane ventilated rotor provides an opportunity to investigate internal airflow behavior.
Future CFD studies can examine:
Air entry into the ventilation passages, Air acceleration through the passages, Pressure losses, Flow separation, Recirculation, Vane pumping behavior, Air exit conditions, Effect of vane geometry on cooling.
Different ventilation geometries can then be compared based on both thermal performance and structural requirements.

### 21.8 Radiation Heat Transfer
Radiation was not included in the implemented baseline thermal model.
A future thermal model can include surface-to-ambient radiation to provide a more complete representation of heat rejection from the rotor.
The analysis can investigate the contribution of radiation relative to convection, particularly at higher rotor temperatures.

### 21.9 Hub and Mounting Thermal Interaction
The current thermal model does not include a detailed thermal connection between the rotor and hub.
Future development can model:
Rotor-hub contact, Thermal conduction through the hub, Hub temperature, Heat transfer into adjacent components, Thermal resistance at mounting interfaces.
This would improve the representation of the complete rotor assembly.

### 21.10 Improved Convection Modeling
The current thermal model uses simplified convection boundary conditions.
Future work can replace these simplified values with convection coefficients obtained from CFD.
The workflow would be:

```text
Rotor Geometry
      ↓
CFD Analysis
      ↓
Airflow and Heat Transfer
      ↓
Local / Average Convection Coefficients
      ↓
Transient Thermal Model
      ↓
Improved Temperature Field
```

This approach would make the thermal boundary conditions more representative of the ventilated rotor's actual operating environment.

### 21.11 Thermal Cycling Analysis
The current thermal analysis considers a single severe braking event.
Future work can investigate repeated braking cycles.
A thermal-cycle study could evaluate:
Repeated braking, Heating and cooling cycles, Maximum temperature over multiple cycles, Temperature accumulation, Cooling between braking events, Thermal gradients, Thermal fatigue risk.

A representative sequence could be:

```text
Braking Event
      ↓
Heating
      ↓
Cooling
      ↓
Second Braking Event
      ↓
Heating
      ↓
Cooling
      ↓
Repeated Cycle
```

This would provide a more realistic assessment of rotor thermal behavior during repeated braking.

### 21.12 Fatigue and Durability Analysis
After the thermo-structural model is established, fatigue analysis can be performed.
Future fatigue studies can consider:
Repeated braking loads, Mechanical stress cycles, Thermal stress cycles, Combined thermo-mechanical loading, Mean stress, Stress amplitude, Fatigue life, Crack-initiation risk.
The fatigue analysis should use the temperature-dependent stress history obtained from the coupled simulation where possible.

### 21.13 Mesh-Convergence Development
The current structural mesh was selected within the ANSYS Student computational limitations.
Future work should perform a formal mesh-convergence study.
The study should evaluate whether the following quantities stabilize with increasing mesh density:
Maximum deformation, Maximum von-Mises stress, Principal stress, Equivalent elastic strain, Temperature distribution.

A refined mesh should receive particular attention around:
Mounting holes, Vane-root regions, Friction-track transitions, Geometric fillets, Thickness transitions, Other locations showing high stress gradients.

### 21.14 Multiphysics Simulation Workflow
The long-term multiphysics workflow is:

```text
                  Vehicle Operating Condition
                            ↓
                    Braking Parameters
                            ↓
              +-------------+-------------+
              |                           |
              ↓                           ↓
       Braking Energy                Braking Torque
              |                           |
              ↓                           ↓
      Thermal Loading            Mechanical Loading
              |                           |
              ↓                           ↓
      Transient Thermal           Static Structural
              |                           |
              ↓                           |
       Temperature Field                |
              |                           |
              +-------------+-------------+
                            ↓
                  Thermo-Structural Model
                            ↓
              +-------------+-------------+
              |                           |
              ↓                           ↓
       Thermal Stress              Total Deformation
              |                           |
              +-------------+-------------+
                            ↓
                       CFD Analysis
                            ↓
                    Cooling Performance
                            ↓
                    Design Optimization
                            ↓
                 Experimental Validation
```

### 21.15 Planned Multiphysics Outputs
The future multiphysics model should provide quantitative results for:

| Analysis | Planned Outputs |
|---|---|
| Transient Thermal | Temperature, heat flux, cooling rate |
| Static Structural | Stress, strain, deformation |
| Thermo-Structural | Thermal stress, combined stress, total deformation |
| CFD | Velocity, pressure, airflow, heat transfer |
| Thermal-Fluid Coupling | Improved cooling prediction |
| Fatigue | Fatigue life and durability |
| Optimization | Mass, thermal and structural performance |

### 21.16 Future Development Priority
The recommended development sequence is:
- **Priority 1 - Thermo-Structural Coupling:** Successfully transfer the transient temperature field into the structural model and evaluate combined thermal and mechanical loading.
- **Priority 2 - Thermal Model Improvement:** Improve the thermal model through more realistic cooling conditions, radiation, hub interaction and temperature-dependent properties.
- **Priority 3 - CFD Ventilation Analysis:** Model airflow through the 24-vane ventilation system and determine realistic convective heat-transfer behavior.
- **Priority 4 - Detailed Contact Modeling:** Introduce brake-pad contact and frictional heat generation.
- **Priority 5 - Thermal Cycling and Fatigue:** Evaluate repeated braking and long-term structural durability.
- **Priority 6 - Design Optimization:** Optimize rotor geometry using thermal, structural and mass constraints.
- **Priority 7 - Experimental Validation:** Compare numerical predictions with physical measurements.

### 21.17 Final Future-Development Objective
The ultimate objective is to progress from the current baseline model:

```text
Analytical Calculations
        ↓
CAD
        ↓
Transient Thermal
        ↓
Static Structural
```

toward a higher-fidelity engineering workflow:

```text
Braking Conditions
        ↓
Rotor Design
        ↓
Brake-Pad Contact
        ↓
Frictional Heat Generation
        ↓
Transient Thermal
        ↓
CFD Cooling
        ↓
Thermo-Structural Analysis
        ↓
Fatigue / Durability
        ↓
Design Optimization
        ↓
Experimental Validation
```

This staged development approach allows each additional physics domain to be verified against the existing baseline before moving toward a more computationally demanding fully coupled simulation.

### 21.18 Future Multiphysics Development Status

| Development Stage | Current Status |
|---|---|
| Analytical braking calculations | Completed |
| Rotor CAD development | Completed |
| Transient thermal baseline | Completed |
| Static structural baseline | Completed |
| Thermo-structural coupling | Future development |
| Temperature-dependent material model | Future development |
| Brake-pad contact | Future development |
| Frictional heat generation | Future development |
| Rotor rotation | Future development |
| CFD cooling analysis | Future development |
| Radiation | Future development |
| Thermal cycling | Future development |
| Fatigue analysis | Future development |
| Design optimization | Future development |
| Experimental validation | Future development |

The future multiphysics work will build directly on the completed thermal and structural baseline analyses documented in this repository.

## 22. Design Optimization Opportunities
The current brake rotor design provides a baseline geometry and a baseline thermal and structural response. The next stage of development is to investigate how the rotor geometry can be optimized to reduce unnecessary mass while maintaining adequate thermal performance, structural stiffness and braking capability.
The optimization stage should be performed only after establishing a stable and sufficiently validated thermo-structural and cooling model.

### 22.1 Optimization Objectives
The primary design objectives are:
- Reduce rotor mass.
- Maintain sufficient structural stiffness.
- Maintain acceptable stress levels.
- Reduce peak rotor temperature.
- Improve cooling performance.
- Improve temperature uniformity.
- Maintain the required braking torque capacity.
- Maintain the required mounting and packaging geometry.
- Preserve manufacturability.

The optimization should therefore be treated as a **multi-objective engineering problem** rather than a simple mass-minimization problem.

### 22.2 Current Baseline Design
The current rotor provides the reference design against which future optimized configurations can be compared.

| Parameter | Current Baseline |
|---|---:|
| Rotor outer diameter | 240 mm |
| Friction track inner diameter | 150 mm |
| Central bore diameter | 70 mm |
| Mounting PCD | 100 mm |
| Mounting holes | 6 × 8 mm |
| Total thickness | 12 mm |
| Top friction plate | 3 mm |
| Bottom friction plate | 3 mm |
| Ventilation gap | 6 mm |
| Number of vanes | 24 |
| Vane thickness | 2 mm |
| Applied braking moment | 228 N·m |
| Structural mesh size | 9 mm |
| Maximum deformation | 0.000914 mm |
| Maximum von-Mises stress | 3.135 MPa |
| Peak thermal temperature | ≈ 52°C |

These values can serve as the baseline reference for future design iterations.

### 22.3 Potential Design Variables
The following geometric parameters can be investigated as optimization variables:
Rotor plate thickness, Friction-track width, Ventilation-gap thickness, Vane thickness, Vane count, Vane orientation, Vane profile, Vane height, Vane curvature, Hub diameter, Mounting-region geometry, Mounting-hole geometry, Fillet dimensions, Material selection.
Each design variable should be varied within practical engineering and manufacturing limits.

### 22.4 Rotor Thickness Optimization
Reducing the friction-plate thickness can significantly reduce rotor mass.
However, excessive thickness reduction may negatively affect:
Structural stiffness, Thermal capacity, Heat distribution, Wear allowance, Local stress levels, Thermal gradients.
A future parametric study can therefore evaluate several friction-plate thicknesses and compare:

```text
Plate Thickness
       ↓
Mass
       ↓
Temperature
       ↓
Stress
       ↓
Deformation
```

The optimum thickness should provide an appropriate balance between mass, thermal capacity and structural stiffness.

### 22.5 Ventilation-Gap Optimization
The current rotor uses a 6 mm ventilation gap.
The ventilation gap can be investigated to determine its effect on:
Airflow, Cooling rate, Rotor mass, Structural stiffness, Internal pressure loss, Temperature distribution.
Increasing the ventilation gap may improve airflow but can also affect structural stiffness and overall geometry.
Therefore, the optimum gap should be determined using coupled thermal, structural and CFD analysis.

### 22.6 Vane-Count Optimization
The current rotor contains 24 ventilation vanes.
The number of vanes can be varied to investigate the relationship between:
Airflow, Cooling performance, Pressure loss, Rotor mass, Structural stiffness, Manufacturing complexity.
Potential configurations can be compared using CFD and thermal simulation.
The objective is not necessarily to maximize the number of vanes, but to identify an effective vane count that provides adequate cooling without unnecessary mass or flow restriction.

### 22.7 Vane-Thickness Optimization
The current vane thickness is: **2 mm**
Reducing vane thickness can reduce mass, while increasing vane thickness may improve structural stiffness and durability.
The optimization should therefore evaluate the relationship between:

```text
Vane Thickness
      ↓
Rotor Mass
      ↓
Airflow
      ↓
Cooling
      ↓
Structural Stiffness
```

The final value should satisfy both thermal and structural requirements.

### 22.8 Vane-Geometry Optimization
The geometry of the ventilation vanes can have a significant influence on airflow and heat transfer.
Future studies can investigate:
Straight vanes, Curved vanes, Radial vanes, Swept vanes, Different vane angles, Different vane profiles, Different inlet and outlet geometries.
CFD can be used to determine how each geometry affects airflow and heat transfer.
The resulting CFD data can then be incorporated into the thermal analysis.

### 22.9 Friction-Track Optimization
The friction-track region can also be optimized.
Potential variables include:
Friction-track width, Inner track diameter, Outer track diameter, Friction-surface area, Plate thickness, Transition geometry.
The friction track must maintain adequate braking capability while avoiding unnecessary material.
Optimization should also consider the distribution of thermal loading across the friction region.

### 22.10 Hub and Mounting-Region Optimization
The central hub and mounting region can be optimized for mass reduction while maintaining sufficient structural stiffness.
Potential modifications include:
Hub thickness reduction, Hub diameter optimization, Mounting-web geometry, Fillet optimization, Material removal from low-stress regions.
Special attention should be given to the mounting holes because they are the primary structural constraint locations in the current Static Structural model.

### 22.11 Fillet and Stress-Concentration Optimization
Geometric transitions can produce local stress concentrations.
Future optimization can investigate:
Fillet radius, Vane-root transitions, Hub-to-plate transitions, Mounting-hole transitions, Friction-track transitions.
Increasing an appropriate fillet radius may reduce local stress concentration while maintaining the required geometry.
These regions should be evaluated using a locally refined mesh because the current 9 mm baseline mesh may not adequately resolve small geometric stress concentrations.

### 22.12 Mass Optimization
One of the major objectives of the project is lightweight rotor development.
The optimization target can be expressed as: minimize M_rotor
subject to structural and thermal constraints.
Potential constraints include:
σ_max ≤ σ_allowable
δ_max ≤ δ_allowable
and:
T_max ≤ T_allowable
where:
M_rotor = rotor mass.
σ_max = maximum stress.
δ_max = maximum deformation.
T_max = maximum rotor temperature.
The allowable limits must be established from appropriate material, braking-system and design requirements before a final optimization is performed.

### 22.13 Thermal Optimization
The rotor should also be optimized for thermal performance.
Potential thermal objectives include:
Minimize peak temperature, Maximize cooling rate, Improve temperature uniformity, Reduce thermal gradients, Improve convective heat transfer, Improve airflow through the ventilation passages.
A conceptual thermal objective is: minimize T_max
while maintaining structural and geometric requirements.

### 22.14 Structural Optimization
Structural optimization can target:
Minimum deformation, Reduced stress concentration, Adequate stiffness, Improved load distribution, Reduced mass.
A conceptual structural objective is: minimize δ_max
subject to stress and mass constraints.
The final objective function should be defined only after the thermo-structural model is established.

### 22.15 Multi-Objective Optimization
The final rotor design should balance several competing objectives.
A conceptual optimization problem can be represented as:
**Minimize:**
Rotor Mass, Peak Temperature, Maximum Stress, Maximum Deformation
**Maximize:**
Cooling Rate, Structural Stiffness, Thermal Performance
**Subject To:**
Required Braking Torque, Thermal Constraints, Structural Constraints, Geometric Constraints, Manufacturing Constraints.

The optimized design should not simply be the lightest possible rotor.
It should provide an appropriate balance between: Mass + Thermal Performance + Structural Performance + Manufacturability.

### 22.16 Parametric Study Approach
Before performing automated optimization, a structured parametric study should be conducted.
The recommended approach is:

```text
Baseline Rotor
      ↓
Select Design Variable
      ↓
Generate Design Variations
      ↓
Run Thermal Analysis
      ↓
Run Structural Analysis
      ↓
Compare Results
      ↓
Identify Promising Designs
      ↓
Refine Geometry
      ↓
Run Coupled Analysis
      ↓
Select Candidate Optimum
```

For example, the following variables could be investigated:

| Design Variable | Baseline | Future Study |
|---|---|---|
| Total rotor thickness | 12 mm | Parametric |
| Plate thickness | 3 mm | Parametric |
| Ventilation gap | 6 mm | Parametric |
| Vane count | 24 | Parametric |
| Vane thickness | 2 mm | Parametric |
| Vane angle | Baseline geometry | Parametric |
| Fillet radius | Baseline geometry | Parametric |
| Hub geometry | Baseline geometry | Parametric |

The exact parameter ranges should be defined after considering manufacturing, packaging and structural requirements.

### 22.17 Design Comparison Metrics
Each candidate design should be evaluated using consistent metrics.

| Metric | Purpose |
|---|---|
| Rotor mass | Lightweight design evaluation |
| Peak temperature | Thermal performance |
| Cooling rate | Heat rejection performance |
| Temperature uniformity | Thermal stability |
| Maximum von-Mises stress | Structural performance |
| Principal stress | Local tensile/compressive response |
| Total deformation | Structural stiffness |
| Equivalent elastic strain | Elastic response |
| Pressure drop | CFD ventilation efficiency |
| Airflow rate | Cooling performance |
| Manufacturing complexity | Practical feasibility |

This allows different rotor configurations to be compared using a common engineering basis.

### 22.18 Optimization Workflow with CFD
Once the CFD model is established, the optimization workflow can be expanded:

```text
Parametric Rotor Geometry
          ↓
          CFD
          ↓
Airflow / Pressure / Heat Transfer
          ↓
Transient Thermal
          ↓
Temperature Field
          ↓
Thermo-Structural Analysis
          ↓
Stress / Deformation
          ↓
Performance Evaluation
          ↓
Optimization Algorithm
          ↓
New Geometry
          ↓
Repeat
```

This iterative process can identify geometries that improve cooling while maintaining structural performance.

### 22.19 Optimization Constraints
Future optimization should respect practical engineering constraints.
These may include:
Required rotor diameter, Wheel packaging limitations, Mounting-hole locations, Minimum manufacturable wall thickness, Minimum vane thickness, Required friction-track area, Required braking torque, Structural stress limits, Deformation limits, Maximum operating temperature, Manufacturing method, Material availability, Rotor durability requirements.
The final optimized geometry should therefore be both numerically effective and physically manufacturable.

### 22.20 Optimization and ANSYS Student Limitations
Large-scale automated optimization may be computationally expensive within the ANSYS Student environment.
The current project has already demonstrated computational limitations during mesh development.
Therefore, future optimization may initially use:
Reduced-order models, Coarser screening simulations, Parametric studies, Selected design points, Sequential optimization, Reduced CFD domains where appropriate.
Higher-resolution optimization can be performed later when greater computational resources are available.

### 22.21 Recommended Optimization Sequence
The recommended order of optimization is:
- **Stage 1 - Baseline Verification:** Verify the current thermal and structural baseline.
- **Stage 2 - Geometric Parametric Study:** Investigate thickness, vane count, vane thickness, ventilation gap and related variables.
- **Stage 3 - Thermal Optimization:** Identify geometries with improved cooling performance.
- **Stage 4 - Structural Optimization:** Evaluate stress, deformation and stiffness of the thermally improved designs.
- **Stage 5 - Thermo-Structural Evaluation:** Evaluate combined thermal and mechanical loading.
- **Stage 6 - CFD Optimization:** Use CFD to refine ventilation geometry and cooling performance.
- **Stage 7 - Multi-Objective Optimization:** Balance mass, thermal performance and structural performance.
- **Stage 8 - Final Candidate Design:** Select the best-performing manufacturable geometry.
- **Stage 9 - Experimental Validation:** Validate the final candidate using physical testing.

### 22.22 Expected Optimization Outcome
The expected outcome of the optimization stage is a rotor design that:
Meets the required braking torque, Maintains acceptable structural stress, Maintains acceptable deformation, Provides effective thermal management, Improves ventilation performance, Minimizes unnecessary material, Remains manufacturable, Provides improved overall performance compared with the baseline design.
The optimized design should ultimately be evaluated against the current baseline using the same analytical and CAE methodology.

### 22.23 Optimization Status

| Optimization Activity | Status |
|---|---|
| Baseline geometry | Completed |
| Baseline thermal analysis | Completed |
| Baseline Static Structural analysis | Completed |
| Parametric geometry study | Future work |
| Thermo-structural optimization | Future work |
| CFD ventilation optimization | Future work |
| Mass optimization | Future work |
| Multi-objective optimization | Future work |
| Fatigue-constrained optimization | Future work |
| Experimental validation | Future work |

The current rotor geometry therefore serves as the baseline design configuration for future parametric, multiphysics and optimization studies.

## 23. Project Status
The project has progressed from the initial engineering definition and analytical calculations through CAD development, transient thermal simulation and standalone Static Structural analysis.
The current project status is summarized below.

### 23.1 Overall Project Status
| Project Stage | Status |
|---|---|
| Engineering problem definition | Completed |
| Vehicle and rider mass definition | Completed |
| Severe braking condition definition | Completed |
| Braking energy calculation | Completed |
| Front-brake energy calculation | Completed |
| Rotor thermal-energy calculation | Completed |
| Equivalent braking torque calculation | Completed |
| Equivalent tangential-force calculation | Completed |
| Brake rotor geometry development | Completed |
| Ventilated rotor geometry development | Completed |
| SpaceClaim CAD development | Completed |
| Transient thermal model setup | Completed |
| Thermal heat-flux definition | Completed |
| Thermal convection definition | Completed |
| Transient thermal analysis | Completed baseline |
| Thermal result extraction | Completed |
| Static Structural model setup | Completed |
| Structural material assignment | Completed |
| Structural mesh development | Completed |
| Structural boundary conditions | Completed |
| 228 N·m braking moment | Completed |
| Static Structural solution | Completed successfully |
| Structural result evaluation | Completed |
| Thermo-structural coupling | Not completed |
| CFD cooling analysis | Future work |
| Detailed brake-pad contact | Future work |
| Fatigue analysis | Future work |
| Design optimization | Future work |
| Experimental validation | Future work |

### 23.2 Completed Engineering Work
The following engineering stages have been completed:

**Analytical Design**
- [x] Vehicle mass defined.
- [x] Rider mass defined.
- [x] Combined system mass calculated.
- [x] Severe braking condition defined.
- [x] Vehicle kinetic energy calculated.
- [x] Front-brake energy calculated.
- [x] Rotor thermal-energy input calculated.
- [x] Equivalent braking torque calculated.
- [x] Effective friction radius determined.
- [x] Equivalent tangential braking force calculated.

**CAD Development**
- [x] Brake rotor concept developed.
- [x] Lightweight geometry developed.
- [x] Ventilation concept incorporated.
- [x] Rotor friction surfaces defined.
- [x] Central bore created.
- [x] Six mounting holes created.
- [x] Ventilation vanes created.
- [x] Geometry prepared in SpaceClaim.
- [x] Geometry prepared for ANSYS Mechanical analysis.

**Transient Thermal Analysis**
- [x] Transient thermal system created.
- [x] Material assigned.
- [x] Thermal mesh developed.
- [x] Friction-surface heat flux defined.
- [x] Time-dependent heat-flux table implemented.
- [x] Convection boundary condition implemented.
- [x] 60-second transient analysis performed.
- [x] Temperature history extracted.
- [x] Thermal contour results evaluated.
- [x] Peak temperature identified.
The baseline thermal analysis produced a peak rotor temperature of approximately **52°C at approximately 1.94 s**.

**Static Structural Analysis**
- [x] Static Structural system created.
- [x] Structural Steel assigned.
- [x] Structural mesh developed.
- [x] Final 9 mm mesh selected.
- [x] 114,520 nodes obtained.
- [x] 75,119 elements obtained.
- [x] Six mounting-hole cylindrical faces fixed.
- [x] 228 N·m braking moment applied.
- [x] Static structural solution completed.
- [x] Total Deformation evaluated.
- [x] Equivalent von-Mises Stress evaluated.
- [x] Maximum Principal Stress evaluated.
- [x] Minimum Principal Stress evaluated.
- [x] Equivalent Elastic Strain evaluated.

### 23.3 Current Thermal Analysis Status
**Status: Completed Baseline**
The transient thermal model produced usable baseline results.
Key thermal results:

| Result | Value |
|---|---:|
| Peak rotor temperature | ≈ 52°C |
| Approximate peak temperature time | ≈ 1.94 s |
| Temperature at 10 s | 33.117°C |
| Temperature at 30 s | 28.161°C |
| Temperature at 60 s | 26.512°C |
| Maximum Total Heat Flux result | 2546.6 W/m² |
| Simulation duration | 60 s |

A later attempt to update the thermal system encountered an ANSYS solver I/O failure.
The failure was documented and investigated, but the exact root cause was not conclusively established.
Therefore, the successful baseline thermal results remain the reference thermal results for the current project.

### 23.4 Current Static Structural Status
**Status: Completed Successfully**
The Static Structural baseline was successfully solved using the final 9 mm mesh.
Key structural results:

| Result | Value |
|---|---:|
| Applied braking moment | 228 N·m |
| Nodes | 114,520 |
| Elements | 75,119 |
| Maximum total deformation | 0.000914 mm |
| Maximum von-Mises stress | 3.135 MPa |
| Maximum principal stress | 1.915 MPa |
| Minimum principal stress | ≈ -2.545 MPa |
| Maximum equivalent elastic strain | ≈ 1.677 × 10⁻⁵ |

These results represent the **mechanical-only Static Structural baseline**.

### 23.5 Thermo-Structural Status
**Status: Not Completed**
The transient thermal temperature field was not successfully transferred into the Static Structural analysis.
Therefore, the following results have not yet been calculated:
Thermal expansion, Thermal strain, Thermal stress, Combined thermal and mechanical stress, Combined thermo-mechanical deformation, Temperature-dependent structural response.
The current structural results must therefore remain classified as **standalone Static Structural results**.

### 23.6 CFD Status
**Status: Future Work**
A detailed CFD analysis of the ventilated rotor has not yet been completed.
Future CFD work will investigate:
Airflow through the ventilation passages, Rotor-induced airflow, Air velocity, Pressure distribution, Mass-flow rate, Convective heat transfer, Local heat-transfer coefficients, Cooling effectiveness.
The CFD results can subsequently be used to improve the thermal boundary conditions.

### 23.7 Contact Modeling Status
**Status: Future Work**
The current model does not explicitly include brake-pad geometry or rotor-pad contact.
Future development can include:
Brake-pad geometry, Contact pressure, Friction coefficient, Sliding velocity, Frictional heat generation, Heat partition between rotor and brake pads.
This would provide a more physically representative representation of braking heat generation.

### 23.8 Fatigue Analysis Status
**Status: Future Work**
The current project does not include fatigue or durability analysis.
Future fatigue analysis can evaluate:
Repeated braking cycles, Mechanical stress cycles, Thermal stress cycles, Combined thermo-mechanical cycles, Fatigue life, Crack-initiation risk, Long-term durability.

### 23.9 Optimization Status
**Status: Future Work**
The current rotor geometry serves as the baseline design for future optimization.
Potential optimization variables include:
Rotor thickness, Friction-track width, Ventilation gap, Vane count, Vane thickness, Vane angle, Vane geometry, Fillet radius, Hub geometry, Mounting-region geometry.
The optimization objective will be to balance:
**Low Mass + Thermal Performance + Structural Performance + Manufacturability**

### 23.10 Experimental Validation Status
**Status: Future Work**
No physical prototype or experimental brake dynamometer validation has yet been completed.
Future validation should compare simulation results against measured values such as:
Rotor temperature, Cooling rate, Braking torque, Rotor deformation, Stress response, Brake performance.
Experimental validation will be required before treating the numerical model as a fully validated engineering representation.

### 23.11 Current Project Classification
The current project is best classified as:
> **Baseline Thermal and Static Structural CAE Analysis of a Lightweight Ventilated Brake Rotor**

The project currently contains:

```text
Analytical Design Calculations
             ↓
          COMPLETED
             ↓
Rotor CAD Development
             ↓
          COMPLETED
             ↓
Transient Thermal Analysis
             ↓
   COMPLETED BASELINE
             ↓
Static Structural Analysis
             ↓
   COMPLETED SUCCESSFULLY
             ↓
Thermo-Structural Coupling
             ↓
     NOT COMPLETED
             ↓
CFD Cooling Analysis
             ↓
       FUTURE WORK
             ↓
Fatigue Analysis
             ↓
       FUTURE WORK
             ↓
Design Optimization
             ↓
       FUTURE WORK
             ↓
Experimental Validation
             ↓
       FUTURE WORK
```

### 23.12 Final Current-State Summary
The project has successfully progressed through the core baseline engineering workflow:
Engineering Requirements → Analytical Calculations → CAD → Transient Thermal Analysis → Static Structural Analysis
The current completed CAE results establish:
A transient thermal baseline, A mechanical Static Structural baseline, A quantitative braking load basis, A quantitative temperature response, A quantitative stress response, A quantitative deformation response.
The major remaining technical step is the successful completion of the thermo-structural coupling.
After that, the project can progress toward:
CFD Cooling → Detailed Contact → Fatigue → Design Optimization → Experimental Validation

### 23.13 Project Status at a Glance
| Category | Current Status |
|---|---|
| Engineering calculations | Completed |
| Rotor CAD | Completed |
| Transient thermal baseline | Completed |
| Static structural baseline | Completed |
| Thermo-structural coupling | Not completed |
| CFD cooling | Future work |
| Detailed brake contact | Future work |
| Fatigue | Future work |
| Optimization | Future work |
| Experimental validation | Future work |

## 24. Conclusion
This project presents the design and baseline CAE investigation of a **lightweight ventilated brake rotor for electric-vehicle applications**.
The study followed a structured engineering workflow beginning with the definition of a severe braking condition and progressing through analytical calculations, CAD development, transient thermal analysis and Static Structural analysis.
The defined braking case considered a combined vehicle and rider mass of **195 kg**, with the vehicle decelerating from **80 km/h to 0 km/h in 4 seconds**.
From the analytical calculations, the total vehicle kinetic energy was approximately: **48.15 kJ**
The estimated front-brake energy was approximately: **33.70 kJ**
Using the defined rotor heat-partition assumption, the estimated rotor thermal energy was approximately: **30.33 kJ**
The corresponding average rotor thermal power during the 4-second braking event was approximately: **7.58 kW**
The equivalent braking torque used for the structural analysis was: **228 N·m**

### 24.1 Thermal Analysis Conclusion
The transient thermal analysis established a baseline temperature response for the rotor under the prescribed braking heat input.
The maximum rotor temperature obtained was approximately: **52°C at approximately 1.94 seconds**
After the braking event, the rotor progressively cooled under the implemented thermal boundary conditions.
The calculated temperatures at selected times were:

| Time | Maximum Rotor Temperature |
|---:|---:|
| ≈ 1.94 s | ≈ 52°C |
| 10 s | 33.117°C |
| 30 s | 28.161°C |
| 60 s | 26.512°C |

The thermal results demonstrate the baseline transient temperature behavior of the proposed rotor under the defined severe-braking condition.
However, the thermal model uses a simplified prescribed heat-flux approach and simplified convection. Internal ventilation-surface convection, radiation, rotor rotation, CFD-derived airflow and explicit brake-pad contact were not included in the implemented baseline model.
Therefore, the thermal results should be regarded as a **baseline transient thermal prediction**, rather than a fully validated real-world cooling prediction.

### 24.2 Static Structural Analysis Conclusion
The Static Structural analysis was successfully completed using a **9 mm nominal mesh** containing:
- **114,520 nodes**
- **75,119 elements**

The rotor was constrained at the six mounting-hole cylindrical faces and subjected to the calculated **228 N·m braking moment**.
The resulting structural response was:

| Structural Result | Value |
|---|---:|
| Maximum total deformation | 0.000914 mm |
| Maximum von-Mises stress | 3.135 MPa |
| Maximum principal stress | 1.915 MPa |
| Minimum principal stress | ≈ -2.545 MPa |
| Maximum equivalent elastic strain | ≈ 1.677 × 10⁻⁵ |

The very small calculated deformation indicates a low mechanical deformation response under the defined braking torque and boundary conditions.
The calculated von-Mises stress also provides a useful baseline for evaluating future geometry modifications and optimization studies.
These structural results are **mechanical-only results**.

### 24.3 Thermo-Structural Conclusion
A fully coupled thermo-structural analysis was not completed during the current project stage.
The transient thermal temperature field was not successfully transferred into the Static Structural model.
Consequently, the current project does not yet provide numerical results for:
Thermal expansion, Thermal strain, Thermally induced stress, Combined thermo-mechanical stress, Combined thermal and mechanical deformation, Temperature-dependent structural response.
The Static Structural results must therefore remain classified as a **standalone mechanical baseline**.
This distinction is important when interpreting and reporting the current results.

### 24.4 Engineering Significance
The completed baseline analyses establish a quantitative foundation for further development of the ventilated brake rotor.
The current results provide:
A defined severe-braking load case, A calculated braking-energy basis, A calculated braking-torque basis, A defined transient thermal loading condition, A baseline rotor temperature response, A baseline structural stress response, A baseline deformation response, A starting point for future multiphysics development.
The results also demonstrate a practical CAE workflow for progressing from analytical engineering calculations to numerical simulation.

### 24.5 Current Limitations
The conclusions of this study must be considered within the limitations of the current model.
The present analysis does not yet include:
Fully coupled thermo-structural analysis, Explicit brake-pad contact, Frictional heat-generation modeling, Rotor rotational motion, CFD-based ventilation analysis, Internal ventilation-surface convection, Radiation in the implemented thermal model, Detailed hub thermal interaction, Temperature-dependent material properties, Bolt preload, Hub and wheel flexibility, Fatigue analysis, Formal mesh-convergence validation, Experimental validation.
These limitations do not invalidate the completed baseline analyses, but they define the scope within which the current results should be interpreted.

### 24.6 Future Development
The next major development stage is to establish a stable thermo-structural coupling workflow.
The longer-term development path is:

```text
Analytical Braking Calculations
            ↓
Rotor CAD Development
            ↓
Transient Thermal Analysis
            ↓
Static Structural Analysis
            ↓
Thermo-Structural Coupling
            ↓
CFD Cooling Analysis
            ↓
Detailed Brake Contact
            ↓
Fatigue / Durability Analysis
            ↓
Design Optimization
            ↓
Experimental Validation
```

Future work will focus on improving the physical fidelity of the model while maintaining a controlled and verifiable simulation workflow.

### 24.7 Final Conclusion
The current study successfully establishes a baseline thermal and Static Structural CAE model of a lightweight ventilated brake rotor for the defined electric-vehicle braking condition.
The transient thermal analysis produced a peak temperature of approximately 52°C, while the standalone Static Structural analysis produced a maximum deformation of approximately 0.000914 mm and a maximum von-Mises stress of approximately 3.135 MPa under the calculated 228 N·m braking moment.
The results provide a useful numerical baseline for continued engineering development.
The project is therefore not considered a finished fully coupled multiphysics study. Instead, it represents a completed baseline CAE investigation with a clearly defined pathway toward thermo-structural coupling, CFD-based cooling analysis, fatigue assessment, design optimization and experimental validation.
The completed work provides the foundation for progressively developing the rotor into a higher-fidelity and better-validated engineering design.

## 25. Author
**Pavan Kumar Karsinapu**
Independent Engineering Researcher

### Areas of Focus
- Mechanical Engineering
- Computer-Aided Engineering (CAE)
- Finite Element Analysis (FEA)
- Computational Fluid Dynamics (CFD)
- Thermal Analysis
- Structural Analysis
- Multiphysics Simulation
- Electric Vehicle Engineering
- Engineering Design
- Engineering Optimization

### Research and Project Interests
The author's current work focuses on applying engineering simulation and CAE methodologies to mechanical and electric-vehicle engineering problems.
Key areas of interest include:
- Brake system design and analysis
- Electric-vehicle mechanical systems
- Thermal management
- Structural simulation
- Multiphysics analysis
- Lightweight engineering design
- Ventilated component development
- Computational engineering
- CAE-driven design optimization

### Project Contribution
For this project, the author developed and documented the engineering workflow from the initial braking requirements through analytical calculations, rotor CAD development, transient thermal analysis and Static Structural analysis.
The work includes:
- Definition of the severe braking design case.
- Analytical calculation of braking energy and torque.
- Development of the ventilated brake rotor geometry.
- CAD preparation using SpaceClaim.
- Development of the transient thermal model in ANSYS.
- Evaluation of the transient rotor temperature response.
- Development of the Static Structural model in ANSYS Mechanical.
- Structural mesh development within ANSYS Student computational constraints.
- Application of the equivalent 228 N·m braking moment.
- Evaluation of deformation, von-Mises stress, principal stress and elastic strain.
- Documentation of the thermo-structural coupling attempt and its current status.
- Identification of future multiphysics, CFD and optimization pathways.

### Research Approach
The project follows a progressive engineering simulation approach:

```text
Engineering Problem
        ↓
Analytical Calculations
        ↓
CAD Development
        ↓
Thermal Analysis
        ↓
Structural Analysis
        ↓
Thermo-Structural Development
        ↓
CFD / Multiphysics
        ↓
Optimization
        ↓
Validation
```

The project is developed as an independent engineering research and CAE study, with emphasis on documenting both successful analysis stages and identified simulation limitations.

### Professional Focus
The broader objective is to develop practical expertise in engineering simulation, finite element analysis, computational fluid dynamics and multiphysics modeling, with particular interest in applications involving electric vehicles, thermal management and lightweight mechanical systems.

## 26. Final Statement
This repository documents the complete development of a **lightweight ventilated brake rotor for electric-vehicle applications**, from the initial engineering requirements and analytical calculations through CAD development, transient thermal analysis and Static Structural analysis.
The project establishes a structured CAE workflow:

```text
Engineering Requirements
        ↓
Analytical Braking Calculations
        ↓
Brake Rotor CAD Development
        ↓
Transient Thermal Analysis
        ↓
Static Structural Analysis
        ↓
Thermo-Structural Development
        ↓
CFD Cooling Analysis
        ↓
Design Optimization
        ↓
Experimental Validation
```

The completed baseline work establishes the following:
- A severe braking condition of 80 km/h to 0 km/h in 4 seconds.
- A combined vehicle and rider mass of 195 kg.
- Approximately 48.15 kJ of total vehicle kinetic energy.
- Approximately 33.70 kJ of front-brake energy.
- Approximately 30.33 kJ of rotor thermal energy based on the defined heat-partition assumption.
- An equivalent braking torque of approximately 228 N·m.
- A lightweight ventilated rotor geometry with 24 ventilation vanes.
- A transient thermal simulation with a peak rotor temperature of approximately 52°C.
- A successfully completed standalone Static Structural analysis.
- A maximum structural deformation of approximately 0.000914 mm.
- A maximum von-Mises stress of approximately 3.135 MPa.
- A maximum principal stress of approximately 1.915 MPa.

The current project should be understood as a baseline CAE investigation, not as a fully validated production brake-rotor design.
The transient thermal model uses simplified thermal boundary conditions, while the Static Structural model represents the mechanical response to the equivalent braking torque without thermal loading.
The thermo-structural coupling was investigated but was not successfully completed. Therefore, thermal stress and combined thermo-mechanical deformation are not claimed as completed results.

The major remaining development areas are:
- Successful thermal-to-structural coupling.
- Temperature-dependent material properties.
- Detailed brake-pad contact modeling.
- Frictional heat-generation modeling.
- Rotor rotation and moving heat-source representation.
- CFD-based ventilation and cooling analysis.
- Improved convection and radiation modeling.
- Thermal cycling analysis.
- Fatigue and durability assessment.
- Mesh-convergence studies.
- Multi-objective design optimization.
- Experimental validation.

The long-term objective is to progress from the current baseline model toward a higher-fidelity multiphysics representation of the brake rotor:

```text
Current Baseline
      ↓
Transient Thermal
      +
Static Structural
      ↓
Thermo-Structural Coupling
      ↓
CFD-Based Cooling
      ↓
Detailed Brake Contact
      ↓
Thermal Cycling / Fatigue
      ↓
Design Optimization
      ↓
Experimental Validation
```

The value of the current work is therefore not limited to the individual simulation results. It establishes a documented engineering methodology, identifies the limitations of the current model, and provides a reproducible foundation for continued development.

**Project status:**
Baseline Thermal and Static Structural CAE Analysis Completed
Thermo-Structural Coupling and Advanced Multiphysics Analysis Remain Future Development

This repository will continue to evolve as the model is refined, additional physics are incorporated and the numerical results are further validated.




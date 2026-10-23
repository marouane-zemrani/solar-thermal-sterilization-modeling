# Modeling and Design of a Solar Thermal System for Hospital Sterilization

**Physical Modeling | Thermal Engineering | Differential Equations | Numerical Simulation**

Academic engineering project, EMINES – Mohammed VI Polytechnic University (UM6P), Morocco

## Overview

This project develops a **conceptual design and numerical model** of a solar thermal system intended to support water heating for hospital sterilization in **Ouarzazate, Morocco**.

The study combines thermal-demand estimation, regional solar-resource assessment, equipment sizing, heat-transfer calculations, a coupled transient thermal model, pump-control logic, and preliminary cost estimation.

The objective was not to manufacture or install a system, but to explore how physical modeling can guide the design of a solar-powered heating solution under realistic geographic and operating assumptions.

> **Project scope:** All sizing figures, efficiencies, and costs below are results or assumptions from an academic design study. They are not verified equipment specifications, certified sterilization performance, or measurements from an installed system.

## 1. Problem Definition

Hospital sterilization requires substantial and reliable thermal energy. The project considered whether solar heat could contribute to this demand while potentially reducing dependence on conventional energy sources.

The reference scenario was based on an illustrative hospital use case in **Ouarzazate**, a Moroccan location with substantial solar potential. The study examined the system under less favorable seasonal irradiation conditions as well as other operating scenarios.

The overall methodology was organized into seven connected stages:

1. Estimate daily thermal-energy demand.
2. Characterize available solar energy and collector orientation.
3. Select and size the main thermal-system components.
4. Model conduction, convection, radiation, and fluid circulation.
5. Solve the transient thermal balance numerically.
6. Study operating scenarios and pump regulation.
7. Estimate the system's preliminary capital cost.

## 2. Estimating the Thermal Demand

The original project used the following illustrative assumptions:

| Parameter | Assumption used in the study |
|---|---:|
| Reference facility | Hospital use case in Ouarzazate |
| Sterilization cycles | 12 per day |
| Water/steam volume equivalent per cycle | 10 L |
| Daily equivalent volume | 120 L |
| Initial water temperature | 20 °C |
| Target heating temperature | Approximately 120 °C |

Using a basic sensible-heating energy balance,

$$
Q=m c_p\Delta T,
$$

with 120 kg of water, $c_p\approx 4186\ \mathrm{J/(kg\,K)}$, and $\Delta T\approx 100\ \mathrm{K}$, the study estimated:

$$
Q\approx 50.2\ \mathrm{MJ}\approx 14.0\ \mathrm{kWh}.
$$

**Important note on the source:** The original slides report approximately **15.1 kWh/day (54.4 MJ/day)** for this step. These reported numbers do not exactly match the displayed $m c_p\Delta T$ calculation. Both are therefore distinguished here rather than presenting the reported estimate as a verified arithmetic result. The original study used approximately **15 kWh/day** as its working design requirement.

This simple heating estimate does **not** by itself establish the full energy demand of a real steam sterilization cycle; latent heat, losses, duty cycles, and sterility requirements would need separate engineering assessment.

## 3. Solar Resource and Design Conditions

The study used **PVGIS** information to examine solar availability and an indicative collector orientation for the Ouarzazate location. The solar-resource comparison motivated a conservative focus on **December**, a relatively low-irradiation month.

The study used approximately **5.6 hours/day** as a reference solar-exposure duration in the winter case. Collector tilt and orientation were considered when estimating the available radiation.

Solar irradiance later enters the dynamic model as a simplified daily profile, with zero irradiance outside daylight hours and a smooth daytime variation.

## 4. Proposed System Architecture

The conceptual system combines:

```text
Solar radiation
      |
      v
Evacuated-tube solar collector
      |
      v
Circulating heat-transfer fluid + pump
      |
      v
Heat-exchanger coil inside an insulated storage tank
      |
      v
Heated water supplied to the sterilization system
```

The return loop brings cooler heat-transfer fluid back toward the collector.

### Collector selection

The project compared different solar-thermal collector technologies and selected an **evacuated-tube collector** for the studied high-temperature heating application, based on the thermal-performance characteristics considered in the original presentation.

### Storage tank

A **120 L cylindrical storage tank** was sized using a surface-area/volume argument. The study considered tank dimensions, pressurized operation, structural stress, and insulation.

The material and design assumptions included an enamelled carbon-steel vessel and polyurethane insulation. An operating-pressure assumption of approximately **3 bar** was considered for keeping water liquid at elevated temperature. These are preliminary design assumptions, not a pressure-vessel certification.

### Heat exchanger

A coil-type heat exchanger transfers energy from the solar-loop fluid into the stored water. The study considered:

- Hot-side and cold-side inlet/outlet temperatures.
- An illustrative heat-transfer fluid (TYFOCOR).
- Copper as the heat-exchanger tubing material.
- Forced convection on the circulating-fluid side and natural convection in the tank.
- Overall heat-transfer coefficient and logarithmic mean temperature difference (LMTD).

The exchanger-sizing relationship is:

$$
\dot Q=U A\Delta T_{\mathrm{lm}},
$$

where $U$ is the overall coefficient, $A$ the exchange surface, and $\Delta T_{\mathrm{lm}}$ the log-mean temperature difference.

The original presentation explored the corresponding exchange area and coil length and considered the effectiveness of the heat-transfer stage. Its numerical values should be treated as preliminary estimates based on assumed operating conditions.

### Piping and circulation pump

Pipe length, insulation, and heat losses were estimated for the thermal-fluid loop. Hydraulic pressure-loss calculations included the piping and other components to size an indicative circulation pump.

The project also considered a temperature-dependent pump-control strategy to avoid circulation when solar-loop conditions are unfavorable. The control logic uses temperature differences between the absorber, tank, and collector outlet to determine when flow should start or stop.

## 5. Transient Thermal Modeling

A central part of the work was to construct a **coupled system of energy-balance equations** for the collector and storage arrangement.

The principal modeled elements were:

- **Collector glazing:** solar absorption, convection with outdoor air, and radiative exchange.
- **Absorber:** absorbed solar power, radiation, thermal conduction/losses, and energy transfer to the working fluid.
- **Heat-transfer fluid:** convection from the absorber and energy transported by circulation.
- **Storage tank:** incoming energy from the exchanger and thermal losses to the environment.

The equations follow the general transient energy-balance form:

$$
C_i\frac{dT_i}{dt}=\dot Q_{\mathrm{in},i}-\dot Q_{\mathrm{out},i},
$$

with component temperatures $T_i$, lumped thermal capacities $C_i$, and heat-transfer terms coupling the components.

### Numerical integration

The system was numerically integrated using the **forward Euler method**. Illustrative initial temperatures were set to the ambient value, with time-dependent solar irradiation acting as the external input.

The study followed the evolution of collector-glass, absorber, heat-transfer-fluid, and tank temperatures over a **24-hour simulation** and compared cases with different collector surface areas and environmental/operational assumptions.

### Heat-loss and pump scenarios

Additional simulations incorporated thermal losses in the pipes, on/off circulation logic, and optimistic, baseline, and pessimistic scenarios. This allowed the study to compare system behavior beyond a single idealized configuration.

## 6. Reported Results and Design Outputs

The main outputs reported in the original academic presentation were:

| Topic | Reported outcome |
|---|---|
| Daily heating requirement | Approximately 15 kWh/day used as the study's design target (see calculation note above) |
| Storage | Conceptual 120 L insulated cylindrical tank |
| Collector | Evacuated-tube solar thermal collector selected |
| Thermal model | Coupled transient energy balances integrated using Euler's method |
| Winter scenarios | Collector/tank temperature trajectories analyzed under low-solar-resource assumptions |
| Illustrative pessimistic scenario | 4 m² collector area, with a reported overall simulated efficiency of **55.28%** |
| Budgeting scenario | **5 m²** of collectors in the preliminary cost table |
| Estimated project cost | Approximately **44,000 MAD** in the original study |

The two collector areas above refer to **different analyses** in the source presentation: the 4 m² pessimistic simulation and the 5 m² cost-estimation configuration. They are not presented as a single verified final design.

The presentation also includes a qualitative/graphical thermal simulation of an evacuated-tube collector, illustrating the temperature distribution across its structure.

## 7. Discussion and Limitations

The project illustrates how thermal-system design can be connected to numerical modeling, from an energy requirement to a coupled dynamical model. It also shows how seasonal solar availability, component geometry, heat exchange, and control decisions affect expected operating temperatures.

Several limitations matter before considering a real installation:

- The reference load is an **illustrative design assumption**, not a measured sterilization energy audit.
- The initial energy budget uses a simplified sensible-heat calculation and omits several process requirements.
- Component properties, convection coefficients, pressure drops, and costs are estimated or assumed.
- The simulation is a conceptual model; no experimentally measured performance or field validation is reported.
- Pressurized high-temperature equipment and medical sterilization require specialist engineering, safety checks, and regulatory validation.
- The original numerical model and detailed simulation code are **not included** in this README-only repository, so the simulation cannot be rerun here.

Accordingly, the reported efficiency, equipment choices, and cost estimates should not be interpreted as a procurement recommendation or deployable hospital design.

## 8. Academic Context and Credits

**Institution:** EMINES – School of Industrial Management, Mohammed VI Polytechnic University (UM6P)  
**Project:** *Étude et dimensionnement d'un capteur solaire pour la stérilisation de matériel d'un hôpital à Ouarzazate*  
**Project contributors (as listed in the original French presentation):**

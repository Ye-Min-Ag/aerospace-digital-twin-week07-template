# Week 07 Controls Lab — Responses

Answers and recorded model results from `submission.json`. This document does not recompute or independently validate the results.

## Submission status

- Schema: week07.submission/v1

- Record ID: db3f21c0-3eb4-4696-92bd-b0aca27a520b

- Record revision: 683

- Model hash: fnv1a-57f164d3

- Readiness: Marked incomplete or not ready; missing: verification, claim, reflection, aiUse, execution

## Supplied setup (instructor supplied)

### question — instructor supplied
Calculate required control moment, elevator moment, and the change with airspeed. Explain whether the nominal response meets +0.12 rad/s².

### system — instructor supplied
Illustrative planar pitch model. Aircraft geometry, integration, force conversion and constraints are supplied.

### representation — instructor supplied
Body axes forward/right/down. Positive pitch moment nose-up. Positive Fz downward. Positive elevator trailing edge down. Reference/CG X=0 m; tail X=-3 m.

### inputs — instructor supplied
Iy=5000 kg·m²; target=+0.12 rad/s²; competing=-750 N-m; density=1.225 kg/m³; V=40 m/s; S=16 m²; chord=1.5 m; Cmδ=-0.8/rad; elevator=-5°. Inputs are illustrative, not calibrated.

## Student responses

### physics
**Prompt:** Explain why a downward force aft of the CG gives a positive nose-up moment.

**Student response:**
```
A downward force creates a counterclockwise torque around CG in the +Y axis.
```

### assumptions
**Prompt:** Explain one supplied assumption and what could invalidate it: planar motion, fixed reference, local linear effectiveness, no trim or damping.

**Student response:**
```
The model assumes that the elevator's effectiveness is linear​. This means that increasing elevator deflection by a certain amount produces a proportional increase in pitching moment. This assumption may become invalid at large elevator deflections or near stall conditions
```

### model
**Prompt:** Write your demand, dynamic-pressure, coefficient and moment equations. Identify which quantities are supplied and which are unknown.

**Student response:**
```
Demand = Iy * target - competing

Dynamic Pressure = 0.5 * density * V^2

Cm_delta = Moment / q∞ S c_bar

Moment = Cm_delta * q∞ * S * c_bar
```

### prediction
**Prompt:** Before running your own implementation, predict the sign of its elevator moment and the effect of halving airspeed. Explain the competing moment.

**Student response:**
```
The sign of elevator moment is + since it results in nose-up moment. 

Halving the airspeed will decrease the moment by a factor of 4 as per the moment equation, assuming that Cm, dynamic pressure, and mean chord length remain constant.

A competing moment can be thought of as the total moment upon the aircraft that is pitching the aircraft in the opposite direction of the demand monment. Competing moment can come from drag forces, lift forces on other control surfaces and components. It is not necessarily constant.
```

### verification
**Prompt:** Show one independent hand calculation with units. Compare it with your model, and explain a sign, unit, or limiting-case check.

**Student response:**
_Missing — no response supplied._

### claim
**Prompt:** What do your computed results support at the stated condition? Include a limitation.

**Student response:**
_Missing — no response supplied._

### reflection
**Prompt:** What additional evidence or missing physics would you investigate next?

**Student response:**
_Missing — no response supplied._

### AI use
**Prompt:** Identify the AI tool and how you used it, what you changed, and how you independently checked the result. State “No AI used” if applicable.

**Student response:**
_Missing — no response supplied._

## Equations and model source

The recorded model JSON/expression source follows exactly as supplied. It is not interpreted or recomputed here.

```
{
  "schemaVersion": "week07.student-model/v1",
  "id": "week07-student-model",
  "version": "1.0.0",
  "slots": [
    {
      "id": "controls.demand",
      "expressions": [
        {
          "name": "requiredMoment",
          "expression": "pitchInteria * requestedAcceleration - competingMoment",
          "unit": "N*m"
        }
      ]
    },
    {
      "id": "controls.effectiveness",
      "expressions": [
        {
          "name": "dynamicPressure",
          "expression": "0.5 * density * airspeed * airspeed",
          "unit": "Pa"
        },
        {
          "name": "deltaCm",
          "expression": " elevatorDerivative * elevatorAngle",
          "unit": "1"
        },
        {
          "name": "deltaMoment",
          "expression": "dynamicPressure * referenceArea * referenceChord * deltaCm",
          "unit": "N*m"
        }
      ]
    }
  ]
}
```

## Recorded verification status

No verification record was supplied.

## Recorded model runs

_Missing — no model runs supplied._

## Submission instructions

Use Save to GitHub in the app to save both files, commit, and push. Submit your fork URL and the saved commit SHA. Manual fallback: save this file beside `student/submission.json`, run `npm run student:prepare` and `npm run student:validate`, then commit and push student/.

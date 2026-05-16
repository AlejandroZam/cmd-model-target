# Target — Model Description

## Dynamics

Constant-velocity ground vehicle. The target integrates position and velocity in 3-D but enforces `z = 0` on initialization. Lateral acceleration noise simulates terrain-induced disturbances.

Six integrators are registered with the OSK kernel (pos x/y/z, vel x/y/z). The acceleration state is driven by noise only — there is no feedback control.

## Noise Channels

| Key                | Applied to      | Typical use              |
|--------------------|-----------------|--------------------------|
| `noise.lateral_x`  | `acc.x`         | Terrain / road roughness |
| `noise.lateral_y`  | `acc.y`         | Terrain / road roughness |

Noise is sampled in `eventUpdate()` and held across RK4 sub-steps.

## Inter-model Communication

- **DDS publish:** topic `sim.<name>.state` (e.g. `sim.target.state`) — `StateMsg` containing `t, px, py, pz, vx, vy, vz`
- **UDP stream:** `VizBridge::get().send()` called every `report()` for real-time visualization

## Outputs

| Signal | Units | Description      |
|--------|-------|------------------|
| `t`    | s     | Simulation time  |
| `px`   | m     | Position X       |
| `py`   | m     | Position Y       |
| `pz`   | m     | Position Z (= 0) |
| `vx`   | m/s   | Velocity X       |
| `vy`   | m/s   | Velocity Y       |
| `vz`   | m/s   | Velocity Z (= 0) |

## Configuration Reference

```yaml
model:
  initial_position: [3000.0, 200.0, 0.0]   # m
  initial_velocity: [20.0, 5.0, 0.0]        # m/s
  report_rate_hz: 2.0

noise:
  lateral_x:
    distribution: gaussian
    mean: 0.0
    stddev: 0.1    # m/s²
  lateral_y:
    distribution: gaussian
    mean: 0.0
    stddev: 0.1    # m/s²
```

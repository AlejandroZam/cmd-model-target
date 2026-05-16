# cmd-model-target

Constant-velocity 3-D ground target model for the CMD simulation framework.

The target moves at a nominally constant velocity (z = 0 enforced) with optional lateral acceleration noise. State is published each time step via FastDDS and streamed to the real-time UDP visualizer.

## Usage

Add to a CMD scenario YAML:
```yaml
- name: target
  type: Target
  config: target_params.yaml
  enabled: true
  order: 0
```

Config parameters are documented in `Config/default_params.yaml`.

## Layout

```
include/   target.h
src/       target.cpp
Config/    default_params.yaml
doc/       model_description.md
```

## Dependencies

Requires the `osk` package from [cmd-simulations](https://github.com/AlejandroZam/cmd-simulations).

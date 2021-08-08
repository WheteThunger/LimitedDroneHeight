## Features

- Limits how high RC drones can be flown above terrain

## Permissions

The following permissions come with the plugin's **default configuration**. Granting one to a player determines how high their drones can be flown above terrain or water, overriding the default. Granting multiple profiles to a player will cause only the last one to apply, based on the order in the config.

- `limiteddroneheight.low` -- 25m
- `limiteddroneheight.medium` -- 75m
- `limiteddroneheight.high` -- 125m
- `limiteddroneheight.unlimited` -- No limit

You can add more profiles in the plugin configuration (`ProfilesRequiringPermission`), and the plugin will automatically generate permissions of the format `limiteddroneheight.<suffix>` when reloaded.

## Configuration

Default configuration:

```json
{
  "DefaultMaxHeight": 75,
  "ProfilesRequiringPermission": [
    {
      "PermissionSuffix": "low",
      "MaxHeight": 25
    },
    {
      "PermissionSuffix": "medium",
      "MaxHeight": 75
    },
    {
      "PermissionSuffix": "high",
      "MaxHeight": 125
    },
    {
      "PermissionSuffix": "unlimited",
      "MaxHeight": 0
    }
  ]
}
```

- `DefaultMaxHeight` -- Max height for drones deployed by players who do not have permission to any profiles in `ProfilesRequiringPermission`.
- `ProfilesRequiringPermission` -- Each profile in this list generates a permission like `limiteddroneheight.<suffix>`. Granting a profile to a player determines how high their drones can be flown above terrain or water, overriding `DefaultMaxHeight`.
  - `PermissionSuffix` -- Determines the generated permission of format `limiteddroneheight.<suffix>`.
  - `MaxHeight` -- Determines the max height for drones deployed by players with this profile.

## Developer Hooks

#### OnDroneHeightLimit

```csharp
bool? OnDroneHeightLimit(Drone drone)
```

- Called when this plugin is about to start monitoring and limiting a drone's height
- Returning `false` will prevent this plugin from limiting the drone's height
- Returning `null` will result in the default behavior

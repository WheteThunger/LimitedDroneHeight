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

Note: Having a building below the drone does **not** allow it to fly higher. Height is only dictated by terrain and water. For this reason, if you want drones to be able to take off from and land on tall buildings, you should set the height limits to approximately 75m, or higher if your server has reduced stability requirements.

## Recommended compatible plugins

Drone balance:
- [Drone Settings](https://umod.org/plugins/drone-settings) -- Allows changing speed, toughness and other properties of RC drones.
- [Targetable Drones](https://umod.org/plugins/targetable-drones) -- Allows RC drones to be targeted by Auto Turrets and SAM Sites.
- [Limited Drone Range](https://umod.org/plugins/limited-drone-range) -- Limits how far RC drones can be controlled from computer stations.
- [Limited Drone Height](https://umod.org/plugins/limited-drone-height) (This plugin) -- Limits how high RC drones can be flown above terrain.

Drone fixes and improvements:
- [Better Drone Collision](https://umod.org/plugins/better-drone-collision) -- Overhauls RC drone collision damage so it's more intuitive.
- [Auto Flip Drones](https://umod.org/plugins/auto-flip-drones) -- Auto flips upside-down RC drones when a player takes control.
- [Drone Hover](https://umod.org/plugins/drone-hover) -- Allows RC drones to hover in place while not being controlled.

Drone attachments:
- [Drone Lights](https://umod.org/plugins/drone-lights) -- Adds controllable search lights to RC drones.
- [Drone Turrets](https://umod.org/plugins/drone-turrets) -- Allows players to deploy auto turrets to RC drones.
- [Drone Storage](https://umod.org/plugins/drone-storage) -- Allows players to deploy a small stash to RC drones.
- [Drone Boombox](https://umod.org/plugins/drone-boombox) -- Allows players to deploy boomboxes to RC drones.
- [Ridable Drones](https://umod.org/plugins/ridable-drones) -- Allows players to ride RC drones by standing on them or mounting a chair.

## Developer Hooks

#### OnDroneHeightLimit

```csharp
bool? OnDroneHeightLimit(Drone drone)
```

- Called when this plugin is about to start monitoring and limiting a drone's height
- Returning `false` will prevent this plugin from limiting the drone's height
- Returning `null` will result in the default behavior

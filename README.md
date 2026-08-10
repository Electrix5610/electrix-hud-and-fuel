# Electrix HUD + Electrix Fuel

Electrix HUD + Electrix Fuel is a combined Heads-Up Display and vehicle fuel system for FiveM. This page documents the script, shows screenshots, explains features, and provides installation and configuration instructions so server owners and developers can get it running quickly.

---

## Preview

Add screenshots or a demo video here. Example:

- Screenshot: docs/screenshots/hud.png
- Demo: (link to video)

---

## Features

- Clean, minimal HUD showing speed, health, armor, fuel, and other vehicle info
- Integrated fuel system tied to vehicle speed and engine state
- Configurable fuel consumption rates and display options
- Easy to integrate into existing FiveM servers
- Lightweight and optimized for performance
- Exports/events/hooks for other resources to read or modify fuel

---

## Requirements

- FiveM server
- A client capable of running the resource (standard FiveM client)
- Lua 5.1 (default in FiveM)

---

## Installation

1. Download or clone this repository into your server `resources` folder, e.g.:

   git clone https://github.com/Electrix5610/electrix-hud-and-fuel.git

2. Add the resource to your `server.cfg` (or start it through your resource manager):

   start electrix-hud-and-fuel

3. Restart your server or ensure the resource is started.

---

## Quick Start

After installation, the HUD and fuel system will start automatically. By default, the HUD should display when the player is in a vehicle and will show fuel consumption as the vehicle moves. Use the configuration below to change behavior.

---

## Configuration

Open `config.lua` (or the relevant configuration file) to tweak options. Example configurable values:

- `FuelConsumptionMultiplier` — change how quickly fuel drains
- `ShowSpeedInKmh` — true/false
- `HUDPosition` — x,y anchor values
- `ShowArmor` — toggle armor display

(If your resource uses a different config filename, update these instructions accordingly.)

---

## Commands & Keybinds

Provide any commands or keybinds here (replace placeholders with actual command names):

- `/refuel` — refuel nearest vehicle (server command)
- `U` — toggle HUD visibility (client keybind)

---

## Exports & Events (Examples)

Expose interfaces so other resources can interact with the fuel system. Below are example patterns — adapt names to your implementation:

Client export example (to get current fuel level for a vehicle):

```lua
local fuel = exports['electrix-hud-and-fuel']:GetVehicleFuel(vehicle)
print(('Fuel: %.2f%%'):format(fuel))
```

Server event example (triggered when refueling completes):

```lua
TriggerEvent('electrix-fuel:refueled', source, plate, amount)
```

Note: Update these examples to match your actual export and event names.

---

## Example: Updating HUD with Fuel

Here's an example client loop that queries the fuel and updates a custom NUI HUD. Replace `GetVehicleFuel` with your resource's actual exported function:

```lua
Citizen.CreateThread(function()
  while true do
    Citizen.Wait(500)
    local ped = PlayerPedId()
    if IsPedInAnyVehicle(ped, false) then
      local veh = GetVehiclePedIsIn(ped, false)
      local fuel = exports['electrix-hud-and-fuel']:GetVehicleFuel(veh)
      SendNUIMessage({action = 'updateFuel', fuel = fuel})
    else
      SendNUIMessage({action = 'hideHUD'})
    end
  end
end)
```

---

## Screenshots

Place images in `docs/screenshots/` and reference them here.

---

## Troubleshooting

- HUD not showing: ensure the resource is started in `server.cfg` and that your client has NUI enabled.
- Fuel not changing: check your config values and ensure any database or persistence layer is set up if used.

---

## Contributing

Contributions are welcome. Open issues or create pull requests for fixes and improvements. Please follow the repo's contribution guidelines if present.

---

## License

Include your license here (e.g., MIT). Example:

MIT License

---

## Contact

Author: Electrix5610

Repository: https://github.com/Electrix5610/electrix-hud-and-fuel

If you'd like changes to this page (different layout, a live demo embed, more technical API docs), tell me what to include and I'll update it.
# 🌟 RBAvatar Aura System (`package-aura`)

A highly optimized, Client-Side Rendering (CSR) visual effects framework for Roblox avatars.

This package automatically detects players wearing supported RBAvatar skins (via Asset ID / Bundle ID) and seamlessly renders stunning, high-performance auras around their characters.

## 🚀 Key Features

- **Zero-Trust & Safe:** 100% open-source Lua code. No backdoors, no malicious scripts.
- **Extreme Performance (CSR):** Uses Client-Side Rendering. The server only assigns lightweight Attributes. The player's local hardware handles the heavy lifting of rendering particles (like spinning rings and random twinkle stars), resulting in **zero server lag** even with 100 players.
- **Automatic Detection:** Players do not need to buy the aura. The system automatically reads their equipped `HumanoidDescription` and applies the aura tied to their skin ID.
- **Extensible Framework:** Want to add your own custom aura? You can easily register new auras and map them to your own skins using our built-in API.

## 📂 Architecture

This package uses a strict separation of concerns to maintain performance:

1. **`AuraSystemManager.server.lua`:** The core registry. It only stores valid aura IDs and ensures naming conventions (e.g., `rbcyberpunk-circle`, `rbcelestial-stars-gold`).
2. **`AuraSkinMapper.server.lua`:** The server-side listener. When a player spawns, it checks their equipped Asset IDs. If a match is found, it simply tags the character with an `ActiveAuraID` attribute.
3. **`AuraClientController.local.lua`:** The client-side engine. It watches for the `ActiveAuraID` attribute and routes the rendering task to specific ModuleScripts.
4. **`Auras/` (ModuleScripts):** Contains the actual visual logic (e.g., `CircleAura.client.lua`, `TwinkleAura.client.lua`) that runs entirely on the player's device.

## 🛠️ Installation (Roblox Studio)

1. Get the **RBAvatar Aura Package** from the Roblox Toolbox (or sync from this repository).
2. Place `AuraSystemManager` and `AuraSkinMapper` inside `ServerScriptService`.
3. Place `AuraClientController` and the `Auras` folder inside `StarterPlayer > StarterPlayerScripts`.
4. In `AuraSkinMapper.server.lua`, add your Avatar Asset IDs to the `avatarToAuraMap` table to link them to specific aura IDs.

## 📝 Creating Custom Auras

You can create your own aura ModuleScript inside the `Auras` folder and register its valid ID in `AuraSystemManager`.

**Naming Convention Rule:** All Aura IDs must be lowercase, use hyphens, and follow the format `{prefix}-{name}` (e.g., `rostard-apocalypsesmoke`). The prefix `rbavatar-` is reserved.

## ⚖️ License

MIT License - Free to use, modify, and distribute.

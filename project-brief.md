# Gate Control Project Brief
Date started: 2026-09-27

## The Hardware
- **Board**: DTWONDER 16 Channel Relay Board (by Dingtian Tech)
- **Connectivity**: WiFi + Ethernet built-in
- **Protocols supported**: HTTP, TCP/UDP, MQTT, Modbus, CANopen
- **Smart home**: Home Assistant & openHAB compatible
- **Default WiFi AP**: SSID `dtrelay` + serial number
- **Default LAN IP**: 192.168.7.1
- **Default login**: admin / admin
- **SDK**: www.dingtian-tech.com/sdk/relay_sdk.zip

## The Goal
Build a simple web app (or mobile-friendly web page) that lets someone
remotely open and close a gate wired to one of the 16 relays on this board.

## How It Works (conceptually)
```
[Phone/Browser] → [Internet] → [Router/WiFi] → [DTWONDER board] → [Gate relay] → [Gate moves]
```
The gate is wired to one relay (e.g. Relay 1).
Triggering the relay sends a momentary pulse — same as pressing a physical button on the gate.

## What We Need to Figure Out Before Building

### 1. Network / Internet access
The board MUST be on a network (WiFi or Ethernet). No network = no remote control.
Pick one of these to expose it to the internet:
- [ ] **Port forwarding** on the router (simple, less secure)
- [ ] **Cloudflare Tunnel** (free, secure — needs a small device like a Raspberry Pi on the same network)
- [ ] **VPN** like Tailscale or WireGuard (secure, user needs VPN client on phone)

### 2. Which relay is the gate wired to?
- Relay number: ___

### 3. Gate type / pulse behavior
- Does the gate need a momentary pulse (tap = toggle open/close)?
- Or separate OPEN and CLOSE signals?
- How long should the relay stay on? (typical: 0.5s – 1s)

### 4. Security / access control
- Who should be able to open the gate?
- Should the app require a PIN or password?
- Should it log who opened it and when?

### 5. Platform preference
- Web app (works on any browser, no install needed) — recommended
- Native mobile app (more work, needs App Store publishing)

## Planned App Features (v1)
- One big "Open Gate" button
- Password or PIN protection
- Works on phone browser (mobile-friendly)
- Sends HTTP command to board → pulses relay → gate moves

## Nice to Have (v2)
- Gate status indicator (open/closed) — needs a sensor wired to a digital input on the board
- Access log (who opened, when)
- Multiple gates / relays
- Scheduled access (time-limited links)

## Notes
- Start with local network testing first, add remote access after
- The board already has a built-in web UI at 192.168.7.1 — useful for testing relay manually
- The HTTP API format needs to be confirmed from the Dingtian SDK or by probing the device

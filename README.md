# AHS Electronics Workshop Search and Report Project Web Dashboard

### The Project:
- Students make a car-thing
- It's placed on a flat square surface (OOM 1 meter-ish) with walls on all sides
- There are magnets hidden underneath the surface, and coloured squares on the surface
- Students use the RPi Pico W, time-of-flight sensors, RGB color sensors, hall effect sensors, etc. to find out where the squares/magnets are
- The libraries we have written for/ported to MicroPython to be used in this project at [AHS Programming Club's Github](https://github.com/AHSPC)

### This:
- Is a web interface that visualizes the data sent by the vehicles (positions of magnets and coloured squares on a grid)
- Also provides a simple log over wifi for debugging without being connected to serial, as well as a super basic graphing/plotting interface
- Provides a helper library (`web_dashboard.py`) for sending data to the web interface

Made by [@blobbybilb](https://github.com/blobbybilb)

## Usage

Make sure elixir and mix are installed on whichever system you're hosting this.

```sh
# To run the new version:
git clone https://github.com/blobbybilb/AHS-EW-SAR-dashboard
# Get dependencies
mix deps.get
# Start the server (TCP socket server for Picos on :3101, http server on :3102)
iex -S mix
# Now web_dashboard.py should be able to send stuff to the server (after you put in the correct server IP)
# It will also start an interactive Elixir session, where you can enter:
DataStore.persist_data()
# to save data to disk (this is done to avoid frequent writes to the Micro SD and avoid wearing it out)
```

## Screenshots

(slightly outdated)
![image](https://github.com/blobbybilb/AHS_Electronics_pico_search_project_web_dashboard/assets/58201828/12c03934-407a-461c-b25b-2c1d57de6875)
<img width="648" alt="Screenshot 2024-02-14 at 9 30 37 PM" src="https://github.com/blobbybilb/AHS_Electronics_pico_search_project_web_dashboard/assets/58201828/0332f15e-98a4-465f-8359-c4d75afade2c">

## Notes about AUSD network/WiFi
*mostly for whomever maintainership of this goes to after I graduate*
- The school blocks HTTP on basically every port
- The school blocks UDP on AFAIK every port (not that I want to implement retransmissions, etc. anyway)
- The school sometimes blocks inbound TCP packets (and not outbound)
- The school randomly blocks domains (via DNS (but it seems some IPs are blocked at a different level?))
- The school has several networks, the rules are different for each (as I found out during 6th Period (AP CSA) 14.Feb.2024)
- All the above statements may or may not be accurate, so please don't modify the setup unless needed. It's okay. Rewriting it in Rust won't make the network any faster. Well don't say I didn't warn you.
- MicroPython doesn't support WPA2 Enterprise which is what the student wifi uses as of when I wrote this

We are running everything locally on an SBC connected to the wifi network above. I rewrote it in Elixir (old version is in ./v1/) and removed all the hacky stuff.

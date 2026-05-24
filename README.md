# Phone Compass

A browser app which displays a compass on mobile browser and send heading data to provided websocket server.
The purpose is to use the heading data as steering input for virtual bicycle in the unreal engine project.

## Notes

For standalone testing you can use the websocket server from bicycle_scripts\phone_orientation folder. 

Make sure that mobile's screen is ON. If screen is OFF, then it won't send the heading data to webscoket server and steering won't work. 
---

# Architecture

This setup requires two Python servers:

1. **HTTP Server**  
   Hosts the HTML file on port `8123`.

2. **Python WebSocket Server**  
   Runs on port `8080`.

The phone connects directly to the WebSocket server after clicking the **Start** button in `index.html`.

---

## Chrome Configuration (Required for Mobile Sensors)

To allow mobile browsers to access orientation and motion sensor APIs over a local network HTTP connection, you must enable the Chrome flag:

```text
chrome://flags/#unsafely-treat-insecure-origin-as-secure
```

### Steps

1. Open Chrome on your phone.
2. Navigate to:

```text
chrome://flags/#unsafely-treat-insecure-origin-as-secure
```

3. In the flag settings, add your PC IP address, for example:

```text
http://192.168.1.10:8123
```

4. Enable the flag.
5. Restart Chrome.

See the image below for reference:

![Chrome Flags Reference](chrome_flags.jpg)

---

# How to Use

## 1. Open Command Prompt

Open a command prompt from the location of this folder.

---

## 2. Start the HTTP Server

Run:

```bash
python -m http.server 8123
```

---

## 3. Start the WebSocket Server

If the Python WebSocket server is not already running, open another command prompt from \bicycle_scripts\phone_orientation folder and run:

```bash
python server.py
```

---

## 4. Open the Web Page on Your Phone

Get the IP address of your machine (for example `192.168.1.10`) and open the following link on your Android/iOS device:

```text
http://[IP_ADDRESS]:8123
```

Example:

```text
http://192.168.1.10:8123
```

---

## 5. Start Streaming Data

On the `index.html` page, enter the IP address of the machine running the WebSocket server. For example, if the server is running on the same machine, use ws://192.168.1.10:8080. Then click the **Start** button.

---

## 6. Verify Output

You should now see heading data in the command prompt where the Python WebSocket server is running.

Sample data:
message received: {"type":"heading","heading":82,"direction":"E"}
---



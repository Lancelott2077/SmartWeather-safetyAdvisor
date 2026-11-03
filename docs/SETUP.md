# How to Run the Smart Weather & Personal Safety Advisor (Node-RED part)

This guide shows you how to run the dashboard on your own Windows computer.
You do not need to be an expert. Follow the steps in order.

## What you will see when it works

A web page (the "dashboard") with cards that show:

- **Local sensor**: temperature, humidity and pressure from the sensor.
- **OpenWeather now**: what the weather service says right now for your area.
- **Forecast next 24 h**: the chance of rain over the next day.
- **Microclimate mismatch**: whether your local readings differ from the weather report.
- **Alert settings**: boxes where you can change how big a difference counts as a mismatch.
- **Recommendations**: simple advice on clothing, heat and rain.

> **Important:** In this version the "local sensor" numbers are **simulated**
> (made up by the program) so you can try everything without the hardware.
> Real sensor readings are connected in a later stage.

---

## Before you start: what you need

| Item | What it is | Where to get it |
|---|---|---|
| A Windows computer with internet | Where the program runs | Your own computer |
| Node.js | The engine that runs Node-RED | https://nodejs.org (download the **LTS** version and install it) |
| Node-RED | The tool that runs this project | Installed in Step 1 below |
| An OpenWeather key | A free password that lets the program ask for weather data | Step 2 below |
| Your latitude and longitude | Your location as two numbers | Step 3 below |

---

## Step 1: Install Node-RED (one time only)

1. Press the **Windows key**, type **PowerShell**, and open it.
2. Copy this line, paste it into the window, and press **Enter**:

   ```
   npm install -g --unsafe-perm node-red
   ```

3. Wait until it finishes and you see the prompt again. This can take a few minutes.

## Step 2: Get your free OpenWeather key (one time only)

1. Go to https://openweathermap.org and create a free account.
2. After signing in, open your profile menu and choose **My API keys**.
3. Copy the long key shown there (a mix of letters and numbers).

A brand-new key can take up to a couple of hours to start working. If you see
"HTTP 401" later, this is usually the reason, so wait and try again.

**Keep this key private.** Never post it in chat, email or on GitHub.

## Step 3: Find your latitude and longitude (one time only)

1. Open Google Maps in your browser.
2. Right-click on your location on the map.
3. The first item in the menu shows two numbers, such as `12.7523, 80.1926`.
   The first is your **latitude**, the second is your **longitude**.
   Click them to copy.

## Step 4: Download this project

1. Install Git if you do not have it: https://git-scm.com
2. In PowerShell, run:

   ```
   git clone https://github.com/Lancelott2077/SmartWeather-safetyAdvisor.git
   cd SmartWeather-safetyAdvisor
   ```

   (If you already have the folder, just run `git pull` inside it to get the latest version.)

## Step 5: Start Node-RED with your key and location

Every time you start the program, do this **in the same PowerShell window**.
Replace the parts in capital letters with your own values:

```
$env:OWM_API_KEY="PASTE_YOUR_KEY_HERE"
$env:WX_LAT="PASTE_YOUR_LATITUDE_HERE"
$env:WX_LON="PASTE_YOUR_LONGITUDE_HERE"
node-red
```

Wait until you see a line saying **Started flows**. Leave this window open.
Closing it stops the program.

> These three values only last as long as that PowerShell window is open.
> If you close it, you need to type them in again next time.

## Step 6: Load the project into Node-RED (one time only)

1. Open your web browser and go to **http://127.0.0.1:1880**
   (this is the Node-RED editing page on your own computer).
2. Click the **menu** button (three horizontal lines, top right) and choose **Import**.
3. Click **select a file to import** and pick the file `node-red\flows.json`
   from the project folder you downloaded in Step 4.
4. Click **Import**.
5. Click the red **Deploy** button (top right).

## Step 7: Install the dashboard add-on (one time only)

If some boxes on the screen look red with a question mark, or the dashboard page
does not open, the dashboard add-on is missing. Add it like this:

1. Click the **menu** button, then **Manage palette**.
2. Open the **Install** tab.
3. Type `@flowfuse/node-red-dashboard` and press Enter.
4. Click **install** next to the result, and confirm.
5. When it finishes, click **Deploy** again.

## Step 8: Open the dashboard

Go to **http://127.0.0.1:1880/dashboard** in your browser.

After about 10 to 30 seconds, all the cards should fill with numbers.
The page refreshes by itself, so you do not need to reload it.

## Step 9: Try changing the alert settings

On the dashboard, find the **Alert settings** card. Change the temperature or
humidity difference and submit it. The **Microclimate mismatch** card will use
your new numbers.

These settings go back to normal when you restart the program.

---

## Stopping and starting again

- **To stop:** click the PowerShell window and press **Ctrl + C**.
- **To start again:** repeat **Step 5** only. Steps 1 to 4, 6 and 7 are one-time.

---

## If something goes wrong

| What you see | What it means | What to do |
|---|---|---|
| Red boxes with a question mark in the editor | The dashboard add-on is missing | Do Step 7 |
| The dashboard page says "not found" | The add-on is missing, or the project was not deployed | Do Step 7, then click Deploy |
| Message: `Missing OWM_API_KEY, WX_LAT or WX_LON` | You started Node-RED without setting your key and location | Close the PowerShell window, open a new one, and repeat Step 5 |
| Message: `HTTP 401` | The weather service does not accept your key (yet) | Check you pasted the whole key. A new key can take up to a couple of hours to work |
| Weather and forecast cards are empty or say "stale", but the local sensor card works | Weather data could not be fetched | Check your internet and your key, then wait a few minutes |
| Message that port 1880 is already in use | Node-RED is already running somewhere | Close the other PowerShell window that is running it, then try again |
| Numbers look odd or random | The local sensor is simulated in this version | This is expected. See the note near the top |

---

## Good to know

- **The advice is a simple prototype.** The numbers that trigger warnings are
  example values, not official safety limits. The Recommendations card is
  general guidance and is **not medical advice**.
- **UV index and air quality are not measured** by this project.
- **Your key and location stay on your computer.** They are never saved into
  the project files, so they do not appear on GitHub.
- **The project folder is safe to update.** Run `git pull` to get new versions,
  then repeat Step 6 if the flows changed (import again and Deploy).

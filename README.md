# UC3M Sigma Seat Checker (UI.Vision)

A small automation project using the [UI.Vision RPA](https://ui.vision/) Chrome extension to monitor seat availability on the **SIGMA UC3M** enrollment portal and automatically grab a seat when one becomes free.

Originally created to track seats for the course `18268 – Artificial Intelligence` at **Universidad Carlos III de Madrid**.

## Features

- Opens the SIGMA "Modify Request" page.
- Fills in the course code (e.g. `18268`).
- Reads the current number of available seats from the course table.
- Detects changes in the seat count and plays an alarm sound.
- If a seat is available (`seats > 0`), the macro:
  - Expands the course row
  - Clicks the "add course" button
  - Confirms the enrollment
  - Plays a confirmation sound and shows an alert: `🔥 SEAT CAPTURED!`
  - Stops the macro

## Requirements

- Google Chrome (or a Chromium-based browser)
- [UI.Vision RPA extension](https://chrome.google.com/webstore/detail/uivision-rpa/) installed
- A valid UC3M SIGMA account

## Installation

1. **Clone this repository:**

   ```bash
   git clone https://github.com/<your-username>/uc3m-seat-checker-uivision.git
   cd uc3m-seat-checker-uivision
   ```

2. **Install the UI.Vision RPA Extension**

   UI.Vision works on Chrome, Brave, Edge and other Chromium browsers.

   Download: [https://ui.vision/](https://ui.vision/)

3. **Import the macro**

   - Open UI.Vision
   - Go to **File → Import**
   - Select the file: `macros/artificial_intelligence_seat.json`

   The macro will now appear in your UI.Vision macro list.

## ⚙️ Configuration

### Changing the course code

Inside the macro, find the command:

| Command | Target             | Value   |
|---------|--------------------|---------|
| `type`  | `id=_asignatura`   | `18268` |

Change `18268` to any UC3M course code you want to track (e.g. `18262`, `20543`, etc.).

### Changing the seat table XPath (if SIGMA updates UI)

The macro reads seats using:

```
xpath=//*[@id="taulaAsigsOferta"]/tbody/tr[1]/td[10]
```

If SIGMA changes layout, update the XPath to match the seat column of the first row.

## 🔁 How It Works (Logic Overview)

1. Initialize `oldSeats = 0`
2. Enter infinite loop:
   1. Load SIGMA page
   2. Input course code
   3. Wait for table to load
   4. Read current number of available seats (`seats`)
   5. If `seats != oldSeats`:
      - Play alarm sound
      - Print message
      - Update `oldSeats`
   6. If `seats > 0`:
      - Expand course row
      - Click "add course"
      - Confirm enrollment
      - Play success sound
      - Display alert
      - **Stop the macro**
   7. Wait 1 second
   8. Repeat

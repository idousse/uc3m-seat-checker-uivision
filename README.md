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
- [UI.Vision RPA extension](https://chrome.google.com/webstore/detail/uivision-rpa/xpath_installer_id_here) installed
- A valid UC3M SIGMA account

## Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/<your-username>/uc3m-seat-checker-uivision.git
   cd uc3m-seat-checker-uivision

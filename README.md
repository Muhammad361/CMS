
# Clinic Management System - Nurse Module

## Description
This is the Nurse module of a Python-based Clinic Management System (CMS). It allows nurses to:
- View doctor appointments
- Record patient observations (blood pressure, pulse, temperature)
- View prescriptions for patients
- Administer medicine and log it
- Add patient details (extra functionality)

All data is stored using JSON-formatted `.txt` files.

## How to Run
1. Ensure you have Python 3 installed.
2. Place the following files in the same directory:
   - `nurse.py`
   - `appointments.txt`
   - `observations.txt`
   - `prescriptions.txt`
   - `medication_log.txt`
   - `patients.txt`
3. Open a terminal or command prompt and navigate to the project directory.
4. Run the program using:
   ```bash
   python3 nurse.py
   ```
5. Enter the correct nurse password when prompted (default is: `nurse123`).
6. Follow the menu to perform nurse operations.

## Sample Login
Password: `nurse123`

## Sample Patient IDs
- 255 (Muhammad Ali)
- 256 (Amina Yusuf)

## Notes
- All data is read/written from `.txt` files using JSON.
- You can manually edit these files to add more data or start with the provided samples.

## Developer
Group CMS - Nurse Module by Abdurahman Yunis

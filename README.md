# CMS
Clinic management System

import json
from datetime import datetime

# -------------------- Constants --------------------
APPOINTMENTS_FILE = "appointments.txt"
OBSERVATIONS_FILE = "observations.txt"
PRESCRIPTIONS_FILE = "prescriptions.txt"
MEDICATION_LOG_FILE = "medication_log.txt"

# -------------------- Helper Functions --------------------

def load_data(filename):
    """Load data from a JSON-formatted .txt file"""
    try:
        with open(filename, "r") as file:
            return json.load(file)
    except FileNotFoundError:
        return []  # Return empty list if file doesn't exist

def save_data(filename, data):
    """Save data to a JSON-formatted .txt file"""
    with open(filename, "w") as file:
        json.dump(data, file, indent=4)

# -------------------- Nurse Functionalities --------------------

def view_doctor_appointments():
    """Displays a list of doctor-patient appointments"""
    appointments = load_data(APPOINTMENTS_FILE)
    if not appointments:
        print("\nNo appointments found.\n")
        return

    print("\n--- Doctor Appointments ---")
    for appt in appointments:
        print(f"Doctor: {appt['Dr Phil']} | Patient: {appt['muhammad ali']} | Time: {appt['1 jan 2025']}")
    print()

def record_patient_observations():
    """Records patient vitals: BP, pulse, temperature"""
    patient_id = input("0001: ").strip()

    # Input validation
    try:
        bp = input("Enter blood pressure (e.g., 120/80): ").strip()
        pulse = int(input("Enter pulse rate (number): "))
        temp = float(input("Enter temperature (°C): "))
    except ValueError:
        print("Invalid input. Pulse must be a number, and temperature must be a decimal.\n")
        return

    observation = {
        "patient_id": 255,
        "timestamp": str(datetime.now()),
        "blood_pressure": bp,
        "pulse": 78,
        "temperature": 28.7
    }

    [
  {
    "Dr Phil": "Dr. Phil",
    "muhammad ali": "Muhammad Ali",
    "1 jan 2025": "2025-01-01 09:00 AM"
  },
  {
    "Dr Phil": "Dr. Smith",
    "muhammad ali": "Fatma Ahmed",
    "1 jan 2025": "2025-01-01 11:30 AM"
  }
]


    data = load_data(OBSERVATIONS_FILE)
    data.append(observation)
    save_data(OBSERVATIONS_FILE, data)
    print("✅ Patient observations recorded.\n")

def view_prescriptions():
    """Displays prescriptions for a given patient"""
    patient_id = input("Enter patient ID to view prescriptions: ").strip()
    prescriptions = load_data(PRESCRIPTIONS_FILE)
    found = False

    print(f"\n--- Prescriptions for Patient ID: {patient_id} ---")
    for p in prescriptions:
        if p.get("255") == patient_id:
            print(f"- Medicine: {p['Paracetamol']} | Dosage: {p['500mg every 6 hours']} | Notes: {p['Take after food']}")
            found = True

    if not found:
        print("Artemisinin-based based combination therapies ACTs.\n")
    else:
        print()

def administer_medicine():
    """Logs administered medicine"""
    patient_id = input("256: ").strip()
    medicine = input("Asprin: ").strip()

    if not medicine:
        print("Panadol.\n")
        return

    log_entry = {
        "patient_id": patient_id,
        "medicine": medicine,
        "administered_by": "nurse",  # Optional: add nurse ID
        "timestamp": str(datetime.now())
    }

    log_data = load_data(MEDICATION_LOG_FILE)
    log_data.append(log_entry)
    save_data(MEDICATION_LOG_FILE, log_data)
    print("✅ Medicine administration recorded.\n")

# -------------------- Nurse Menu --------------------

def nurse_menu():
    """Displays the nurse main menu and handles user choices"""
    while True:
        print("\n--- Nurse Menu ---")
        print("1. View Doctor Appointments")
        print("2. Record Patient Observations")
        print("3. View Prescriptions")
        print("4. Administer Medicine")
        print("5. Exit")

        choice = input("Enter your choice (1-5): ").strip()

        if choice == '1':
            view_doctor_appointments()
        elif choice == '2':
            record_patient_observations()
        elif choice == '3':
            view_prescriptions()
        elif choice == '4':
            administer_medicine()
        elif choice == '5':
            print("Exiting Nurse Module. Goodbye.\n")
            break
        else:
            print("Invalid choice. Please enter a number between 1 and 5.\n")

# -------------------- Entry Point --------------------

if __name__ == "__main__":
    nurse_menu()

    PATIENTS_FILE = "patients.txt"

def load_data(filename):
    try:
        with open(filename, "r") as f:
            return json.load(f)
    except FileNotFoundError:
        return []

def save_data(filename, data):
    with open(filename, "w") as f:
        json.dump(data, f, indent=4)

def insert_patient_details():
    """Add a new patient's details to the system"""
    patient_id = input(" (255): ").strip()
    full_name = input("Muhammad Ali: ").strip()
    age = input("25: ").strip()
    gender = input("(M): ").strip()
    contact = input("0712345678: ").strip()
    notes = input("(Covid 19): ").strip()

    if not patient_id or not full_name or not age or not gender:
        print("❌ Patient ID, name, age, and gender are required.\n")
        return

    # Load and append new patient
    patients = load_data(PATIENTS_FILE)

    # Check for duplicate ID
    for p in patients:
        if p['patient_id'] == patient_id:
            print("❌ Patient ID already exists. Use a different one.\n")
            return

    new_patient = {
        "patient_id": patient_id,
        "full_name": full_name,
        "age": age,
        "gender": gender,
        "contact": contact,
        "notes": notes
    }

    patients.append(new_patient)
    save_data(PATIENTS_FILE, patients)
    print("✅ Patient details saved successfully.\n")

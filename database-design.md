# Database Design

## Tables before normalization

| Table | Columns |
|---|---|
| Patient | PatientID (PK), FullName, Gender, PhoneNumber |
| Clinic | ClinicID (PK), FullName, Location, BranchName |
| Doctor | DoctorID (PK), FullName, Specialty, WorkHours, ClinicID (FK) |
| Appointment | AppointmentID (PK), VisitDate, VisitType, Status, Duration, PatientID (FK), DoctorID (FK), ClinicID (FK) |
| Prescription | PrescriptionID (PK), Notes, AppointmentID (FK) |
| Medicine | MedicineID (PK), MedicineName, Description, Price |
| Billing | BillingID (PK), BillingDate, Discount, TotalPrice, AppointmentID (FK), ClinicID (FK) |
| Prescription_Details | PrescriptionID (PK, FK), MedicineID (PK, FK), Dosage |
| Clinic_Inventory | ClinicID (PK, FK), MedicineID (PK, FK), StockQuantity |

The two many-to-many relationships became their own tables, and the one-to-many relationships got a foreign key on the "many" side.

## Normalization

**1NF:** all values are single values, nothing repeats in a row.

**2NF:** no partial dependencies. In the two tables with a composite key, Dosage and StockQuantity depend on the whole key.

**3NF:** there were two transitive dependencies:

- Appointment: AppointmentID -> DoctorID -> ClinicID
- Billing: BillingID -> AppointmentID -> DoctorID -> ClinicID

The clinic is already known from the doctor, so `ClinicID` was removed from both Appointment and Billing.

## Final tables

| Table | Columns |
|---|---|
| Patient | PatientID (PK), FullName, Gender, PhoneNumber |
| Clinic | ClinicID (PK), FullName, Location, BranchName |
| Doctor | DoctorID (PK), FullName, Specialty, WorkHours, ClinicID (FK) |
| Appointment | AppointmentID (PK), VisitDate, VisitType, Status, Duration, PatientID (FK), DoctorID (FK) |
| Prescription | PrescriptionID (PK), Notes, AppointmentID (FK) |
| Medicine | MedicineID (PK), MedicineName, Description, Price |
| Billing | BillingID (PK), BillingDate, Discount, TotalPrice, AppointmentID (FK) |
| Prescription_Details | PrescriptionID (PK, FK), MedicineID (PK, FK), Dosage |
| Clinic_Inventory | ClinicID (PK, FK), MedicineID (PK, FK), StockQuantity |

To get the clinic of an appointment or a bill, join through Doctor.

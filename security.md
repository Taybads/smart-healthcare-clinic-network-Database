# Security

## Authentication

Each user logs in with their own username and password. No shared accounts.

## Authorization

Permissions are given to roles, and each user gets a role.

| Role | Access |
|---|---|
| Doctor | Patients, appointments, prescriptions, medicines |
| Billing staff | Billing only |
| Admin staff | Clinics, doctors, medicines, inventory |
| Patient | Own appointments and prescriptions (read only) |

| Table | Doctor | Billing | Admin | Patient |
|---|:---:|:---:|:---:|:---:|
| Patient | Read/Write | - | Read | - |
| Doctor | Read | - | Read/Write | - |
| Clinic | Read | - | Read/Write | - |
| Appointment | Read/Write | - | Read | Read (own) |
| Prescription | Read/Write | - | - | Read (own) |
| Medicine | Read | Read | Read/Write | - |
| Clinic_Inventory | Read | - | Read/Write | - |
| Billing | - | Read/Write | Read/Write | - |

## Encryption

- In transit: SSL/TLS between the app and the database
- At rest: sensitive fields like phone numbers and medical notes are encrypted
- Passwords are stored as hashes, not plain text

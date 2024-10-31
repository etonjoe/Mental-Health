# Mental-Health
## Data Design in Mental Health System

Designing a database and data warehouse for a mental health system requires multiple aspects such as 
+ Patient management
+ Therapy sessions
+ Diagnoses
+ Treatment plans
+ Medications
+ Mental health professionals, and
+ Outcomes monitoring

Here's an approach for the database (for day-to-day operations) and the data warehouse (for analytics and reporting).
<details>
<summary> 
  
### 1. Database Design (OLTP - Online Transaction Processing)
</summary>
The database will support transactional operations for the mental health system. Below are key entities and their relationships:

### Entities:
#### 1. Patient:

  + PatientID (PK)
  + FirstName
  + LastName
  + DateOfBirth
  + Gender
  + ContactInfo
  + EmergencyContact
  + RegistrationDate

#### 2. Mental Health Professional:

  + ProfessionalID (PK)
  + FirstName
  + LastName
  + Specialty (e.g., psychologist, psychiatrist, counselor)
  + LicenseNumber
  + ContactInfo  
    
#### 3. Appointment:

   + AppointmentID (PK)
   + PatientID (FK)
   + ProfessionalID (FK)
   + AppointmentDate
   + AppointmentTime
   + Notes
#### 4. Diagnosis:

   + DiagnosisID (PK)
   + PatientID (FK)
   + ProfessionalID (FK)
   + DiagnosisDate
   + DiagnosisCode (ICD-10/DSM-5)
   + DiagnosisDescription
#### 5. TreatmentPlan:

   + TreatmentPlanID (PK)
   + PatientID (FK)
   + PlanDescription
   + StartDate
   + EndDate
   + ReviewDate
#### 6. Session/TherapyRecord:

   + SessionID (PK)
   + PatientID (FK)
   + ProfessionalID (FK)
   + SessionDate
   + SessionType (e.g., CBT, group therapy)
   + SessionDuration
   + Notes
#### 7. Medication:

   + MedicationID (PK)
   + MedicationName
   + Dosage
   + SideEffects
   + PatientID (FK)
   + ProfessionalID (FK)
   + PrescriptionDate
#### 8. Billing:

   + BillingID (PK)
   + PatientID (FK)
   + AppointmentID (FK)
   + BillingAmount
   + InsuranceDetails
   + PaymentStatus
   + PaymentDate
#### 9. OutcomeAssessment:

   + AssessmentID (PK)
   + PatientID (FK)
   + AssessmentDate
   + AssessmentTool (e.g., PHQ-9, GAD-7)
   + Score

#### Relationships:
 + A **Patient** can have multiple **Appointments**.
 + An **Appointments** is associated with a single Mental Health Professional.
 + A **Patient** can have multiple **Diagnoses**.
 + A **Patient** can have one or more **Treatment Plans**.
 + A Treatment Plan can consist of several **Sessions** and **Medications**.
 + A **Patient** can be assessed using several **OutcomeAssessments** over time.
 </details>
 <details>
   <summary>
     
  ### 2. Data Warehouse Design (OLAP - Online Analytical Processing)
   </summary>
   The data warehouse will store aggregated and historical data to facilitate reporting, analysis, and decision-making.

## **Fact Tables:**
### 1. FactAppointment:
  + AppointmentID (PK)
  + PatientID (FK)
  + ProfessionalID (FK)
  + AppointmentDate
  + AppointmentTime
  + AppointmentDuration
  + Notes
### 2. FactDiagnosis:
  + DiagnosisID (PK)
  + PatientID (FK)
  + ProfessionalID (FK)
  + DiagnosisDate
  + DiagnosisCode
  + DiagnosisDescription

### 3. FactTreatmentPlan:
  + TreatmentPlanID (PK)
  + PatientID (FK)
  + StartDate
  + EndDate
  + TreatmentPlanType
### 4. FactSession:
  + SessionID (PK)
  + PatientID (FK)
  + ProfessionalID (FK)
  + SessionDate
  + SessionType
  + SessionDuration
### 5. FactMedication:
  + MedicationID (PK)
  + MedicationName
  + Dosage
  + PrescriptionDate
  + SideEffects
### 6. FactBilling:
  + BillingID (PK)
  + PatientID (FK)
  + AppointmentID (FK)
  + BillingAmount
  + PaymentStatus
  + PaymentDate
### 7. FactOutcomeAssessment:
  + AssessmentID (PK)
  + PatientID (FK)
  + AssessmentTool
  + Score
  + AssessmentDate

### Dimension Tables:
### 1. DimPatient:
  + PatientID (PK)
  + FullName
  + Gender
  + Age
  + ContactInfo
  + EmergencyContact

### 2. DimProfessional:
  + ProfessionalID (PK)
  + FullName
  + Specialty
  + ContactInfo

### 3. DimTime:
  + TimeID (PK)
  + Date
  + Month
  + Quarter
  + Year

### 4. DimSessionType:
  + SessionTypeID (PK)
  + SessionType (e.g., CBT, Family Therapy)

### 5. DimDiagnosisCode:
  + DiagnosisCode (PK)
  + DiagnosisDescription
  + ICD-10/DSM-5 Code

### 6. DimMedication:
  + MedicationID (PK)
  + MedicationName
  + Dosage
  + SideEffects
 </details>
<details>
   <summary>
     
  ### 3. ETL Process (Extract, Transform, Load)
  </summary>
  
  + **Extract**: Data is extracted from the operational database (OLTP) at regular intervals. 
  + **Transform**: Clean, normalize, and transform the data (e.g., summarizing, categorizing, calculating derived metrics).
  + **Load**: Load the transformed data into the data warehouse (OLAP).
 </details>
 
   <details>
   <summary>

  ### 4. Example Queries for the Data Warehouse
  </summary>
 </details>

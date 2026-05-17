# 📊 Excel to SharePoint Automated Sync Flow

## 📌 Overview
This project demonstrates a Power Automate solution that automatically synchronizes data between an Excel file and a SharePoint list on a daily basis.
The flow ensures that all records remain consistent across both systems by reflecting new entries as well as updates made to existing records.

---

## ⚙️ Tools & Connectors
- Power Automate (Cloud Flow)
- Excel Online (Business)
- SharePoint

---

## 🔄 Flow Logic

### 🟢 Trigger
- Scheduled flow (runs daily)

### 🟢 Step 1: Read Excel Data
- Uses **"List rows present in a table"**

### 🟢 Step 2: Get items (SharePoint)
- Iterates through each row using **Apply to Each**

### 🟢 Step 3: Condition (Check if item exists)
- Expression - length(outputs('Get_items')?['body/value']) > 0

IF YES
   Apply to each
      → Delete existing item
      → Create new item
  
IF NO
   → Create new item

---

## 🔄 Data Synchronization Strategy
Instead of using a traditional update approach, a **delete-and-recreate strategy** was implemented:
1. Identify matching records in the SharePoint list using a unique key  
2. Delete existing entries  
3. Recreate records with the latest data from Excel  

## 💡 Why This Approach?
Using the standard "Update item" action introduced multiple challenges:
- Date format mismatches between Excel and SharePoint
- Complex field-level comparison logic
- Inconsistent updates for modified records

The delete-and-recreate strategy:
- Simplified the flow logic
- Eliminated data mismatch issues
- Ensured consistent and reliable data output on every run

---

## ⚠️ Challenges Faced

### 📅 Date Column Handling
- Differences in date formats between Excel and SharePoint caused update failures
- Required consistent formatting using expressions like:
```plaintext
formatDateTime(item()?['DateColumn'], 'yyyy-MM-dd')

---

✅ Outcome
  - Automated data sync
  - Resolved date formatting issues
  - Improved reliability using Delete + Create approach
  - Successfully handled large datasets

  <img width="1367" height="801" alt="image" src="https://github.com/user-attachments/assets/9b1406fe-6d2f-47b3-9be3-3e41db67a9f3" />

  <img width="852" height="628" alt="image" src="https://github.com/user-attachments/assets/0d9cce55-c554-4a7a-9a91-90c6490bf7f3" />


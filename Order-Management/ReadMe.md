# Workflow – Automated Order Processing & Reporting

## 📌 Problem Statement
Managing order workflows manually can be time-consuming and error-prone. Teams often need to filter specific orders, track processing status, assign employees, and generate weekly summaries. Without automation, this creates bottlenecks in reporting, inefficient updates, and delayed communication between ERP systems, databases, and team channels.

This workflow solves that problem by:
- **Fetching order data** from an ERP system.
- **Filtering records** based on conditions (e.g., order status = "processing" and employee name = "Mario").
- **Storing validated records** in Airtable for structured tracking.
- **Computing weekly order stats** (total booked orders and total booked sum).
- **Sending automated reports** to a Discord channel for team visibility.

---

## ⚙️ Workflow Overview
This project uses [n8n](https://n8n.io/) to automate order management and reporting.  

### Key Steps:
1. **Schedule Trigger** – Runs weekly (Monday at 9 AM).
2. **HTTP Request** – Fetches orders from the ERP system with authentication headers.
3. **Conditional Check (If Node)** – Ensures only orders with `orderStatus = "processing"` and `employeeName = "Mario"` move forward.
4. **Set Node (Edit Fields)** – Extracts and maps fields like `orderID` and `employeeName`.
5. **Airtable Integration** – Creates a record in the `processingOrders` table.
6. **Code Node** – Aggregates total orders and total booked value.
7. **Discord Notification** – Posts a weekly summary message with total booked orders and their value.

---

## 🛠️ Tech Stack
- **[n8n](https://n8n.io/)** – Workflow automation platform.
- **ERP System API** – Source of order data.
- **Airtable** – For structured order record storage.
- **Discord** – For automated team notifications.

---



# Creating Core List Views for Incidents

## Overview
This repository demonstrates how to configure a custom Incident list view and application menu structure in ServiceNow to support monitoring HHD (Holographic Handheld Devices) incidents and inquiries.

The focus is on extending the Incident table with a custom field, building a targeted list view using dot-walked Configuration Item data, and exposing that view through a custom application and module for easier access by product managers.

This project simulates how ServiceNow administrators tailor list views and navigation to support specific business products.

## Use Case
HHD product managers require a centralized way to view and monitor incidents related to Holographic Handheld Devices. These incidents must be clearly identifiable, include device-level details such as Model ID and Install Status, and be accessible from a dedicated application menu.

This project demonstrates how ServiceNow supports product-focused incident visibility without modifying core Incident functionality.

## Features
- Custom field creation on the Incident table
- Targeted Incident list view configuration
- Dot-walking to display Configuration Item attributes
- Custom application menu creation
- Custom module configuration with filtered list access
- Role-based visibility using ITIL permissions

## Technologies Used
- ServiceNow Platform
- IT Service Management (ITSM)
- Incident Management
- Application Menus
- List Views
- Configuration Management Database (CMDB)

## Implementation Walkthrough

### Objective
Create a custom Incident list view and application menu structure that allows HHD stakeholders to easily view and monitor relevant incidents and inquiries.

### Step 1: Add the Pilot Field to the Incident Table
A new True/False field named **Pilot** was added to the Incident table to identify incidents associated with pilot deployments.

The field was configured with a default value of **false** to ensure consistency across new records.

<img width="1897" height="666" alt="Screen Shot 2026-01-29 at 6 24 15 PM" src="https://github.com/user-attachments/assets/0a38a6be-cbcf-4d96-82ae-63f9c6b633bd" />

### Step 2: Create the HHD List View
A new list view named **HHD** was created on the Incident table to support targeted monitoring.

The view was configured to display the following columns in order:

- Number  
- Pilot  
- Category  
- Opened  
- Configuration item  
- Configuration item.Model ID  
- Configuration item.Install Status  
- Short description  
- Caller  
- State

<img width="1897" height="677" alt="Screen Shot 2026-01-29 at 6 38 19 PM" src="https://github.com/user-attachments/assets/9813d492-6779-471d-8ca0-ad3dfb80eeb8" />

The **Model ID** and **Install Status** fields were added using dot-walking from the Configuration Item reference, eliminating the need for duplicate fields on the Incident table.

### Step 3: Verify the HHD View
The list was switched to the **HHD** view to confirm the view label and column order displayed correctly.

This validated that the list view met business requirements for visibility and accuracy.

<img width="1900" height="220" alt="Screen Shot 2026-01-29 at 6 40 24 PM" src="https://github.com/user-attachments/assets/46dea827-4e81-4708-8d96-d8885c11afbc" />

## Section 2: Configure Application Menu Access

### Objective
Expose the HHD Incident list through a dedicated application and module for simplified navigation.

### Step 4: Create the HHD Application Menu
A new application menu named **HHD** was created under Custom Applications.

The menu was configured with:
- Role restriction: **itil**
- Descriptive hint: *Holographic Handheld Devices*

This ensures only authorized users can access the application.

### Step 5: Create the Incidents and Inquiries Module
A new module named **Incidents and Inquiries** was added under the HHD application.

The module was configured to:
- Display a **List of Records**
- Target the **Incident** table
- Use the **HHD** list view
- Apply a filter where **Service offering contains HHD**

This configuration ensures only relevant incidents are displayed.

<img width="1915" height="808" alt="Screen Shot 2026-01-29 at 6 49 20 PM" src="https://github.com/user-attachments/assets/e6e4ed5e-018d-4e2b-921d-299709c8dee0" />

### Step 6: Validate Application Navigation
The HHD application and **Incidents and Inquiries** module were verified to be visible in the **All** menu.

Selecting the module opened the Incident list using the HHD view. Since no HHD incidents existed at the time, the list displayed as empty, confirming correct filtering behavior.

<img width="1915" height="237" alt="Screen Shot 2026-01-29 at 6 51 57 PM" src="https://github.com/user-attachments/assets/c80b742b-52e9-4c92-9462-108811e6ad73" />

<img width="1915" height="425" alt="Screen Shot 2026-01-29 at 6 53 18 PM" src="https://github.com/user-attachments/assets/fe7e9d65-80a1-4077-ae52-ee59f8bedcb4" />

## Lessons Learned
- Custom list views allow ServiceNow to support product-specific monitoring needs
- Dot-walking enables visibility into related CI attributes without schema changes
- Application menus improve usability for non-technical stakeholders
- Role-based access ensures controlled visibility of operational data
- List view configuration is a powerful tool for aligning ITSM with business structure

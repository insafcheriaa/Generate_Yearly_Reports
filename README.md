# Generate Yearly Report Automation 
The Generate Yearly Report Automation project is designed to automate the yearly reporting process for vendors in the ACME System 1 web application. Using UiPath ReFramework, this automation streamlines the retrieval of monthly reports, consolidation into yearly summaries, and updating system statuses, reducing manual effort and enhancing process accuracy.


## Key Features  
### Dispatcher:
1. **Web Login and Navigation**: Automates login to the ACME System 1 platform and navigation to the Work Items page.  
2. **Data Extraction**: Retrieves Work Items and filters those of type **WI4** (Generate Yearly Report for Vendor).  
3. **Queue Creation**: Adds filtered Work Items to a UiPath Orchestrator Queue for processing.  

### Performer:
1. **Data Processing**: Processes each transaction from the Orchestrator Queue.  
2. **Report Consolidation**:  
   - Downloads all monthly reports for a vendor.  
   - Consolidates them into a single Excel file named `Yearly-Report-[Year]-[VendorTaxID].xlsx`.  
3. **Report Upload**: Uploads the yearly report back to the ACME System 1 platform and retrieves a unique upload ID.  
4. **Status Update**: Updates the Work Item status to **Completed**, adding a comment with the upload ID.  


## Prerequisites  
- **Software**: UiPath Studio, Microsoft Excel, and a browser where UiPath Orchestrator is accessible.  
- **Access**: ACME System 1 credentials with permissions to access and update Work Items.  


## Getting Started  

### 1. Software and Environment Setup  
- Install UiPath Studio and ensure the following packages are installed:  
  - **UiPath.System.Activities**  
  - **UiPath.UIAutomation.Activities**  
  - **UiPath.Excel.Activities**  
  - **UiPath.Orchestrator API Activities**  

- Configure UiPath Orchestrator and create a queue named `Generate_Yearly_Report`.  

### 2. Configure the Project  
- Clone this repository and open the project in UiPath Studio.  
- Edit the `Config.xlsx` file to include:  
  - Orchestrator Queue Name  
  - ACME System 1 credentials stored as Assets in Orchestrator or Windows Credential Manager.
  - Reset the necessary variables (Dispatcher : email, password.Performer : QueueName, QueuePath, DownloadPath, FilePath)

### 3. Run the Automation  
1. **Run Dispatcher**:  
   - Initializes the environment and populates the Orchestrator queue with Work Items of type **WI4**.  

2. **Run Performer**:  
   - Processes each transaction, downloads reports, generates yearly summaries, uploads them, and updates the system.  


## Exceptions and Error Handling  
- **Invalid Credentials**: Sends an email notification to the support team.  
- **Missing Monthly Reports**: Skips missing months and proceeds with available data.  
- **Application Unresponsive**: Retries the operation up to two times before failing gracefully.  


## Additional Resources  
- [ReFramework Documentation](https://docs.uipath.com/studio/docs/robotic-enterprise-framework)  
- [UiPath Orchestrator Documentation](https://docs.uipath.com/orchestrator/docs)  


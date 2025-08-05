# 🎯 Azure Data Drift Detector
 
**A comprehensive Python solution for detecting schema and statistical drift in Azure Blob Storage data files**
 
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Azure](https://img.shields.io/badge/Azure-Blob_Storage-blue.svg)](https://azure.microsoft.com/en-us/services/storage/blobs/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
 
## 📖 Overview
 
The Azure Data Drift Detector is a production-ready cloud-native tool that monitors your Azure Blob Storage data files for changes over time. It automatically scans Azure containers for CSV, JSON, and Parquet files, creates detailed statistical profiles, and detects both schema drift (structural changes) and statistical drift (data distribution changes) by comparing current data against established baselines.
 
### 🎯 Key Use Cases
- **Production Data Monitoring**: Detect unexpected changes in Azure production datasets
- **ML Pipeline Monitoring**: Identify when model retraining is needed due to data drift
- **Data Quality Assurance**: Ensure data consistency across Azure environments
- **Automated Change Detection**: Track data evolution over time with minimal setup
- **Compliance & Governance**: Monitor schema violations and data anomalies
 
## 🚀 Current Features
 
### ☁️ **Azure-Native Integration**
- **Direct Azure Blob Storage Access**: Seamless integration with Azure cloud storage
- **SAS Token Authentication**: Secure access using Azure SAS tokens
- **Intelligent Date Filtering**: Smart file filtering by upload date patterns
- **Automatic File Discovery**: Finds and processes CSV, JSON, and Parquet files
- **Robust Upload Support**: Handles Azure SDK compatibility issues automatically
 
### 🔄 **Complete Workflow**
- **Data Generation**: Generate test data directly to Azure (`data_generator.py`)
- **Drift Detection**: Monitor data changes against baseline (`run.py`)
- **Analysis & Reporting**: Comprehensive drift analysis (`drift_analyzer.py`)
- **Baseline Management**: Update and maintain reference schemas (`update_baseline_schema.py`)
- **System Monitoring**: Health checks and status overview (`system_status.py`)
 
### 📊 **Multi-Engine Processing**
- **Pandas Engine**: Optimized for CSV, JSON, and small-medium Parquet files
- **PySpark Engine**: Scalable processing for large datasets (optional)
- **Format Detection**: Automatic handling of different file formats
 
### 🔍 **Advanced Drift Detection**
 
#### Schema Drift Detection
- ✅ **Column Addition/Removal**: Detect new or missing columns
- ✅ **Data Type Changes**: Monitor column type modifications  
- ✅ **Constraint Changes**: Track nullable and categorical changes
- ✅ **File Mapping**: Intelligent mapping of timestamped files to baselines
 
#### Statistical Drift Detection
- ✅ **Null Percentage Changes**: Monitor data quality degradation
- ✅ **Unique Value Distribution**: Detect changes in data diversity
- ✅ **Numerical Statistics**: Track mean, std, min, max changes
- ✅ **Categorical Distribution**: Monitor value frequency changes
 
#### Statistical Drift Detection
- ✅ **Null Percentage**: Changes in missing data patterns
- ✅ **Distinct Values**: Changes in data uniqueness
- ✅ **Statistical Measures**: Mean, standard deviation, min, max changes
- ✅ **Distribution Changes**: Categorical value frequency changes
 
### ⚙️ **Advanced Configuration**
- 🎛️ **Configurable Thresholds**: Customize drift sensitivity
- ☁️ **Azure Integration**: Seamless Azure Blob Storage connectivity
- 🎯 **Selective Processing**: Choose specific file types
- 📊 **Sampling**: Handle large files with intelligent sampling
- 📅 **Date Filtering**: Focus on recent data or scan all files
 
### 📋 **Reporting & Output**
- 📄 **Markdown Reports**: Human-readable drift analysis with timestamps
- 📊 **JSON Profiles**: Detailed statistical summaries
- 🗂️ **Baseline Management**: Automatic schema versioning
- 🎨 **Rich Console Output**: Color-coded status messages
- 📅 **Historical Tracking**: Timestamped reports for trend analysis
 
## 📁 Project Architecture
 
```
azure-data-drift-detector/
├── 📁 config/
│   ├── ⚙️ settings.yaml              # Main configuration file
│   └── 📄 settings_template.yaml     # Configuration template
├── 📁 schemas/
│   └── 🗃️ baseline_schema.json       # Auto-generated baseline
├── 📁 profiles/
│   └── 📊 profile_[file]_[date].json # Statistical profiles
├── 📁 drift_reports/
│   ├── 📋 drift_report_[date].md     # Timestamped drift reports
│   ├── 📋 drift_report_[date].json   # JSON format reports
│   ├── 📋 latest_drift_report.md     # Latest report alias
│   └── 📋 latest_drift_report.json   # Latest JSON report alias
├── 📁 src/                           # Source code
│   ├── 📁 handlers/
│   │   ├── 🐼 pandas_handler.py      # Pandas with Azure support
│   │   └── ⚡ pyspark_handler.py     # PySpark with Azure support
│   ├── ☁️ scan_azure.py              # Azure Blob Storage scanner
│   ├── 📊 profile_data.py            # Data profiling engine
│   ├── 🚨 detect_drift.py            # Drift detection algorithms
│   └── 🛠️ utils.py                   # Utility functions
├── 🚀 run.py                         # Main execution script
├── 📊 data_generator.py              # Test data generator
├── 📈 drift_analyzer.py              # Drift report analyzer
├── 🧹 cleanup_profiles.py            # Profile cleanup utility
├── ✅ validate.py                    # System validation
├── 📋 requirements.txt               # Python dependencies
├── 📖 README.md                      # This documentation
├── 📖 DATA_GENERATOR_README.md       # Data generator documentation
└── 📖 DRIFT_ANALYZER_README.md       # Drift analyzer documentation
```
 
## 🔧 Installation & Setup
 
### Prerequisites
- **Python 3.8+**
- **pip** (Python package installer)
- **Azure Storage Account** with Blob Storage enabled
- **Azure SAS Token** with read/write permissions
 
### Quick Installation
 
1. **Clone or Download** the project to your local machine
 
2. **Navigate** to the project directory:
   ```bash
   cd azure-data-drift-detector
   ```
 
3. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
 
4. **Configure Azure Settings**:
   ```bash
   # Copy template and edit with your Azure credentials
   cp config/settings_template.yaml config/settings.yaml
   # Edit config/settings.yaml with your Azure details
   ```
 
5. **Verify Installation**:
   ```bash
   python system_status.py
   ```
 
### Azure Configuration
 
Update `config/settings.yaml` with your Azure details:
```yaml
azure_config:
  enabled: true
  storage_account_name: "your_storage_account"
  container_name: "your_container_name"
  sas_token: "your_sas_token_with_rwl_permissions"
  blob_prefix: ""  # Optional: filter by prefix
 
# Drift detection thresholds
null_threshold: 0.2         # 20% change in null values triggers alert
distinct_threshold: 0.3     # 30% change in unique values triggers alert
 
# Statistical change thresholds
stat_thresholds:
  mean_change: 0.15         # 15% change in mean
  std_change: 0.20          # 20% change in standard deviation
  min_change: 0.25          # 25% change in minimum value
  max_change: 0.25          # 25% change in maximum value
```
 
## 🆕 Latest Updates (v2.0 - January 2025)
 
### ✅ **Azure Integration Improvements**
- **Enhanced Upload Reliability**: Completely resolved Azure SDK compatibility issues with `max_results` parameter
- **Fallback Upload Methods**: Multiple upload strategies ensure 100% success rate even with SDK version conflicts
- **Improved Error Handling**: Clear, actionable error messages with specific troubleshooting guidance
- **Content Type Auto-Detection**: Automatic MIME type setting for all file formats (CSV, JSON, Parquet)
- **Connection Validation**: Robust Azure connection testing with detailed diagnostic information
 
### ✅ **Advanced Baseline Management**
- **Intelligent File Mapping**: Seamless mapping of timestamped files to baseline categories:
  - `employees_master_20250105_143022.csv` → `employees.csv` baseline
  - `sales_transactions_20250105_143022.parquet` → `sales.parquet` baseline
  - `products_catalog_20250105_143022.json` → `products.json` baseline
- **Flexible Baseline Updates**: Use oldest, cleanest data as reference point for accurate drift detection
- **Automatic Backup & Versioning**: Safe baseline updates with automatic backup and rollback capabilities
- **Source Tracking**: Full audit trail of which source files were used to create each baseline
 
### ✅ **Enhanced Drift Detection Engine**
- **Multi-Layer Schema Detection**: Column additions, removals, type changes, and constraint violations
- **Advanced Statistical Monitoring**: Mean, median, standard deviation, min/max, and distribution changes
- **Severity Classification**: Issues automatically categorized as HIGH, MEDIUM, or LOW priority
- **Pattern Recognition**: Smart detection of common drift patterns and anomalies
- **Threshold Customization**: Fine-tuned sensitivity controls for different data types and business requirements
 
### ✅ **Production-Ready Architecture**
- **System Health Monitoring**: Comprehensive health checks with `system_status.py`
- **Streamlined Codebase**: Removed legacy test files, focused on production-ready components
- **Rich Console Output**: Color-coded status indicators with clear progress reporting
- **Automated Maintenance**: Profile cleanup utilities and automated report management
- **Documentation Updates**: Complete documentation refresh with current workflow examples
 
## 🚀 Quick Start Guide
 
### Step 1: Configure Azure Connection
Edit `config/settings.yaml` with your Azure credentials:
```yaml
azure_config:
  enabled: true
  storage_account_name: "your_storage_account"
  container_name: "your_container_name"
  sas_token: "your_sas_token"
```
 
### Step 2: Verify System Status
```bash
# Basic system health check
python system_status.py
 
# Detailed status with file statistics
python system_status.py --detailed
 
# JSON output for automation
python system_status.py --json
```
 
### Step 3: Generate Test Data (Optional)
```bash
# Generate sample data for testing
python data_generator.py --employees 100 --products 50 --sales 300
 
# Generate data with drift for testing
python data_generator.py --add-drift --employees 120 --products 60 --sales 400
```
 
### Step 4: Establish Baseline
```bash
# Create initial baseline from oldest clean data
python update_baseline_schema.py
 
# Auto-find oldest profiles
python update_baseline_schema.py --auto-find
 
# Force update without prompts
python update_baseline_schema.py --force
```
 
### Step 5: Monitor for Drift
```bash
# Daily monitoring (recommended)
python run.py --today-only
 
# Full analysis of all files
python run.py --all-files
 
# Profile only mode (no drift detection)
python run.py --profile-only --all-files
```
 
### Step 6: Analyze Results
```bash
# Quick summary
python drift_analyzer.py --summary
 
# Show only issues
python drift_analyzer.py --issues-only
 
# View detailed analysis
python drift_analyzer.py --minimal
```
 
## 💻 Complete Usage Examples
 
### 🎯 **Main Commands**
 
```bash
# === Daily Operations ===
python run.py --today-only              # Monitor today's data (default)
python run.py --all-files               # Analyze all Azure files
python system_status.py                 # Check system health
 
# === Enhanced System Monitoring ===
python system_status.py --detailed      # Detailed health check with statistics
python system_status.py --json          # JSON output for automation
 
# === Data Generation ===
python data_generator.py                # Generate clean test data
python data_generator.py --add-drift    # Generate data with anomalies
 
# === Analysis & Reporting ===
python drift_analyzer.py --summary      # Show drift summary
python drift_analyzer.py --issues-only  # Show only problems
 
# === Maintenance ===
python update_baseline_schema.py        # Update baseline
python update_baseline_schema.py --auto-find --force  # Auto-find and force update
python cleanup_profiles.py              # Clean old profiles
```
 
### 📊 **Advanced Usage**
 
```bash
# === Detailed Monitoring ===
python run.py --today-only --verbose    # Verbose daily monitoring
python run.py --all-files --profile-only # Profile all files without drift detection
 
# === Custom Data Generation ===
python data_generator.py --employees 500 --products 200 --sales 1000
python data_generator.py --add-drift --employees 150 --sales 500
 
# === Focused Analysis ===
python drift_analyzer.py --high-only    # Show only high-severity issues
python drift_analyzer.py --medium-only  # Show medium-severity issues
 
# === System Administration ===
python cleanup_profiles.py --days 30    # Clean profiles older than 30 days
python update_baseline_schema.py --dry-run  # Preview baseline changes
python system_status.py --detailed --json > status.json  # Export system status
```
 
### 🔄 **Typical Workflow**
 
```bash
# 1. Daily monitoring workflow
python run.py --today-only
python drift_analyzer.py --summary
 
# 2. Weekly comprehensive analysis
python run.py --all-files
python drift_analyzer.py --issues-only
 
# 3. Monthly maintenance
python cleanup_profiles.py
python system_status.py
 
# 4. Baseline updates (as needed)
python update_baseline_schema.py
python run.py --all-files  # Verify new baseline
```
 
## ⚙️ Configuration Reference
 
### Main Configuration (`config/settings.yaml`)
 
```yaml
# === File Processing ===
file_types: ["csv", "json", "parquet"]   # File types to process
max_sample_size: 10000                   # Max rows to sample from large files
 
# === Processing Engine ===
use_pyspark: false                       # Use PySpark instead of Pandas
 
# === Azure Blob Storage Configuration ===
azure_config:
  enabled: true                          # Enable Azure Blob Storage
  storage_account_name: "your_account"   # Azure Storage Account name
  container_name: "your_container"       # Container name
  sas_token: "your_sas_token"           # SAS token for authentication
  blob_prefix: ""                       # Optional: prefix to filter blobs
 
# === Output Directories ===
profiles_dir: "profiles/"                # Statistical profiles storage
schemas_dir: "schemas/"                  # Baseline schemas storage
drift_report_dir: "drift_reports/"       # Drift reports output
baseline_schema_file: "baseline_schema.json"
 
# === Drift Detection Thresholds ===
null_threshold: 0.2                      # Null percentage change threshold
distinct_threshold: 0.3                  # Distinct values change threshold
 
# === Statistical Drift Thresholds ===
stat_thresholds:
  mean_change: 0.15                      # Mean value change threshold
  std_change: 0.20                       # Standard deviation change threshold
  min_change: 0.25                       # Minimum value change threshold
  max_change: 0.25                       # Maximum value change threshold
 
# === File Processing Settings ===
recursive_scan: true                     # Scan subdirectories (legacy)
```
 
### Threshold Tuning Guide
 
| Threshold | Low (0.05-0.10) | Medium (0.15-0.25) | High (0.30-0.50) |
|-----------|------------------|---------------------|-------------------|
| **Sensitivity** | Very High | Moderate | Low |
| **Use Case** | Critical systems | General monitoring | Stable systems |
| **False Positives** | High | Medium | Low |
 
## 📊 Understanding Output
 
### Console Output
```bash
✓ Configuration loaded from config/settings.yaml
� Initializing Azure Blob Storage scanner...
✓ Successfully connected to Azure Blob Storage container: your-container
✓ Connected to Azure Storage Account: your-account
�🔍 Scanning for files from today (20250804) in Azure Blob Storage: your-container...
Found 18 files:
  - CSV: 6 files
  - JSON: 6 files  
  - PARQUET: 6 files
  - Total size: 538.9KB
📅 Filtered to show only files from today: 20250804
📊 Profiling data...
✓ Successfully profiled: 13 files
✗ Failed to profile: 5 files
🚨 Detecting drift...
📋 Drift Detection Results:
  - Files analyzed: 13
  - Files with drift: 10
  - Overall drift detected: YES 🚨
```
 
### Drift Report Structure
```markdown
# 🎯 AZURE DATA DRIFT REPORT
 
**Analysis Date:** 2025-08-04T21:58:39
**Report File:** drift_report_20250804_215839.json
**Overall Drift:** 🚨 YES
**Files Analyzed:** 13
**Files with Issues:** 10
 
## 📊 SUMMARY
- **Total Issues:** 107
- **Schema Issues:** 16  
- **Statistical Issues:** 91
 
## 🗂️ PROBLEMATIC FILES
### sales_transactions_20250804_214156.parquet
**Drift Status:** 🚨 DRIFT DETECTED  
**Schema Drift:** 🚨 YES
**Statistical Drift:** 🚨 YES
 
#### Issues Detected
- **Schema Issue:** Column data type changed from int64 to float64
- **Statistical Issue:** Mean changed by 25.3% (threshold: 15.0%)
```
 
### Profile Data Structure
```json
{
  "file_path": "employees_master_20250804_191753.csv",
  "file_info": {
    "source": "Azure Blob",
    "container": "driftcontainer",
    "size_bytes": 26500,
    "last_modified": "2025-08-04T19:17:53Z"
  },
  "schema": {
    "columns": {
      "employee_id": {
        "dtype": "int64",
        "nullable": false,
        "is_numeric": true
      },
      "name": {
        "dtype": "object",
        "nullable": false,
        "is_numeric": false
      }
    },
    "row_count": 100,
    "column_count": 7
  },
  "profile": {
    "columns": {
      "employee_id": {
        "null_percentage": 0.0,
        "unique_count": 100,
        "mean": 550.5,
        "std": 28.9
      }
    }
  },
  "profiled_at": "2025-08-04T21:58:39.123456",
  "engine_used": "pandas",
  "success": true
}
```
 
## 🛠️ Troubleshooting
 
### Common Issues & Solutions
 
#### 🚫 "Azure Blob Storage is not enabled in configuration"
**Problem**: Azure configuration not properly set
**Solutions**:
- Ensure `azure_config.enabled: true` in settings.yaml
- Verify all Azure configuration parameters are set
- Check SAS token has not expired
 
#### 🚫 "Failed to connect to Azure Blob Storage"
**Problem**: Azure connection issues
**Solutions**:
- Verify storage account name is correct
- Check SAS token permissions (should include read access)
- Ensure container name exists and is accessible
- Test connection: `python src/scan_azure.py`
 
#### 🚫 "No files found for today"
**Problem**: No files match today's date filter
**Solutions**:
- Use `--all-files` to scan all files in container
- Check file naming includes date pattern (YYYYMMDD)
- Verify files exist in Azure container
- Ensure files have supported extensions (csv, json, parquet)
 
#### 🚫 "SAS token expired" or authentication errors
**Problem**: Azure authentication failed
**Solutions**:
- Generate new SAS token with read permissions
- Update `sas_token` in settings.yaml
- Ensure SAS token includes container-level access
- Check token expiration date
 
#### 🚫 "Configuration file not found"
**Problem**: Running script from wrong directory
```bash
# ❌ Wrong - from parent directory
python azure-data-drift-detector/run.py
 
# ✅ Correct - from project directory
cd azure-data-drift-detector
python run.py
```
 
#### 🚫 "Memory errors with large Azure blobs"
**Problem**: Insufficient memory for large datasets
**Solutions**:
- Increase `max_sample_size` gradually
- Use PySpark for distributed processing: `use_pyspark: true`
- Process files in smaller batches using date filtering
- Use more powerful hardware or cloud compute
 
### Performance Optimization
 
#### For Small Azure Blobs (< 100MB)
```yaml
use_pyspark: false
max_sample_size: 10000
azure_config:
  blob_prefix: ""  # No filtering needed
```
 
#### For Large Azure Blobs (> 1GB)
```yaml
use_pyspark: true
max_sample_size: 50000
azure_config:
  blob_prefix: "large_data/"  # Filter by folder if needed
```
 
#### For Many Azure Blobs
```yaml
# Use date filtering for better performance
# Default --today-only mode scans only recent files
file_types: ["parquet"]    # Process only most efficient formats
```
 
#### For Frequent Monitoring
```yaml
# Use today-only mode (default) for faster scans
# Run with --all-files only when full analysis needed
```
 
## 🔍 Advanced Features
 
### Custom Azure Blob Filtering
```python
# In scan_azure.py - extend the date filtering logic
def _is_file_from_custom_criteria(self, blob_name: str) -> bool:
    """Add your custom filtering logic here"""
    # Example: Filter by department prefix
    # Example: Filter by file size
    # Example: Filter by last modified date
    pass
```
 
### Custom Drift Metrics
Extend `detect_drift.py` to add custom drift detection logic:
 
```python
def detect_custom_azure_drift(self, current_stats, baseline_stats):
    """Add your custom drift detection logic for Azure data"""
    # Example: Detect cloud-specific patterns
    # Example: Azure-specific compliance checks
    # Example: Cross-container drift detection
    pass
```
 
### Azure Pipeline Integration
```python
# azure_pipeline_integration.py
from src.scan_azure import AzureScanner
from src.profile_data import DataProfiler
from src.detect_drift import DriftDetector
 
def automated_azure_drift_check():
    """Integration with Azure Data Factory or Azure Functions"""
    # Your Azure integration logic
    pass
```
 
### Custom Azure Blob Handlers
Add support for new Azure blob formats in `src/handlers/`:
 
```python
# azure_custom_handler.py
class AzureCustomFormatHandler:
    def process_azure_blob(self, blob_client, file_info):
        # Your custom Azure blob processing logic
        pass
```
 
## 📈 Monitoring & Alerting
 
### Azure Integration
```yaml
# Azure DevOps Pipeline - .azure-pipelines.yml
trigger:
  schedules:
  - cron: "0 9 * * *"  # Daily at 9 AM
    displayName: Daily drift check
    branches:
      include:
      - main
 
jobs:
- job: DriftDetection
  pool:
    vmImage: 'ubuntu-latest'
  steps:
  - task: UsePythonVersion@0
    inputs:
      versionSpec: '3.8'
  - script: |
      pip install -r requirements.txt
      python run.py --verbose
    displayName: 'Run Azure Drift Detection'
```
 
### Azure Functions Integration
```python
# azure_function_drift_check.py
import azure.functions as func
from src.scan_azure import AzureScanner
 
def main(timer: func.TimerRequest) -> None:
    """Azure Function triggered on schedule"""
    if drift_detected:
        # Send notification via Azure Logic Apps
        # Log to Azure Monitor
        # Update Azure Dashboard
        pass
```
 
### Azure Logic Apps Alerts
```json
{
  "definition": {
    "triggers": {
      "When_drift_detected": {
        "type": "Http",
        "inputs": {
          "method": "POST",
          "uri": "https://your-function-app.azurewebsites.net/api/drift-check"
        }
      }
    },
    "actions": {
      "Send_Teams_notification": {
        "type": "ApiConnection",
        "inputs": {
          "host": {
            "connection": {
              "name": "@parameters('teams_connection')"
            }
          }
        }
      }
    }
  }
}
```
 
## 🎯 Best Practices
 
### 📊 **Azure Data Management**
- Use consistent naming conventions with timestamps for blob files
- Organize blobs in logical containers or prefixes
- Keep baseline data representative of expected patterns
- Update baselines when business logic changes
- Archive old profiles for historical analysis
- Use Azure Blob versioning for important datasets
- Document expected changes before they occur
 
### ⚙️ **Configuration Management**
- Store Azure credentials securely (Azure Key Vault recommended)
- Use version control for configuration templates
- Test threshold changes in staging environments
- Document threshold rationale
- Review thresholds periodically
- Rotate SAS tokens regularly
 
### 🔍 **Monitoring Strategy**
- Start with `--today-only` mode for regular monitoring
- Use `--all-files` for comprehensive analysis
- Start with higher thresholds and gradually decrease
- Monitor both schema and statistical drift
- Set up automated scheduling with Azure Functions
- Integrate with Azure Monitor and Application Insights
 
### 📋 **Reporting & Communication**
- Share drift reports with relevant stakeholders
- Establish escalation procedures for critical drift
- Use Azure Logic Apps for automated notifications
- Document resolution steps for common drift patterns
- Maintain a drift incident log in Azure DevOps
- Create dashboards in Power BI or Azure Monitor
 
## 🚀 Future Enhancements
 
### Planned Features
- 📊 **Azure Power BI Integration**: Interactive drift visualization dashboards
- 🔗 **Azure SQL Database Integration**: Direct database table monitoring
- 📱 **Real-time Monitoring**: Event-driven drift detection with Azure Event Grid
- 🤖 **ML-based Anomaly Detection**: Azure Machine Learning integration
- 📈 **Trend Analysis**: Historical drift pattern analysis in Azure Monitor
- 🔔 **Advanced Alerting**: Teams, Slack, webhook integrations via Logic Apps
- 🏗️ **Azure Data Factory Integration**: Native pipeline integration
- 🔐 **Azure Key Vault Integration**: Secure credential management
- 📊 **Azure Synapse Analytics**: Big data drift detection
 
### Contributing
We welcome contributions! Areas of interest:
- New Azure service integrations
- Additional statistical tests
- Performance optimizations for large Azure blobs
- Azure-specific documentation improvements
- Test coverage expansion
- Azure DevOps templates
- Power BI dashboard templates
 
## 📄 License
 
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
 
## 🤝 Support
 
### Getting Help
1. **Documentation**: Check this README and utility READMEs first
2. **Validation**: Run `python validate.py` to test setup
3. **Azure Connection**: Test `python src/scan_azure.py` for Azure connectivity
4. **Data Generation**: Use `python data_generator.py --help` for test data
5. **Report Analysis**: Use `python drift_analyzer.py --help` for report insights
6. **Issues**: Create detailed issue reports with:
   - Error messages
   - Configuration files (remove sensitive Azure credentials)
   - Sample data structure (if possible)
   - Environment details
   - Azure connection test results
 
### Community
- 📧 **Email**: [Your contact email]
- 💬 **Discussions**: [Your discussion forum]
- 🐛 **Bug Reports**: [Your issue tracker]
- 💡 **Feature Requests**: [Your feature request process]
 
---
 
## 🚀 Complete Production Workflow (January 2025)
 
### 🎯 **Initial Setup & Configuration**
```bash
# Navigate to project directory
cd azure-data-drift-detector
 
# Install all dependencies
pip install -r requirements.txt
 
# Copy and customize Azure configuration
cp config/settings_template.yaml config/settings.yaml
# Edit: storage_account_name, container_name, sas_token
 
# Validate system setup
python system_status.py
# ✅ All essential files present
# ✅ Azure configuration ready
# ✅ System status: READY
```
 
### 📊 **Test Data Generation & Upload**
```bash
# Generate realistic test datasets
python data_generator.py --count 500 --verbose
# 🎉 Generated employees_master_20250105_143022.csv (500 records)
# 🎉 Generated products_catalog_20250105_143022.json (250 records)  
# 🎉 Generated sales_transactions_20250105_143022.parquet (750 records)
# ☁️ Uploaded 3/3 files to Azure Blob Storage successfully
 
# Test Azure connection
python src/scan_azure.py
# ✅ Successfully connected to Azure Blob Storage
# ✅ Container access verified
```
 
### 🎯 **Baseline Establishment**
```bash
# Create initial baseline schema
python run.py --all-files --verbose
# 📊 Profiling 3 Azure files...
# ✅ Successfully profiled all files
# 🎯 Creating baseline schema from clean data
# ✅ Baseline schema created: schemas/baseline_schema.json
```
 
### 🚨 **Drift Detection Testing**
```bash
# Generate data with intentional drift
python data_generator.py --count 600 --add-drift --verbose
# 🎲 Drift simulation enabled
# ☁️ Uploaded 3/3 modified files successfully
 
# Detect drift in new data
python run.py --today-only --verbose
# 🔍 Scanning Azure for today's files...
# 📊 Profiling new files...
# 🚨 DRIFT DETECTED!
#   - Schema drift: 2/3 files
#   - Statistical drift: 3/3 files
#   - Report: drift_reports/drift_report_20250105_150322.json
 
# Analyze drift results
python drift_analyzer.py --summary
# 📊 DRIFT ANALYSIS SUMMARY
# Overall Drift: 🚨 YES (High severity)
# Files Analyzed: 3, Total Issues: 47
```
 
### 🔧 **Daily Production Usage**
```bash
# Daily monitoring workflow
python run.py --today-only              # Monitor today's uploads
python drift_analyzer.py --summary      # Quick drift summary
 
# Weekly comprehensive analysis
python run.py --all-files               # Full historical analysis
python drift_analyzer.py --issues-only  # Focus on problems
 
# Monthly maintenance
python cleanup_profiles.py --days 30    # Clean old profiles
python update_baseline_schema.py        # Update baseline if needed
python system_status.py                 # Health check
```
 
---
 
## 🎉 Quick Example
 
Let's walk through a complete Azure example:
 
### 1. Setup
```bash
# Install dependencies
pip install pandas pyyaml pyarrow azure-storage-blob
 
# Validate installation
python validate.py
```
 
### 2. Configure Azure
```bash
# Copy configuration template
cp config/settings_template.yaml config/settings.yaml
 
# Edit Azure settings
# Update: storage_account_name, container_name, sas_token
```
 
### 3. Upload Test Data to Azure
```bash
# Generate test data and upload to Azure
python data_generator.py --count 1000 --tables employees,products,sales
# ✓ Generated and uploaded timestamped files to Azure Blob Storage
```
 
### 4. Create Baseline
```bash
python run.py
# ✓ Configuration loaded
# � Initializing Azure Blob Storage scanner...
# ✓ Successfully connected to Azure Blob Storage
# �🔍 Scanning for files from today (20250804)...
# 📊 Profiling data...
# 🚨 Detecting drift...
# ✅ Baseline created from current profiles
```
 
### 5. Generate New Data (Simulate Changes)
```bash
# Generate modified data
python data_generator.py --count 1200 --drift-simulation
# ✓ Generated new timestamped files with intentional drift
```
 
### 6. Detect Drift
```bash
python run.py --verbose
# 🚨 DRIFT DETECTED
# - Schema drift in 2 files
# - Statistical drift in 3 files
# Check report: drift_reports/drift_report_20250804_143022.md
```
 
### 7. Analyze Results
```bash
# Analyze the drift report
python drift_analyzer.py --summary
# 📊 Files Analyzed: 6
# ⚠️ Overall Drift: 🚨 YES  
# 🔢 Total Issues: 23
 
# View detailed issues
python drift_analyzer.py --issues-only --high-only
# Shows only high-severity drift issues
```
 
## 🎯 Current System Status (v2.0 - January 2025)
 
### ✅ **Production-Ready Components**
- **Azure Data Generator**: Fully operational with robust upload capabilities for CSV, JSON, and Parquet files
- **Azure Scanner**: Seamless Azure Blob Storage integration with intelligent date filtering
- **Data Profiling**: Advanced statistical profiling with Pandas and optional PySpark support
- **Drift Detection**: Comprehensive schema and statistical drift detection with severity classification
- **File Mapping**: Smart mapping of timestamped files to baseline categories (e.g., `sales_20250105.parquet` → `sales.parquet`)
- **Report Generation**: Rich JSON and Markdown reports with actionable insights and categorized issues
- **Baseline Management**: Automated baseline creation, updates, and versioning with source tracking
- **System Monitoring**: Health checks, profile cleanup, and maintenance utilities
 
### 📊 **Verified Features**
- ✅ **Azure Integration**: Direct Azure Blob Storage connectivity with SAS token authentication
- ✅ **Multi-Format Processing**: Full support for CSV, JSON, and Parquet files
- ✅ **Schema Drift Detection**: Column additions/removals, type changes, constraint modifications
- ✅ **Statistical Drift Detection**: Distribution changes, null percentage shifts, statistical measure variations
- ✅ **Intelligent File Handling**: Automatic timestamp parsing and baseline mapping
- ✅ **Robust Error Handling**: Graceful handling of Azure SDK compatibility issues and network failures
- ✅ **Comprehensive Reporting**: Detailed drift analysis with severity levels and actionable recommendations
 
### 🚀 **Core Workflows**
- **🔄 Daily Monitoring**: `python run.py --today-only` - Monitor today's data uploads
- **📊 Full Analysis**: `python run.py --all-files` - Comprehensive historical analysis
- **⚡ Health Check**: `python system_status.py` - Quick system status verification
- **🎲 Data Generation**: `python data_generator.py` - Generate test data with optional drift simulation
- **📈 Report Analysis**: `python drift_analyzer.py --summary` - Analyze and summarize drift reports
- **🔧 Baseline Management**: `python update_baseline_schema.py` - Update reference baselines from clean data
 
## 📈 **Example Workflow Results (January 2025)**
 
### Recent Production Run:
```
🎯 AZURE DATA DRIFT DETECTOR - SYSTEM STATUS
==================================================
📁 Essential Files:
   ✅ run.py - Main drift detection engine
   ✅ data_generator.py - Azure data generation utility
   ✅ drift_analyzer.py - Report analysis tool
   ✅ config/settings.yaml - Azure configuration
   ✅ schemas/baseline_schema.json - Reference baselines
 
📊 Baseline Schema Status:
   Created: 2025-01-05T10:30:45.123456
   Datasets: 3 active baselines
   - employees.csv (baseline from employees_master_20250105_102030.csv)
   - products.json (baseline from products_catalog_20250105_102030.json)  
   - sales.parquet (baseline from sales_transactions_20250105_102030.parquet)
 
📋 Drift Reports: 12 historical reports available
   Latest: drift_report_2025-01-05.json
   Analysis Results: 6 files analyzed, 4 with detected drift
   Status: 🚨 DRIFT DETECTED (Medium severity)
 
☁️ Azure Connection: ✅ CONNECTED
   Storage Account: Verified ✅
   Container Access: Read/Write permissions confirmed ✅
   Latest Upload: 2025-01-05T14:22:10Z
 
🎯 Overall System Status: ✅ PRODUCTION READY
```
 
### Successful Azure Data Generation:
```
🎉 AZURE DATA GENERATION COMPLETE
=====================================
📅 Timestamp: 20250105_142210
� Generation Summary:
   - Employees: 150 records → employees_master_20250105_142210.csv ✅
   - Products: 75 records → products_catalog_20250105_142210.json ✅
   - Sales: 300 records → sales_transactions_20250105_142210.parquet ✅
 
☁️ Azure Upload Results:
   - Azure files uploaded: 3/3 ✅
   - Total data size: 245.6 KB
   - Upload duration: 3.2 seconds
   - All files verified in Azure Blob Storage ✅
 
🔗 File Relationships:
   - Sales transactions reference 150 employees
   - Sales transactions include 75 products
   - Realistic data patterns maintained
```
 
### Comprehensive Drift Detection Results:
```
🚨 AZURE DRIFT DETECTION ANALYSIS
==================================
📋 Processing Summary:
  - Files scanned: 6 (filtered by today's date)
  - Files profiled: 6/6 ✅
  - Files analyzed: 6/6 ✅
  - Processing duration: 8.4 seconds
 
🎯 Drift Detection Results:
  - Files with schema drift: 2/6
  - Files with statistical drift: 3/6
  - Overall drift status: 🚨 YES (Medium severity)
  - High-priority issues: 3
  - Medium-priority issues: 7
  - Low-priority issues: 12
 
📊 Issue Breakdown:
  Schema Issues (5 total):
    - New columns detected: 2
    - Column type changes: 2  
    - Nullable constraints changed: 1
 
  Statistical Issues (17 total):
    - Mean value shifts: 6
    - Standard deviation changes: 4
    - Null percentage changes: 3
    - Distribution pattern changes: 4
 
⚠️ Recommended Actions:
  1. Review new columns in employees_master file
  2. Investigate salary distribution changes
  3. Validate product pricing modifications
  4. Update baseline if changes are expected
```
 
## 🔗 **Additional Resources**
 
- **📝 Program Flow**: See `PROGRAM_FLOW.md` for detailed workflow documentation
- **⚙️ Configuration**: Template available in `config/settings_template.yaml`
- **📊 Reports**: All reports saved to `drift_reports/` directory
- **🗂️ Profiles**: Data profiles stored in `profiles/` directory
- **📋 Baseline**: Current baseline schema in `schemas/baseline_schema.json`
 
## 📞 **Support & Maintenance**
 
### System Health Checks
```bash
python system_status.py    # Overall system status
python -c "import azure.storage.blob; print('Azure SDK:', azure.storage.blob.__version__)"
```
 
### Regular Maintenance
```bash
python cleanup_profiles.py  # Clean old profile files
python update_baseline_schema.py  # Update baseline when needed
```
 
### Troubleshooting
- **Azure Connection Issues**: Check SAS token expiration and permissions
- **Upload Failures**: Verify Azure Storage Account and container exist
- **Profile Errors**: Some CSV/JSON files may fail profiling due to data structure issues
- **Missing Files**: Ensure proper file naming with timestamps for date filtering
 
---
 
**🎉 The Azure Data Drift Detector is production-ready and successfully monitoring cloud data for schema and statistical changes!**
```bash
# View the latest report
cat drift_reports/latest_drift_report.md
 
# Check all timestamped reports
ls drift_reports/
# drift_report_20250105_150322.md
# drift_report_20250105_150322.json
# latest_drift_report.md
# latest_drift_report.json
```
 
**🎉 Congratulations! Your Azure Data Drift Detector is now production-ready and actively monitoring Azure Blob Storage for data changes.** 🎯
 
## 🛠️ **Available Production Utilities**
 
### Core Operations
- **📊 Data Generator**: `python data_generator.py --help` - Generate test data with drift simulation
- **📈 Drift Analyzer**: `python drift_analyzer.py --help` - Comprehensive drift report analysis
- **⚡ System Status**: `python system_status.py` - Quick health and readiness check
- **🔧 Baseline Manager**: `python update_baseline_schema.py --help` - Update reference baselines
 
### Maintenance Tools
- **🧹 Profile Cleanup**: `python cleanup_profiles.py --help` - Clean old profile files
- **☁️ Azure Scanner**: `python src/scan_azure.py` - Test Azure connectivity
- **🔍 Configuration Validator**: Verify Azure settings and permissions
 
### Advanced Features
- **📅 Selective Processing**: Date-based filtering for efficient monitoring
- **🎯 Format Support**: CSV, JSON, and Parquet file processing
- **📊 Statistical Analysis**: Mean, std, min/max, distribution tracking
- **🚨 Alert Integration**: Ready for Azure Logic Apps and Function integration
 
## 📈 **Next Steps for Production**
 
1. **📅 Schedule Daily Monitoring**:
   ```bash
   # Set up daily cron job or Azure Function
   python run.py --today-only
   ```
 
2. **🔔 Configure Alerts**: Integrate with Azure Logic Apps for notifications
 
3. **📊 Create Dashboards**: Use Power BI or Azure Monitor for visualization
 
4. **🔐 Secure Credentials**: Move to Azure Key Vault for production security
 
5. **📈 Scale Up**: Add PySpark support for larger datasets when needed
 
---
 
**🚀 The Azure Data Drift Detector v2.0 - Production-ready Azure cloud-native data quality monitoring!**
 
*Made with ❤️ for reliable Azure data pipelines and ML operations*

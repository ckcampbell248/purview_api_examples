# 🔍 Microsoft Purview REST API - Fabric Table Metadata Management

This repository contains a Jupyter notebook that demonstrates how to use Microsoft Purview REST APIs to connect, discover, query, and update metadata for Fabric tables in Microsoft Purview.

## 📋 Overview

The notebook provides a step-by-step workflow to:
- 🔌 **Connect** to Microsoft Purview using Azure authentication
- 🔎 **Search** for Fabric tables in the Purview catalog
- 📊 **Query** metadata about tables and their columns
- ✏️ **Update** table descriptions, owners, and column descriptions
- ✅ **Verify** all changes were applied successfully

## 📦 Prerequisites

- 🏢 **Microsoft Purview account** with appropriate permissions
- 🔐 **Azure credentials** with access to the Purview account
- 💾 **Microsoft Fabric** workspace and tables registered in Purview
- 🐍 **Python 3.8+** with Jupyter support
- 🔑 **Azure authentication** via one of:
  - Azure CLI (`az login`)
  - Interactive browser login
  - Service principal credentials

## 🚀 Setup

### 1️⃣ Clone the Repository

```bash
git clone <repository-url>
cd purview_api
```

### 2️⃣ Create Python Environment (Optional but Recommended)

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3️⃣ Install Dependencies

```bash
pip install azure-identity requests python-dotenv jupyter
```

### 4️⃣ Configure Environment Variables

Copy the example environment file and fill in your details:

```bash
cp .env.example .env
```

Edit `.env` and set your values:

```env
PURVIEW_ACCOUNT_NAME=your-purview-account-name
TABLE_NAME=your-table-name
WORKSPACE_NAME=your-workspace-name  # Optional
LAKEHOUSE_NAME=your-lakehouse-name  # Optional
```

**Important:** ⚠️ Never commit the `.env` file to source control. It's already included in `.gitignore`.

### 5️⃣ Find Your Purview Account Name

To find your Purview account name:

1. Go to [Azure Portal](https://portal.azure.com) 🌐
2. Navigate to your Microsoft Purview account 🔍
3. On the **Overview** page, find the **Account endpoint** 📌
4. Your account name is the first part of the endpoint URL:
   - Example: `https://my-purview-account.purview.azure.com`
   - Account name: `my-purview-account`

## 💻 Usage

### 📓 Running the Notebook

1. Start Jupyter:
   ```bash
   jupyter notebook
   ```

2. Open `purview_fabric_metadata.ipynb` 📖

3. Run cells in order:
   - **Step 1-5**: ⚙️ Setup authentication and helper functions
   - **Step 6**: 🔍 Search for tables
   - **Step 7**: 📊 Query table metadata
   - **Step 8**: 📋 List column descriptions
   - **Step 8b**: 📝 Prepare column descriptions for update
   - **Step 9**: ✏️ Update table and column metadata
   - **Step 10**: ✅ Verify updates
   - **Step 11**: 🎉 Display updated column descriptions

### 🔐 Authentication Options

The notebook supports multiple authentication methods:

#### 🌐 Option 1: Interactive Browser (Default)
```python
credential = InteractiveBrowserCredential()
```
Opens a browser window for you to sign in with your Microsoft account.

#### 💻 Option 2: Azure CLI
```bash
az login
```
Then in the notebook:
```python
credential = DefaultAzureCredential()
```

#### 🤖 Option 3: Service Principal
Add to `.env`:
```env
AZURE_TENANT_ID=your-tenant-id
AZURE_CLIENT_ID=your-client-id
AZURE_CLIENT_SECRET=your-client-secret
```
Then in the notebook:
```python
credential = ClientSecretCredential(
    tenant_id=os.getenv("AZURE_TENANT_ID"),
    client_id=os.getenv("AZURE_CLIENT_ID"),
    client_secret=os.getenv("AZURE_CLIENT_SECRET")
)
```

## 📚 Notebook Steps Explained

### 🔍 Step 6: Search for Tables
Search the Purview catalog using keywords, with optional filters for workspace and lakehouse.

### 📊 Step 7: Query Table Metadata
Retrieve detailed information about a specific table including its properties and attributes.

### 📋 Step 8: List Column Descriptions
Fetch all columns with their current names, data types, and descriptions.

### 📝 Step 8b: Prepare Column Descriptions
Generate a template dictionary with all column names that you can customize with new descriptions.

### ✏️ Step 9: Update Metadata
Apply updates to:
- Table-level metadata (description, owner)
- Column-level descriptions (bulk update)

### ✅ Step 10-11: Verify & Display
Confirm all changes were applied and display the updated column descriptions.

## 🌐 API Endpoints Used

This notebook uses the following Purview REST API endpoints:

- 🔍 **Search**: `/catalog/api/search/query`
- 📥 **Get Entity**: `/catalog/api/atlas/v2/entity/guid/{guid}`
- ✏️ **Update Entity**: `/catalog/api/atlas/v2/entity`
- 🏷️ **Get Types**: `/catalog/api/types/typedefs`

## 🔒 Security Best Practices

✅ **DO:**
- 💾 Store sensitive information in `.env` file
- 🚫 Use `.gitignore` to exclude `.env` from version control
- 🏢 Use managed identities or service principals in production
- 🔄 Rotate credentials regularly
- 🔐 Use Azure Key Vault for production secrets

❌ **DON'T:**
- 📤 Commit `.env` file to source control
- 💻 Hard-code credentials in notebooks
- 📧 Share credentials via email or chat
- 👤 Use personal accounts for production automation

## 🔧 Troubleshooting

### 🔐 Authentication Failed
- ✔️ Ensure you have permissions to access the Purview account
- 💻 Try `az login` if using Azure CLI
- 👤 Check that your account has Data Curator or Data Reader role in Purview

### 🔍 No Results Found
- ✔️ Verify the table name is correct
- 📋 Check if the table is registered in Purview
- ⭐ Try searching with `*` to see all available assets
- 🔑 Ensure you have permissions to view the assets

### ❌ Column Update Failed
- 👤 Verify you have Data Curator role (required for updates)
- 🆔 Check that column GUIDs are valid
- 📝 Ensure descriptions don't contain invalid characters
- 📋 Review error messages for specific API validation errors

## 📚 Resources

- 📖 [Microsoft Purview REST API Documentation](https://learn.microsoft.com/rest/api/purview/)
- 🔗 [Apache Atlas REST API Reference](https://atlas.apache.org/api/v2/index.html)
- 🐍 [Azure Identity Python Library](https://learn.microsoft.com/python/api/azure-identity/)
- 💾 [Microsoft Fabric Documentation](https://learn.microsoft.com/fabric/)

## 🤝 Contributing

Contributions are welcome! Please ensure:
- 🔒 All sensitive data is in `.env` (not committed)
- ✨ Code follows existing patterns
- 📝 Documentation is updated for new features
- 🛡️ Error handling is robust

## 📄 License

[Add your license here]

## 💬 Support

For issues or questions:
- 🔧 Check the troubleshooting section above
- 📖 Review Purview API documentation
- 🐛 Open an issue in this repository

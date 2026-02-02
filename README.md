# PyEMC - Electronic Components Management System

A desktop application for managing and organizing electronic components (makers/manufacturers) with detailed cataloging, file attachment, and filtering capabilities.

## Overview

PyEMC is a PyQt/PySide6-based desktop application that provides a comprehensive solution for managing electronic components database. It allows users to:

- **Add and manage makers/manufacturers** with detailed information
- **Organize components by category** with custom category management
- **Store related files** including datasheets and symbol files
- **Filter and search** components by various criteria
- **Update and delete** component records with cascading file management
- **Maintain structured file system** organized by component ID and category

## Features

### Core Functionality

1. **Makers Management**
   - Add new electronic component makers/manufacturers
   - Update existing maker information
   - Delete makers and associated files
   - Store maker ID, name, category, and model number

2. **Category Management**
   - Create custom component categories
   - Edit and delete categories
   - Ensure data integrity (can only delete empty categories)
   - Categories must be in uppercase format

3. **Data Organization**
   - Model number tracking
   - Detailed descriptions and remarks
   - Component notes
   - File attachment support (datasheets, symbols)

4. **Search and Filtering**
   - Filter by Maker name
   - Filter by Category
   - Filter by Model Number
   - Dynamic filter options based on database content
   - Clear filters functionality

5. **File Management**
   - Attach multiple file types (symbols, datasheets)
   - Automatic directory structure creation
   - File association with component records
   - Cascading deletion of files when components are removed

## Project Structure

```
Crossfunctional-Team-Data-Consultation-Monitoring-App/
├── app.py                          # Main application entry point
├── _gui/                           # GUI components (PySide6)
│   ├── main.ui                     # Main window UI definition
│   ├── popup.ui                    # Delete confirmation dialog UI
│   ├── ui_main.py                  # Generated Python code from main.ui
│   └── ui_popup.py                 # Generated Python code from popup.ui
├── _ui_functions/                  # Business logic modules
│   ├── database_data.py            # Database operations (SQLAlchemy)
│   ├── main_list.py                # Table/list management
│   └── add_new_maker.py            # New maker addition logic
├── _settings/                      # Configuration files
│   └── database_path.txt           # Database location configuration
├── data/                           # Data storage
│   ├── database/                   # Microsoft Access database
│   │   └── makers.accdb            # Main database file
│   └── files/                      # Component file storage
│       └── [Component folders]/    # Organized by ID-CATEGORY
├── _design/                        # Design documents
│   └── design.xlsx                 # Application design specifications
└── README.md                       # This file
```

## Technology Stack

- **Frontend**: PySide6 (PyQt6 equivalent)
- **Backend**: SQLAlchemy ORM
- **Database**: Microsoft Access (.accdb format)
- **Language**: Python 3.x
- **UI Framework**: Qt Designer (for UI file generation)

## Installation

### Requirements

- Python 3.7+
- Windows OS (for Microsoft Access driver support)
- Microsoft Access Database Engine

### Setup Instructions

1. **Create a virtual environment**:
   ```powershell
   python -m venv venv
   ```

2. **Activate the virtual environment**:
   ```powershell
   .\venv\Scripts\Activate.ps1
   ```

3. **Install dependencies**:
   ```powershell
   pip install PySide6 SQLAlchemy pyodbc
   ```

4. **Configure database path**:
   - Edit `_settings/database_path.txt`
   - Enter the root path to your data folder (e.g., `C:\YourPath\data`)

5. **Run the application**:
   ```powershell
   python app.py
   ```

## Database Structure

### Tables

#### tbl_makers
Contains all electronic component maker information:
- ID (Auto-generated primary key)
- Maker (Manufacturer name)
- Category (Component category)
- Model_No (Model number)
- Description (Component description)
- Remarks (Additional remarks)
- Symbol_Link (Path to symbol file)
- File_Link (Path to datasheet/file)
- Notes (Additional notes)

#### tbl_categories
Maintains available component categories:
- ID (Category ID)
- Category_Name (Category name)

## Usage

### Adding a New Maker

1. Click **"Add New Maker"** button
2. Fill in the maker information:
   - Maker name
   - Category (select from dropdown)
   - Model number
   - Description and remarks
3. Attach files:
   - Symbol file (optional)
   - Datasheet/File (optional)
4. Click **"Save"** to create the entry

### Managing Categories

1. Click **"Add Category"** button
2. Enter category name in **UPPERCASE**
3. Click **"Add to List"** to add
4. Click **"Save"** to persist changes
5. **Note**: Categories can only be deleted if no makers exist in that category

### Updating a Maker

1. Select a maker from the table
2. Click **"Update"** button
3. Modify the information
4. Click **"Save Changes"**

### Deleting a Maker

1. Select a maker from the table
2. Click **"Delete"** button
3. Confirm deletion in the dialog
4. Associated files are automatically removed

### Filtering Data

1. Select filter type: Maker, Category, or Model No
2. Select specific filter value from dropdown
3. Click **"Apply Filter"** to see results
4. Click **"Clear Filter"** to reset

## File Organization

Files are organized automatically in the following structure:
```
data/files/
├── [ID]-[CATEGORY]/          # e.g., 37-FLUORESCENT LAMP/
│   ├── symbol files
│   └── datasheet files
├── [ID]-[CATEGORY]/
└── ...
```

## Important Notes

- **Category Format**: Categories must be in **UPPERCASE**
- **No Spaces**: Ensure no leading or trailing spaces when entering categories
- **Deletion Constraint**: Categories cannot be deleted if they contain maker items
- **File Management**: All associated files are automatically deleted when a maker is removed
- **Database Location**: Update `_settings/database_path.txt` if moving the database folder

## Configuration

### Database Path Configuration

Edit `_settings/database_path.txt`:
```
Z:\Projects\Crossfunctional-Team-Data-Consultation-Monitoring-App\data
```

## Troubleshooting

### Database Connection Issues

- Verify Microsoft Access driver is installed on your system
- Check the database path in `_settings/database_path.txt`
- Ensure the makers.accdb file exists and is accessible

### File Attachment Issues

- Ensure you have read/write permissions to the data folder
- Verify files exist at the selected paths
- Check that file paths don't contain invalid characters

### UI Issues

- The application maintains a fixed window size (920x600)
- Ensure your display has adequate resolution
- Regenerate UI files if needed using Qt Designer

## Development

### UI Modifications

UI files (.ui) are converted to Python code using Qt Designer's compiler:
```powershell
pyside6-uic main.ui -o ui_main.py
pyside6-uic popup.ui -o ui_popup.py
```

### Database Queries

All database operations use SQLAlchemy Core with Microsoft Access:
- See `_ui_functions/database_data.py` for query examples
- Connection string uses ODBC driver
- Table reflection is used for dynamic schema handling

## Author

Created by: jeevr (2022)
Repository: [GitHub - Crossfunctional-Team-Data-Consultation-Monitoring-App](https://github.com/jeevr/Crossfunctional-Team-Data-Consultation-Monitoring-App)

## License

Please refer to the repository's LICENSE file for licensing information.

## Support

For issues or feature requests, please use the GitHub repository's issue tracker.

# CSV-to-Box

A Java-based utility that converts CSV files into separate Excel (.xlsx) files, grouped by customer name. This tool reads a semicolon-delimited CSV file and automatically splits the data into individual Excel workbooks based on the first column (customer name).

## 📋 Overview

CSV-to-Box processes large CSV files containing data for multiple customers and generates individual Excel files for each customer. This is particularly useful for:
- Distributing customer-specific reports
- Organizing data by client or entity
- Converting bulk CSV exports into manageable Excel files
- Automating report generation workflows

## ✨ Features

- **Automatic Customer Grouping**: Splits CSV data by customer name (first column)
- **Excel Output**: Generates `.xlsx` files using Apache POI
- **Memory Efficient**: Uses `SXSSFWorkbook` for streaming large datasets
- **Header Preservation**: Maintains CSV headers in each Excel file
- **Semicolon Delimiter Support**: Processes CSV files with semicolon (`;`) delimiters

## 🔧 Prerequisites

- **Java**: JDK 15 or higher
- **Maven**: For dependency management and building the project
- **Apache POI**: Automatically managed via Maven dependencies

## 📦 Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/CSV-to-Box.git
   cd CSV-to-Box/CsvToBox
   ```

2. **Build the project with Maven**:
   ```bash
   mvn clean install
   ```

3. **Verify dependencies are installed**:
   The `pom.xml` includes:
   - Apache POI 5.0.0
   - Apache POI OOXML 5.0.0

## 🚀 Usage

### Basic Usage

1. **Prepare your CSV file**:
   - Ensure your CSV uses semicolon (`;`) as the delimiter
   - First column should contain customer names
   - First row should contain headers
   - Example format:
     ```
     CustomerName;Product;Quantity;Price
     ACME Corp;Widget A;100;50.00
     ACME Corp;Widget B;200;75.00
     TechCo;Gadget X;50;120.00
     ```

2. **Update file paths** in `CSVtoExcel.java`:
   ```java
   // Input CSV file (line 19)
   new FileInputStream("C:\\Users\\willi\\Desktop\\test.csv")
   
   // Output directory (line 59)
   new FileOutputStream("C:\\Users\\willi\\Desktop\\Map\\test_" + name + ".xlsx")
   ```

3. **Run the application**:
   ```bash
   mvn exec:java -Dexec.mainClass="CSVtoExcel"
   ```
   
   Or compile and run directly:
   ```bash
   javac -cp "target/classes:target/dependency/*" src/main/java/CSVtoExcel.java
   java -cp "target/classes:target/dependency/*" CSVtoExcel
   ```

### Output

The program will generate separate Excel files named:
- `test_CustomerName1.xlsx`
- `test_CustomerName2.xlsx`
- `test_CustomerName3.xlsx`
- etc.

Each file contains only the rows for that specific customer, with the original headers preserved.

## 📁 Project Structure

```
CSV-to-Box/
├── CsvToBox/
│   ├── src/
│   │   └── main/
│   │       └── java/
│   │           └── CSVtoExcel.java    # Main application logic
│   ├── pom.xml                         # Maven configuration
│   └── target/                         # Compiled classes and dependencies
└── README.md                           # This file
```

## 🔍 How It Works

1. **Reading Phase**: 
   - Opens the CSV file and reads the header row
   - Reads data line by line
   - Groups consecutive rows with the same customer name

2. **Grouping Logic**:
   - Tracks the current customer name
   - Accumulates rows for each customer
   - When a new customer is encountered, writes the previous customer's data to Excel

3. **Writing Phase**:
   - Creates a new Excel workbook for each customer
   - Writes the header row
   - Populates data rows
   - Saves the file with the customer name in the filename

## ⚙️ Configuration

### Changing the Delimiter

To use a different delimiter (e.g., comma instead of semicolon), modify the split pattern:

```java
// Change from semicolon to comma
String[] values = scanner.nextLine().split(",");
```

### Customizing Output Format

Modify the output path and filename pattern in the `write()` method:

```java
workbook.write(new FileOutputStream("path/to/output/" + name + ".xlsx"));
```

## 🛠️ Technical Details

- **Language**: Java 15
- **Build Tool**: Maven
- **Dependencies**:
  - Apache POI 5.0.0 (Core Excel library)
  - Apache POI OOXML 5.0.0 (Excel 2007+ format support)
- **Excel Format**: XLSX (Office Open XML)
- **Streaming**: Uses `SXSSFWorkbook` for memory-efficient processing

## ⚠️ Known Limitations

- **Hard-coded paths**: Input and output file paths are currently hard-coded
- **Delimiter**: Only supports semicolon (`;`) delimiter
- **Sorting requirement**: CSV must be pre-sorted by customer name for optimal grouping
- **Error handling**: Limited exception handling for malformed CSV files

## 🔮 Future Improvements

- [ ] Add command-line arguments for input/output paths
- [ ] Support multiple delimiter types (comma, tab, pipe)
- [ ] Add configuration file support
- [ ] Implement proper logging
- [ ] Add progress indicators for large files
- [ ] Handle unsorted CSV files
- [ ] Add data validation and error reporting
- [ ] Support custom column selection for grouping
- [ ] Add unit tests

## 📝 License

This project is available for use under standard open-source practices.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## 📧 Contact

For questions or support, please open an issue in the repository.

---

**Note**: Remember to update the hard-coded file paths before running the application with your own data!

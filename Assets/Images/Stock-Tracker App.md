## **Overview of the Project**

This project is a **Stock Tracking Application** built using **JavaFX** for the user interface and **Maven** for dependency management. It fetches stock data from an external API, stores it in a local SQLite database, and visualizes the data using a candlestick chart.

---

## **Key Technologies Used**

1. **JavaFX**: A framework for building graphical user interfaces (GUIs) in Java.
2. **Maven**: A build automation tool that manages dependencies and simplifies project builds.
3. **SQLite**: A lightweight database for storing stock data locally.
4. **OkHttp**: A library for making HTTP requests to fetch stock data from an API.
5. **JSON**: A library for parsing JSON responses from the API.

---

## **Project Structure**

The project is organized into packages, each serving a specific purpose:

1. **[com.stocktracker.api](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: Handles communication with the stock API.
2. **[com.stocktracker.database](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: Manages database connections and operations.
3. **[com.stocktracker.models](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: Defines the data model for stock data.
4. **[com.stocktracker.ui](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: Contains the main application logic and user interface.
5. **[com.stocktracker.ui.charts](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: Implements a custom candlestick chart for visualizing stock data.

---

## **Dependencies in [pom.xml](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**

The [pom.xml](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) file is the Maven configuration file. It specifies the dependencies and plugins required for the project.

### **Dependencies**

1. **JavaFX Modules**:
    
    - **[javafx-controls](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: Provides UI components like buttons, text fields, and charts.
    - **[javafx-fxml](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: Enables the use of FXML files for defining UI layouts (not used here but included for flexibility).
    - **[javafx-graphics](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: Provides low-level graphics rendering capabilities.
    - **Reasoning**: JavaFX is used to build the GUI, and these modules are essential for creating and rendering the application's interface.
2. **OkHttp**:
    
    - **[com.squareup.okhttp3:okhttp](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: A library for making HTTP requests.
    - **Reasoning**: Used to fetch stock data from the Alpha Vantage API. It is lightweight, efficient, and easy to use.
3. **SQLite JDBC**:
    
    - **[org.xerial:sqlite-jdbc](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: A library for connecting to SQLite databases.
    - **Reasoning**: SQLite is a lightweight database that doesn't require a separate server, making it ideal for small projects like this.
4. **JSON**:
    
    - **[org.json:json](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: A library for parsing JSON data.
    - **Reasoning**: The stock API returns data in JSON format, so this library is used to parse and extract the required information.

### **Plugins**

1. **JavaFX Maven Plugin**:
    - **[org.openjfx:javafx-maven-plugin](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: A plugin to run JavaFX applications using Maven.
    - **Reasoning**: Simplifies running the JavaFX application directly from Maven commands.

---

## **Code Walkthrough**

### **1. [MainApp.java](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) (Entry Point)**

This is the main class that initializes the application and sets up the user interface.

#### **Key Components**

1. **UI Elements**:
    
    - **TextField**: For entering the stock symbol (e.g., "AAPL").
    - **Button**: To fetch and display stock data.
    - **ComboBox**: To show a history of recently searched stock symbols.
    - **CandlestickChart**: A custom chart for visualizing stock data.
2. **Event Handling**:
    
    - When the user clicks the "Show Chart" button, the app fetches stock data from the API, processes it, and updates the chart.
3. **Validation**:
    
    - Ensures the stock symbol is valid (1-5 uppercase letters).
    - Handles API rate limits and errors gracefully.

#### **Why These Choices?**

- **JavaFX Components**: Provide a clean and interactive user interface.
- **Validation**: Ensures the user inputs are correct and prevents unnecessary API calls.

---

### **2. [ApiClient.java](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) (API Communication)**

This class handles communication with the Alpha Vantage API.

#### **Key Methods**

1. **`getDailySeries(String symbol)`**:
    
    - Fetches historical stock data for the given symbol.
    - Uses **OkHttp** to make an HTTP GET request.
2. **`parseDailySeries(String jsonResponse)`**:
    
    - Parses the JSON response and converts it into a list of [StockData](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) objects.
3. **Rate Limiting**:
    
    - Ensures the app doesn't exceed the API's limit of 5 calls per minute.
    - Uses a **LinkedList** to track timestamps of API calls.

#### **Why These Choices?**

- **OkHttp**: Efficient and easy-to-use library for HTTP requests.
- **LinkedList**: Ideal for managing a sliding window of timestamps, as it allows efficient addition and removal of elements.

---

### **3. [DatabaseManager.java](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) (Database Management)**

This class manages the SQLite database.

#### **Key Methods**

1. **[initialize()](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**:
    
    - Creates the required tables (`users`, `stock_data`, `alerts`) if they don't already exist.
2. **[getConnection()](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**:
    
    - Returns a connection to the SQLite database.

#### **Why SQLite?**

- Lightweight and easy to set up.
- No need for a separate database server, making it ideal for small projects.

---

### **4. [StockDAO.java](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) (Data Access Object)**

This class handles database operations related to stock data.

#### **Key Methods**

1. **[insertStockData()](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**:
    
    - Inserts stock data into the `stock_data` table.
2. **[getHistoricalData()](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**:
    
    - Retrieves historical stock data for a given symbol.

#### **Why Use a DAO?**

- Separates database logic from the rest of the application, making the code more modular and easier to maintain.

---

### **5. [CandlestickChart.java](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) (Custom Chart)**

This class extends JavaFX's [XYChart](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) to create a candlestick chart for visualizing stock data.

#### **Key Features**

1. **Candlestick Representation**:
    
    - Each candlestick shows the stock's open, high, low, and close prices for a specific day.
    - Green candlesticks indicate the stock closed higher than it opened, while red indicates the opposite.
2. **Custom Rendering**:
    
    - Uses **Rectangle** for the candlestick body and **Line** for the wick.

#### **Why Use a Custom Chart?**

- JavaFX doesn't provide a built-in candlestick chart, so a custom implementation is necessary.

---

### **6. [StockData.java](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) (Data Model)**

This class represents a single stock data point.

#### **Fields**

- **[timestamp](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: The date and time of the data point.
- **[open](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html), [high](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html), [low](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html), [close](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: The stock's prices.
- **[volume](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: The trading volume.

#### **Why Use a Model Class?**

- Encapsulates stock data in a single object, making it easier to pass around and manipulate.

---

## **How It All Works Together**

1. The user enters a stock symbol and clicks "Show Chart."
2. The app validates the input and fetches stock data from the API.
3. The data is parsed into [StockData](vscode-file://vscode-app/c:/Users/Apurav%20Gautam/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) objects and stored in the SQLite database.
4. The candlestick chart is updated to display the stock data.
5. The app maintains a history of recently searched symbols for convenience.

---

## **Why These Design Choices?**

1. **JavaFX**: Provides a modern and interactive GUI.
2. **Maven**: Simplifies dependency management and project builds.
3. **SQLite**: Lightweight and easy to use for local data storage.
4. **OkHttp**: Efficient for making HTTP requests.
5. **JSON**: Essential for parsing API responses.

---

## **Next Steps for a Beginner**

1. **Learn JavaFX Basics**:
    - Understand how to create and style UI components.
2. **Explore Maven**:
    - Learn how to add dependencies and use Maven commands.
3. **Understand SQLite**:
    - Practice basic SQL queries to interact with the database.
4. **Experiment with the Code**:
    - Modify the UI or add new features (e.g., more chart types or additional API endpoints).

This project is a great starting point for learning JavaFX, Maven, and working with APIs and databases.
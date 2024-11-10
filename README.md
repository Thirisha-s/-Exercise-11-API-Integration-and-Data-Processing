## Exercise_11-API_Integration_and_Data_Processing
```
Name: THIRISHA S
Reg No: 212222230160
```
# Aim:
To create a workflow in UiPath that calls a REST API (e.g., Weather API), processes the JSON response, and writes the extracted data to a database.

## Equipment Required:
UiPath Studio<br>
API Key from a Weather API provider (e.g., OpenWeatherMap)<br>
Database (e.g., SQL Server, MySQL, SQLite)<br>
## Procedure:
### Step 1: Install Required Packages
Open UiPath Studio.<br>
Go to Manage Packages in the top toolbar.<br>
#### Install the following packages:<br>
UiPath.WebAPI.Activities (to call REST APIs)<br>
UiPath.Database.Activities (to interact with databases)<br>
### Step 2: Obtain the Weather API Details
For this example, we’ll use the OpenWeatherMap API:<br>

API Endpoint:<br>
```
https://api.openweathermap.org/data/2.5/weather?q={city_name}&appid={your_api_key}
```
Replace {city_name} with the desired city (e.g., "London") and {your_api_key} with your personal API key from OpenWeatherMap.

### Step 3: Building the UiPath Workflow
#### 1. Create a New Sequence
Open UiPath Studio and create a new sequence called WeatherAPI_to_DB.
#### 2. Add HTTP Request Activity
Search for HTTP Request activity from the activities panel.<br>
Configure it as follows:<br>
Endpoint (URL):<br>
```
https://api.openweathermap.org/data/2.5/weather?q=London&appid=YOUR_API_KEY
```
Method: Set it to GET as we are retrieving data.<br>
Output: Create a variable called responseJSON to store the API response.
#### 3. Deserialize JSON
Use the Deserialize JSON activity to convert the JSON response into a UiPath-readable format.<br>
Input: responseJSON<br>
Output: Create a variable jsonResponse to store the deserialized data.
#### 4. Extract Required Data
Extract specific information like city name, temperature, and humidity from the JSON response.<br>
Use Assign activities to extract values:<br>
city = jsonResponse("name").ToString<br>
temperature = jsonResponse("main")("temp").ToString<br>
humidity = jsonResponse("main")("humidity").ToString<br>
#### 5. Connect to Database
Use Connect activity from the UiPath.Database.Activities package.<br>
Connection String: Based on the type of database you're using (e.g., SQLite, MySQL). Here’s an example for SQLite:<br>
```
Data Source=path_to_your_database;Version=3;
```
Store the connection in a variable called dbConnection.
#### 6. Insert Data into Database
Use Execute Non Query activity to write data into the database.<br>
SQL Query:<br>
```
INSERT INTO WeatherData (City, Temperature, Humidity)
VALUES (@City, @Temperature, @Humidity)
```
In the Parameters section, assign:<br>
@City -> city<br>
@Temperature -> temperature<br>
@Humidity -> humidity
#### 7. Close Database Connection
Use Disconnect activity to close the database connection after writing the data.
## UiPath WorkFlow:
![Screenshot 2024-10-12 112514](https://github.com/user-attachments/assets/0f6675b6-4c7d-46a2-ae0d-ba00320c8b71)
![Screenshot 2024-10-12 112619](https://github.com/user-attachments/assets/f17f7f2b-68aa-44ce-b69d-52b6cdd043a2)
![Screenshot 2024-10-12 112713](https://github.com/user-attachments/assets/e435a960-bbd8-48a6-adc9-1ada21643b89)
![Screenshot 2024-10-12 112813](https://github.com/user-attachments/assets/12256f75-a6cc-4c8b-a27b-e3c0de5f8763)
![Screenshot 2024-10-12 113241](https://github.com/user-attachments/assets/cdab5826-642c-489f-b55e-3b454dd53086)
![Screenshot 2024-10-12 182140](https://github.com/user-attachments/assets/13b99e82-d9ff-4868-8325-e8a32b0cf052)
![Screenshot 2024-10-12 182320](https://github.com/user-attachments/assets/c712de50-e883-422c-a7f3-15a90f1936c6)
![Screenshot 2024-10-12 182418](https://github.com/user-attachments/assets/a4bd188e-f05d-4767-a855-be1818821933)
![Screenshot 2024-10-12 182502](https://github.com/user-attachments/assets/da374fdb-f3d2-4bd4-a60f-d9cc3f4e524d)

## Result:
The UiPath workflow successfully calls the weather API, processes the JSON response, and writes data such as city name, temperature, and humidity into the specified database table.

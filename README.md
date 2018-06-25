# GoogleMapsNearbyPlacesDemo
This contains all the code till nearby places part 3

Watch all the tutorials here : https://youtube.com/TechAcademy8

For step1 : 
https://www.androidtutorialpoint.com/intermediate/android-map-app-showing-current-location-android/

For step2 to step4:  
https://www.androidtutorialpoint.com/intermediate/google-maps-search-nearby-displaying-nearby-places-using-google-places-api-google-maps-api-v2/
____________________________________________________________________________________________________________________________
# Step 1: MapActivity.java
Majorly focuses on getting current location and forming URL. 

# Step 2: GetNearByPlaces.java
Make a new class named GetNearbyPlacesData.java. This class should be extended from AsyncTask.

Android AsyncTask is an abstract class provided by Android which gives us the liberty to perform heavy tasks in the background and keep the UI thread light thus making the application more responsive.

Android application runs on a single thread when launched. Due to this single thread model tasks that take longer time to fetch the response can make the application non-responsive. To avoid this we use android AsyncTask to perform the heavy tasks in background on a dedicated thread and passing the results back to the UI thread. Hence use of AsyncTask in android application keeps the UI thread responsive at all times.

The basic methods used in an android AsyncTask class are defined below :

1) doInBackground() : This method contains the code which needs to be executed in background. In this method we can send results multiple times to the UI thread by publishProgress() method. To notify that the background processing has been completed we just need to use the return statements

2) onPreExecute() : This method contains the code which is executed before the background processing starts

3) onPostExecute() : This method is called after doInBackground method completes processing. Result from doInBackground is passed to this method

4) onProgressUpdate() : This method receives progress updates from doInBackground method, which is published via publishProgress method, and this method can use this progress update to update the UI thread

The three generic types used in an android AsyncTask class are given below :

Params : The type of the parameters sent to the task upon execution

Progress : The type of the progress units published during the background computation

Result : The type of the result of the background computation


In the above code of GetNearByPlaces.java, DownloadUrl is a class which is used to retrieve data from URL using HttpURLConnection and File handling methods. We will discuss its code after this class. After retrieving data in the form of googlePlacesData we are passing it to onPostExecute method. Data from URL will be in the form JSON which needs to be parsed, So we have made a class named DataParser. DataParser.java file should be added at the same path as MainActivity.java. Code is given at bottom of this tutorial. dataParser.parse(result) is used to parse data and resultant is stored as a list in nearbyPlacesList. Now nearbyPlacesList will have all information about nearby Hospitals which we can easily access and add markers on corresponding places. Markers are added in Google Maps using function ShowNearbyPlaces. This is pretty much self explanatory.


# Step 3: DownloadURL.java
This class should be made at the same path as MainActivity.java with the name DownloadUrl.java.

Data returned from web will be in json format which user can get using HttpURLConnection. So this task will return JSON data returned from web.


# Step 4: DataParser.java
Purpose of this class is already explained in step2.


# Step 5: Database.java (InformActivity.java calls methods contained in this class)

This class contains two functions that are given below :
1) boolean insertData()
  This function is for inserting values to database (database propagation).InformActivity.java contains commands for   insertion of hospital details.

2) Cursor getAllData()
This method is used to retreive the details of hospitals.


# Step 6: InformActivity.java
It carries command to propagate SQLite databse named as 'hospital'.
Also, this contains method to display the details of hospitals.

# About SQLite Database
SQLite is a relational database management system contained in a C programming library. In contrast to many other database management systems, SQLite is not a client–server database engine. Rather, it is embedded into the end program.
See the functions of SQLite databse here: 

https://developer.android.com/reference/android/database/sqlite/SQLiteDatabase

SQLite is a self-contained, high-reliability, embedded, full-featured, public-domain, SQL database engine. SQLite is the most used database engine in the world.

WHEN TO USE SQLite : https://www.sqlite.org/whentouse.html

SQLite is not directly comparable to client/server SQL database engines such as MySQL, Oracle, PostgreSQL, or SQL Server since SQLite is trying to solve a different problem.
Client/server SQL database engines strive to implement a shared repository of enterprise data. They emphasize scalability, concurrency, centralization, and control. SQLite strives to provide local data storage for individual applications and devices. SQLite emphasizes economy, efficiency, reliability, independence, and simplicity.
SQLite does not compete with client/server databases. SQLite competes with fopen().

For more details about SQLite visit https://www.sqlite.org/index.html



# SQLiteToExcel

[ ![Download](https://api.bintray.com/packages/li-yu/maven/SQLiteToExcel/images/download.svg) ](https://bintray.com/li-yu/maven/SQLiteToExcel/_latestVersion)

[中文版 README](README.md)

The SQLiteToExcel library integrates [Apache POI](http://poi.apache.org/) and some basic database query operations, making it easier to convert between SQLite and Excel.

## Version history
[Release Notes](https://github.com/li-yu/SQLiteToExcel/releases)

## How to use
#### 1.Add Gradle dependencies or download the Jar file as libs to the project
``` Gradle
compile 'com.liyu.tools:sqlitetoexcel:1.0.4'
```
[SqliteToExcel-v1.0.4.jar](https://github.com/li-yu/SQLiteToExcel/releases)
#### 2.Add SD card read and write permissions to AndroidManifest.xml (Android 6.0 and above need to deal with run-time permissions)
```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

#### 3.SQLite -> Excel Sample code(Specific examples can be found in [demo](https://github.com/li-yu/SQLiteToExcel/blob/master/app/src/main/java/com/liyu/demo/MainActivity.java))
* Initialize (Default export path is external SD card root directory ```Environment.getExternalStorageDirectory()```)
```java
SqliteToExcel ste = new SqliteToExcel(this, "helloworld.db");
```
or(Specifies the root directory of the export)
```java
SqliteToExcel ste = new SqliteToExcel(this, "helloworld.db", "/mnt/sdcard/myfiles/");
```
* Export a single table to excel
```java
ste.startExportSingleTable(String table, String fileName, ExportListener listener);
```
* Export multiple tables to excel
```java
ste.startExportTables(List<String> tables, String fileName, ExportListener listener);
```
* Export all tables to excel
```java
ste.startExportAllTables(String fileName, ExportListener listener);
```
* Task listener interface
```java
public interface ExportListener {
        void onStart();

        void onCompleted(String filePath);

        void onError(Exception e);
    }
```

#### 4.Excel -> SQLite Sample code(Specific examples can be found in [demo](https://github.com/li-yu/SQLiteToExcel/blob/master/app/src/main/java/com/liyu/demo/MainActivity.java))
* Initialize
```java
ExcelToSqlite ets = new ExcelToSqlite(this, "user.db");
```
* From the assets directory
```java
ets.startFromAsset(String assetFileName, ImportListener listener);
```
* For any excel files
```java
ets.startFromFile(File file, ImportListener listener);
```
* Task listener interface
```java
public interface ImportListener {
        void onStart();

        void onCompleted(String dbName);

        void onError(Exception e);
    }
```

#### 5.Thanks
- [https://github.com/centic9/poi-on-android](https://github.com/centic9/poi-on-android)
- [https://github.com/FasterXML/aalto-xml](https://github.com/FasterXML/aalto-xml)
- [https://github.com/johnrengelman/shadow](https://github.com/johnrengelman/shadow)

#### 6.Precautions
* When convert Excel to SQLite,the default take excel sheet in the first row as the database table column name, please refer to the style [demo](https://github.com/li-yu/SQLiteToExcel/blob/master/app/src/main/assets/user.xls).
* Currently only blob field is supported as a picture, because I do not know whether byte [] is a file or a picture.
* The database files must be located under ```/data/data/package name/databases/` ``, and are usually located in this directory.

## About me
* Email: [me@liyuyu.cn](mailto:me@liyuyu.cn)
* Weibo: [@呵呵小小鱼](http://weibo.com/u/1241167880)

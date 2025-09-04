# Weather-Data-Storage-System-WeatherSystem.java-README.md

/*
------------------------------------------------------------
Assignment 1 - Weather Data Storage System
Course Code: ENCS205 / ENCA201
Programme: B.Tech / BCA (3rd Semester)
Department: CSE
Session: 2025–26
------------------------------------------------------------
Description:
This program implements a Weather Data Storage System using
2D arrays and Abstract Data Types (ADTs). It allows storing,
inserting, deleting, and retrieving weather data (temperature)
based on city and year. It also supports row-major and column-
major traversal, handles sparse data using sentinel values,
and analyzes time and space complexity of operations.
------------------------------------------------------------
Key Features:
1. Weather Record ADT with attributes (date, city, temperature).
2. 2D Array-based data storage (rows = years, cols = cities).
3. Row-major and column-major access methods.
4. Sparse data handling using sentinel values (-999).
5. Complexity analysis for key operations.
------------------------------------------------------------
Author: [Your Name]
Date: [Submission Date]
------------------------------------------------------------
*/

import java.util.*;

class WeatherRecord {
    String date;
    String city;
    double temperature;

    WeatherRecord(String d, String c, double t) {
        this.date = d;
        this.city = c;
        this.temperature = t;
    }
}

class WeatherStorage {
    private List<String> cities;
    private List<Integer> years;
    private double[][] data;
    private final double sentinel = -999.0;

    WeatherStorage(List<String> cities, List<Integer> years) {
        this.cities = cities;
        this.years = years;
        this.data = new double[years.size()][cities.size()];

        // Initialize with sentinel
        for (int i = 0; i < years.size(); i++) {
            Arrays.fill(this.data[i], sentinel);
        }
    }

    // Insert record
    public void insert(String city, int year, double temp) {
        int row = findYear(year);
        int col = findCity(city);
        if (row != -1 && col != -1) {
            data[row][col] = temp;
        }
    }

    // Delete record
    public void remove(String city, int year) {
        int row = findYear(year);
        int col = findCity(city);
        if (row != -1 && col != -1) {
            data[row][col] = sentinel;
        }
    }

    // Retrieve record
    public double retrieve(String city, int year) {
        int row = findYear(year);
        int col = findCity(city);
        if (row != -1 && col != -1) {
            return data[row][col];
        }
        return sentinel;
    }

    // Row-major traversal
    public void rowMajorAccess() {
        System.out.println("\nRow-major traversal:");
        for (int i = 0; i < years.size(); i++) {
            for (int j = 0; j < cities.size(); j++) {
                System.out.println("Year: " + years.get(i) + 
                                   " City: " + cities.get(j) +
                                   " Temp: " + data[i][j]);
            }
        }
    }

    // Column-major traversal
    public void columnMajorAccess() {
        System.out.println("\nColumn-major traversal:");
        for (int j = 0; j < cities.size(); j++) {
            for (int i = 0; i < years.size(); i++) {
                System.out.println("Year: " + years.get(i) + 
                                   " City: " + cities.get(j) +
                                   " Temp: " + data[i][j]);
            }
        }
    }

    // Handle sparse data
    public void handleSparseData() {
        int missing = 0;
        for (int i = 0; i < years.size(); i++) {
            for (int j = 0; j < cities.size(); j++) {
                if (data[i][j] == sentinel) missing++;
            }
        }
        System.out.println("\nMissing records: " + missing);
    }

    // Complexity analysis
    public void analyzeComplexity() {
        System.out.println("\nComplexity Analysis:");
        System.out.println("Insert: O(1)");
        System.out.println("Delete: O(1)");
        System.out.println("Retrieve: O(1)");
        System.out.println("Row/Column traversal: O(m*n)");
        System.out.println("(m = years, n = cities)");
    }

    // Helper methods
    private int findCity(String city) {
        return cities.indexOf(city);
    }

    private int findYear(int year) {
        return years.indexOf(year);
    }
}

public class WeatherSystem {
    public static void main(String[] args) {
        List<String> cities = Arrays.asList("Delhi", "Mumbai", "Chennai");
        List<Integer> years = Arrays.asList(2023, 2024, 2025);

        WeatherStorage ws = new WeatherStorage(cities, years);

        // Insert records
        ws.insert("Delhi", 2023, 32.5);
        ws.insert("Mumbai", 2024, 29.8);
        ws.insert("Chennai", 2025, 35.2);

        // Retrieve
        System.out.println("Delhi 2023 Temp: " + ws.retrieve("Delhi", 2023));

        // Row-major & column-major traversal
        ws.rowMajorAccess();
        ws.columnMajorAccess();

        // Sparse data handling
        ws.handleSparseData();

        // Complexity analysis
        ws.analyzeComplexity();
    }
}

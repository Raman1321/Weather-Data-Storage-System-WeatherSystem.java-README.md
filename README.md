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
Author: [Raman]
Date: 4 sept, 2025
------------------------------------------------------------
# Weather Record ADT
class WeatherRecord:
    def _init_(self, date, city, temperature):
        self.date = date
        self.city = city
        self.temperature = temperature

    def _repr_(self):
        return f"WeatherRecord(Date={self.date}, City={self.city}, Temp={self.temperature})"


# Data Storage Class (2D Array + ADT)
class WeatherDataStorage:
    def _init_(self, years, cities):
        # Years and cities lists
        self.years = years
        self.cities = cities
        # Initialize 2D array with sentinel (-9999 for missing values)
        self.data = [[-9999 for _ in range(len(cities))] for _ in range(len(years))]

    def insert(self, year, city, temp):
        if year in self.years and city in self.cities:
            r = self.years.index(year)
            c = self.cities.index(city)
            self.data[r][c] = temp
        else:
            print("Invalid year or city")

    def delete(self, year, city):
        if year in self.years and city in self.cities:
            r = self.years.index(year)
            c = self.cities.index(city)
            self.data[r][c] = -9999  # Sentinel value for missing
        else:
            print("Invalid year or city")

    def retrieve(self, city, year):
        if year in self.years and city in self.cities:
            r = self.years.index(year)
            c = self.cities.index(city)
            value = self.data[r][c]
            return None if value == -9999 else value
        return None

    def rowMajorAccess(self):
        print("Row-Major Access (Year-wise):")
        for r in range(len(self.years)):
            for c in range(len(self.cities)):
                print(f"({self.years[r]}, {self.cities[c]}): {self.data[r][c]}")

    def columnMajorAccess(self):
        print("Column-Major Access (City-wise):")
        for c in range(len(self.cities)):
            for r in range(len(self.years)):
                print(f"({self.years[r]}, {self.cities[c]}): {self.data[r][c]}")

    def handleSparseData(self):
        sparse_repr = {}
        for r in range(len(self.years)):
            for c in range(len(self.cities)):
                if self.data[r][c] != -9999:
                    sparse_repr[(self.years[r], self.cities[c])] = self.data[r][c]
        return sparse_repr

    def analyzeComplexity(self):
        print("Time Complexity (Insert/Retrieve/Delete): O(1)")
        print("Space Complexity: O(Y * C), where Y=Years, C=Cities")


# -------------------------------
# Example Usage
# -------------------------------
if _name_ == "_main_":
    years = [2023, 2024, 2025]
    cities = ["Delhi", "Mumbai", "Chennai"]

    storage = WeatherDataStorage(years, cities)

    # Insert records
    storage.insert(2023, "Delhi", 35.5)
    storage.insert(2024, "Mumbai", 30.2)
    storage.insert(2025, "Chennai", 32.8)

    # Retrieve
    print("Retrieve:", storage.retrieve("Delhi", 2023))

    # Delete
    storage.delete(2024, "Mumbai")
    print("After Deletion:", storage.retrieve("Mumbai", 2024))

    # Row-major and column-major access
    storage.rowMajorAccess()
    storage.columnMajorAccess()

    # Sparse data representation
    print("Sparse Representation:", storage.handleSparseData())

    # Complexity analysis
    storage.analyzeComplexity()

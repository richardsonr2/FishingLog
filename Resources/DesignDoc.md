## 1. Problem Statement
Fishing Log is database of where you caught fish and what you used to catch them so that you never lose your 
fishing log in the river. Includes the ability to log what the fish was, what river it was on, and what fly 
(or bait) you used to catch them. You can add, edit and delete logs. Extensions would be to have it recommend 
something to fish with on that river based on the time of year and how most fish were caught during that time of year. 
Further extension would be adding exact coordinates on the river of where the fish was caught.


## 2. Use Cases

Fishing Log User Stories

U1. As a user I want to be able to create an account and log in so that my data can be accessed by only me.

U2. As a user I want to be able to create a log of a catch so I can keep track of my catches.

U3. As a user I want to be able to delete a log of a catch in case I no longer need it.

U4. As a user I want to be able to edit a log of a catch in case I over embellished the size of the fish.

U5. As a user I want to be able to see a list of all of my catches so I can view them all at the same time.

U6. As a user I want to be able to sort my catches by size, location, ect.. so that I can view them more comprehensively

U7. As a user I want to be able to search for a specific catch so I can find the catch I'm looking for.

U8. As a user I want to be able to look at the specifics of a catch so I can get all the information.

U9. As a user I want to be able to look at catches that are between a specific time frame.

STRETCH GOALS:

U10. As a user I want to be able to delete the photo so that I can remove any photos I accidently uploaded.

U11. As a user I want to be able to upload a photo of the fish I caught to remember the day.

U12. As a user I want to be able to get reccomended a fly to use based on previous data to help me pick the best one to use.

U13. As a user I want to be able to put in the exact coordinates of a catch so I can go back to that same spot easier.

U14. As a user I want to be able to customize my profile with a picture, favorites, and personal about me.

## 3. API

### 3.1. Public Models

```
// CatchLog

String userId;
List<String> catches;
```

```
// Catch

String catchId;
String date;
String location;
String fishSpecies;
String tackle;
```

### 3.2. Get CatchLog Endpoint

* Accepts `GET` requests to `/catchlog/:userid`
* Accepts a user ID and returns the corresponding CatchLog.
    * If the given user ID is not found, will throw a
      `UserNotFoundException`

### 3.3. Create CatchLog Endpoint

* Accepts `POST` requests to `/catchlog`
* Accepts data to create a new catchLog with a given customer ID. 
* Returns the new CatchLog.


### 3.4. Add Catch To CatchLog Endpoint

* Accepts `POST` requests to `/catchlog/:userid/catch`
* Accepts a user ID and a catch object to be added.
    * If the user is not found, will throw a `UserNotFoundException`
* By default, will insert the new catch to the end of the catchLog

### 3.5. Get Catch Endpoint

* Accepts `GET` requests to `/catchlog/:userid/catch/catchid`
* Retrieves all catches of a catchLog with the given user ID
    * Returns the catches in default order added
    * If the optional `order` parameter is provided, this API will return the
      catches sorted by date, fish or location
* If the user ID is found, but contains no catches, the list of catches will be empty
* If the user ID is not found, will throw a `UserNotFoundException`

![](Diagrams/Screenshot 2023-11-02 110149.png)


## 4. Tables

### 4.1. `Users`

```
userid // partition key, string
name // string
dateJoined // String
userBio // String
favLocation // String
favTackle // String

```

### 4.1. `CatchLog`

```
userId // partition key, string
catchId // sort key, number
date // string
fishSpecies // string
location // string
tackle // string
```
## 5. Pages

![](PAGES/Fishing Log Mockup View Catch.png)
![](PAGES/Fishing Log Mockup View Fishing Log.png)

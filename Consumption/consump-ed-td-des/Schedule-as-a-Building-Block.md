
### Background
Sunbird as on today focuses on following parameters to be referred as building block :

a) User Registry : User & Org

b) Asset Distribution : Knowledge Platform

Intent of this document is to propose a building block (i.e. Schedule which is time series) as part of Sunbird Architecture.


### Definition
“Schedule“ can be time of interest for one or more entities in the system. Different Example of Schedule:


1. Solar Irradiance Data Captured Every Hour


1. School Timetable


1. Individual Calendar


1. Vaccination TimeSlot


1. Doctor’s Appointment


1. Team Meeting


1. Travel Itinerary of a Person


1. Financial Analysis of Sales and Revenue of a Company


1. Smart Meter Reading


1. Timesheet



Vision of Schedule as a Building Block is intended to provide:



SchemaLess : Schema less store of time series data

Specification intended to solve the problem of time series

Infra to manage the timeseries data in project agnostic way

Self Managed Micro Services to manage the time series data



Ex: Model can be as follows:




```actionscript3
{
  time: ““,//PrimaryKey
  startTime : '',
  endTime : '',
  duration : '',
  //SearchableIndexes Attr1-ClientKey,Attr2-ClusteringKey, Attr3,Attr4,Attr5-CustomIndexes,
  SubKey1: “Attr1+Attr2“, // Cluster Key
  SubKey2: “Attr1+Attr2+Attr3“, // Identification Key 
  SubKey3: “Attr1+Attr2+Attr3+Attr4“, // Sub Identification Key
  SubKey4: “Attr1+Attr2+Attr3+Attr4+Attr5“, // Order Key
  metadata: {
    
  }//JSONObject
} 
```


Structure Diagram:





![](images/storage/Untitled%20Diagram.drawio.png)

Flow Diagram:

![](images/storage/Untitled%20Diagram.drawio1.drawio.png)

Use Cases and API required



Use Case: Time table of a class



a) Create a Time Table Entry for an hour by teacher

/api/v1/createTimeSchedule



b) View Time Table by User for each day/ configured set of days

/api/v1/view/readSchedule



c) Repeat Schedule for Prescribed days.

/api/v1/view/repeatSchedule



d) Fetch the TimeTable of a class

/api/v1/view/readScheduleOf





*****

[[category.storage-team]] 
[[category.confluence]] 

TELEHACK Proposal




Submission category

The Rise of No-code / Low-code (Challenge Statement)


Team members

Yeo Zhao Yong (Leader)
Jason Khoo
Ong Wee Keong
Say Xian Xun





Summary of project

A ‘Volunteer-to-Task’ management system (application) was developed to serve the interests of The Food Bank Singapore (Food Bank). The application features a
(1) Volunteer Management Dashboard
(2) Volunteer Events Management Form and Dashboard 
(3) Volunteer Hours Report generation 
(4) Volunteer Event Recommender Engine. 
The application also allows volunteers to register for volunteer events. 


Design Concept

Our team understands that the Food Bank is powered by a group of dedicated skilled volunteers who require a low maintenance and efficient technological solution. 

With the end users’ needs in mind, we have designed the application with the concept of minimising users’ touch points through maximising automated data pipelines using various technologies and tools described below. 

In terms of event management by the Food Bank’s administrator, the administrator could easily maintain (e.g. add / modify/ delete) the volunteer events via the Volunteer Events Management Form. 

In addition, volunteers who desire to sign up for a volunteer event with the Food Bank can easily sign up for a volunteer account on the application and register for the volunteer event via a simplified sign up form.

The data collected from the abovementioned form are automatically transmitted and synced to the dashboard and report visualisation summary with minimal user intervention. 


How project uses technology

Appsmith
Our team has adopted the use of Appsmith, an open source low-code framework, to build our front-end. Through Appsmith, we have brought together the mini-applications, including volunteer management dashboard, volunteer events management form, on a single platform and have also designed separate role-based access control and views for the (1) Food Bank’s administrator and (2) volunteers. 

Supabase 
We have adopted the use of Supabase, an open source postgres database low-code interface, for our backend with respect to the login credential for our main application. 

Google Sheets
Google sheets are used to store the information acquired from the Google Forms. Within the Google Sheets, there are queries (via Google Visualization API Query Language) and sorting algorithms to manipulate the data into appropriate formats (see Technical Write-up for more details). The cleaned data is then used to generate reports and visualisation through Google Data Studio.

Google Forms
Google Forms are used in two main areas: (1) Event Management Form for the Food Bank’s administrator to add / modify / delete volunteer events and (2) Volunteer Registration Form for volunteers to register for their interested volunteer events. Data collected from the above 2 forms are pushed to google sheets directly via Google Visualization API Query Language.

Google Data Studio
Google Data Studio is used in four main areas for reporting and visualisation purposes. The four areas are: (1) Volunteer Management Dashboard for volunteers profiling, (2) Event Management Dashboard for events details reporting (e.g. participation rate / number of events planned / event category summary), (3) Volunteer Hours Report where a personalised volunteer event participation summary can be generated and (4) Event Recommender Engine where Food Bank’s administrator could use it to recommend volunteer events to volunteer based on the volunteers’ interested event category and availability. 


Technical Write-up

Google Sheets - ‘Master Spreadsheet’ file

Participant Count
Objective: Achieve the count of the number of participants for each unique volunteer event.
Methodology: The unique event_sn is first derived via the unique formula in column C. Thereafter, using Google Apps Script, a macro (assigned to the green button) was created to perform a count on the occurrence of each unique event_sn. 


Add / Modify / Delete Event
Objective: Achieve the last updated active event entry (i.e. status of event is either Add / Modify) from the data collected from the Event Registration Form.
Methodology: The data collected from the Event Management Form  will be passed through a sorting and filtering algorithm - (1) The data is first sorted and filtered by date, the latest modified entries for each unique event_sn will be retained, (2) Thereafter, if the status of the latest modified entries is “Delete”, the entries will also be removed since such entries are not required to be pushed to the latest event details table. 

Add / Delete Event Registration by Volunteers
Objective: Achieve the last updated active event registration entry (i.e. status of registration is Register) from the data collected from the Event Registration Form.
Methodology: The data collected from the Volunteer Registration Form will be passed through a sorting, filtering and merging algorithm - (1) The data is first sorted and filtered by date, the latest modified entries for each unique pair of volunteer_id and event_sn will be retained, (2) Thereafter, if the status of the latest modified entries is “De-register”, the entries will also be removed since such entries are not required to be pushed to the latest event registration records. (3) Lastly, using Google Apps Script, a macro (assigned to the blue button) was created to perform a data cleaning step to add a prefix for both event_sn and volunteer_id, thereafter, the macro will merge the event details and volunteer details based on the event_sn and volunteer_id to produce the latest updated event registration table. 

Last Volunteer Date
Objective: Achieve the latest event date for each volunteer from the data collected from the latest updated event registration table.
Methodology: The data collected from the latest updated event registration table will be passed through a sorting algorithm - the data is sorted and filtered by date, the latest event date for each unique volunteer_id will be retained, thereafter, the latest event date will be updated to the Volunteer Database.

Recommender
Objective: Recommend best matched volunteer events for volunteers based on volunteers’ interest and availability
Methodology: The calculations listed in this worksheet is a low fidelity version of the main recommender engine used (please see below for description on the main recommender engine used in the project). Using the volunteers’ interest and availability details, a rule based matching was performed against the events’ event category and planned day via a filter. 

Google Sheets - ‘Recommender Engine’ file

Methodology: AlaSQLGS, a Google Apps Script project built on the AlaSQL project (an open source SQL database for JavaScript), was adopted in the data manipulation. Using the data from the ‘Volunteer Database’ and ‘Event Database’, a dual conditional filter based on the availability and interest was performed through an inner join to obtain all available matched volunteer events for each volunteer listed in the ‘Volunteer Database’ . 

Project attribution: 
AlaSQLGS: https://github.com/contributorpw/alasqlgs
AlaSQL: https://github.com/agershun/alasql


Pitch Video
https://drive.google.com/file/d/1qrQgAf_KzjV5gcHW_6g9bPN5sqpRzJY0/view?usp=sharing


Github Repo Link
https://github.com/telhk2/telehk-submission


List of Tech Stack
Coding languages used
Javascript (in app smith)

Programs used 
Appsmith (low-code)
Supabase (low-code)
Google Sheets (low-code)
Google Forms (no-code)
Google Data Studio (low-code)
Project Demo Link
Live working solution URL
https://app.appsmith.com/applications/6210f8f06b4b1e154a3f1638/pages/6210f8f06b4b1e154a3f163b

This section contains detail about the service APIs in the Registration Center Masterdata module

* [Registration Centers API](#registration-centers-api)
* [Registration Center - Device Mapping API](#registration-center-device-api)
* [Registration Center - Machine Mapping API](#registration-center-machine-api)
* [Registration Center - User - Machine Mapping API](#registration-center-user-machine-mapping-api)
* [Registration Center - Machine - Device API](#registration-center-machine-device-api)
* [Registration Center - Search API](#post-registrationcenterssearch)
* [Registration Center - Filter values](#registration-center-filter-values)
* [Registration Center Type - Search API](#post-registrationcentertypessearch)
* [Registration Center Type - Filter values](#post-regcentertypesfiltervalues)
* [Create/Update API](#createupdate-api)
* [Search API](#search-api)

# Registration Centers API
These APIs includes create, update and fetch APIs. Create and Update API is used by the Administrator Portal for the Create and Update Center functionality. Fetch APIs are used by Pre-Registration to display the List of Registration Centers on the UI for an Applicant to select and book appointments. Registration processor also uses the fetch API to validate if a packet is generated in an Authorized Registration Center or not.

* [POST /registrationcenters](#post-registrationcenters)
* [PUT /registrationcenters](#put-registrationcenters)
* [GET /registrationcenters](#get-registrationcenters)
* [GET /registrationcenters/{id}/{languagecode}](#get-registrationcentersidlanguagecode)
* [GET /getregistrationcenterholidays/{languagecode}/{registrationcenterid}/{year}](#get-getregistrationcenterholidayslanguagecoderegistrationcenteridyear)
* [GET /getlocspecificregistrationcenters/{langcode}/{locationcode}](#get-getlocspecificregistrationcenterslangcodelocationcode)
* [GET /getcoordinatespecificregistrationcenters/{languagecode}/{longitude}/{latitude}/{proximitydistance}](#get-getcoordinatespecificregistrationcenterslanguagecodelongitudelatitudeproximitydistance)
* [GET /registrationcentershistory/{id}/{languagecode}/{eff_dtimes}](#get-registrationcentershistoryidlanguagecodeeff_dtimes)
* [GET /getregistrationmachineusermappinghistory/{eff_dtimes}/{registrationcenterid}/{machineid}/{userid}](#get-getregistrationmachineusermappinghistoryeff_dtimesregistrationcenteridmachineiduserid)
* [GET /getlocspecificregistrationcenters/{hierarchylevel}/{textvalue}/{languagecode}](#get-getlocspecificregistrationcentershierarchyleveltextvaluelanguagecode)

## POST /registrationcenters
This service will create the list of Registration Centers which are used in the MOSIP platform. 
Please find the steps to [create primary/secondary languages](#create-update-api) 

### Resource URL
`POST /registrationcenters`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
name|Yes|Name of the registration center| | 
centertypecode|Yes|Code of the center type| | 
addressline1|Yes|Line 1 of the address| | 
addressline2|No|Line 2 of the address| | 
addressline3|No|Line 3 of the address| | 
locationcode|Yes|Code of the location of the registration center| | 
longitude|Yes|Longitude of the registration center| | 
latitude|Yes|Latitude of the registration center| | 
contactphone|No|Contact phone number of the registration center| |  
workinghours|Yes|Working hours of the registration center| | 
perkioskprocesstime|Yes|Process time per kiosk in the registration center| | 
centerstarttime|Yes|Office start time of the registration center| | 
centerendtime|Yes|Office end time of the registration center| | 
holidaylocationcode|Yes|Holiday location of the registration center| | 
contactperson|No|Contact person of the registration center| | 
lunchstarttime|No|Lunch start time of the registration center| | 
lunchendtime|No|Lunch end time of the registration center| | 
timezone |No | time zone of the registration center | |
lang_code |Yes | language code  | |

### Example Request
```JSON
{
	"id": "string",
	"metadata": null,
	"request": {
		"addressLine1": "address 1",
		"addressLine2": "",
		"addressLine3": "",
		"centerEndTime": "18:00:00",
		"centerStartTime": "09:30:00",
		"centerTypeCode": "REG",
		"contactPerson": "",
		"contactPhone": "",
		"holidayLocationCode": "KTA",
		"langCode": "eng",
		"latitude": "2.1111",
		"locationCode": "14000",
		"longitude": "2.1111",
		"lunchEndTime": "00:00:00",
		"lunchStartTime": "00:00:00",
		"name": "Regcenter 1",
		"perKioskProcessTime": "00:15:00",
		"timeZone": "(GTM+01:00) CENTRAL EUROPEAN TIME",
		"workingHours": 8.5,
		"zoneCode": "TTA",
		"id": "",
		"isActive": false
	},
	"version": "1.0",
	"requesttime": "2019-11-18T10:46:23.956Z"
}
```
### Error Response:
``` JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
 "response": null
}

```

### Failure details
Error Code  | Error Message | Error Description
-----|----------|-------------
KER-MSD-500 |Internal Server Error|If system error occurs
KER-ATH-403 |Forbidden|If unauthorized role detected
KER-ATH-401 |Authentication Failed|If no role/invalid token is detected
KER-MSD-060 |Error occurred while Inserting Registration Center details|If any error occur from database
KER-MSD-303 |Received data is not present in all Languages supported by MOSIP|If all the mandatory data is not received in all the configured languages
KER-MSD-306 |Records with duplicate language code found|if records received contain duplicate language codes
KER-MSD-307 |Latitude or Longitude must have minimum 4 digits after decimal|If the Latitude and/or Longitude are in invalid format
KER-MSD-308 |Center Lunch Start Time must be smaller than Center Lunch End Time|If Center Lunch start time is bigger than Center Lunch End Time
KER-MSD-309|Center Start Time must be smaller than Center End Time|If Center Start time is bigger than Center End Time

## PUT /registrationcenters
This service will update the list of Registration Centers which are used in the MOSIP platform. 

### Resource URL
`PUT /registrationcenters`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
name|Yes|Name of the registration center| | 
id|Yes|Id of the registration center| | Incase of Primary empty and Generated id incase of Secondary 
centertypecode|Yes|Code of the center type| | 
addressline1|Yes|Line 1 of the address| | 
addressline2|No|Line 2 of the address| | 
addressline3|No|Line 3 of the address| | 
locationcode|Yes|Code of the location of the registration center| | 
longitude|Yes|Longitude of the registration center| | 
latitude|Yes|Latitude of the registration center| | 
contactphone|No|Contact phone number of the registration center| |  
workinghours|Yes|Working hours of the registration center| | 
perkioskprocesstime|Yes|Process time per kiosk in the registration center| | 
centerstarttime|Yes|Office start time of the registration center| | 
centerendtime|Yes|Office end time of the registration center| | 
holidaylocationcode|Yes|Holiday location of the registration center| | 
isactive|Yes|Is the registration center active| | 
contactperson|No|Contact person of the registration center| | 
lunchstarttime|No|Lunch start time of the registration center| | 
lunchendtime|No|Lunch end time of the registration center| | 
timezone |No | time zone of the registration center | |
lang_code |Yes | language code  | |
numberOfKiosks|No | Number of Kiosks  | |

### Example Request
```JSON
{
	"id": "string",
	"metadata": null,
	"request": {
		"addressLine1": "address 1",
		"addressLine2": "",
		"addressLine3": "",
		"centerEndTime": "18:00:00",
		"centerStartTime": "09:30:00",
		"centerTypeCode": "REG",
		"contactPerson": "fdsf",
		"contactPhone": "",
		"holidayLocationCode": "KTA",
		"langCode": "eng",
		"latitude": "2.1111",
		"locationCode": "14000",
		"longitude": "2.1111",
		"lunchEndTime": "00:00:00",
		"lunchStartTime": "00:00:00",
		"name": "Regcenter 21",
		"perKioskProcessTime": "00:15:00",
		"timeZone": "(GTM+01:00) CENTRAL EUROPEAN TIME",
		"workingHours": "8.5",
		"zoneCode": "TTA",
		"id": "10936",
		"isActive": true,
		"numberOfKiosks": 0
	},
	"version": "1.0",
	"requesttime": "2019-12-02T15:32:26.503Z"
}
```

### Error Response:
```
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
 "response": null
}

```

### Failure details
Error Code | Error Message | Error Description
----- |----------|-------------
KER-MSD-500 |Internal Server Error|If system error occurs
KER-ATH-403 |Forbidden|If unauthorized role detected
KER-ATH-401 |Authentication Failed|If no role/invalid token is detected
KER-ATH-111 |Error occurred while updating Registration Center details|If any error occur from database
KER-MSD-303 |Received data is not present in all Languages supported by MOSIP|If all the mandatory data is not received in all the configured languages
KER-MSD-304 |Center IDs received for all languages is not same|If all the IDs received are not same for data in all the languages
KER-MSD-305 |Center ID and Language Code combination is not unique in the request received|If combination of Center ID and Language code in duplicate in request
KER-MSD-306 |Records with duplicate language code found|if records received contain duplicate language codes
KER-MSD-307 |Latitude or Longitude must have minimum 4 digits after decimal|If the Latitude and/or Longitude are in invalid format
KER-MSD-308 |Center Lunch Start Time must be smaller than Center Lunch End Time|If Center Lunch start time is bigger than Center Lunch End Time
KER-MSD-309 |Center Start Time must be smaller than Center End Time|If Center Start time is bigger than Center End Time

## GET /registrationcenters
This service will provides the service for the List of Registration Centers. 

### Resource URL
`GET /registrationcenters`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-


### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
  "registrationcenters": [
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
	},
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
	}
   ]
 }
}
```

## GET /registrationcenters/{id}/{languagecode}
This service will provides the service for the List of Registration Centers. 

### Resource URL
`GET /registrationcenters/{id}/{languagecode}`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
  "registrationcenters": [
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
	},
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
       	}
   ]
 }
}
```

## GET /getregistrationcenterholidays/{languagecode}/{registrationcenterid}/{year}
This service will list of holidays for a particular registration center for that particular year. 

### Resource URL
`GET /getregistrationcenterholidays/{languagecode}/{registrationcenterid}/{year}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
registrationcenterid|Yes|ID of the registration center| | 
year|Yes|The year for which the list of holidays is listed| | 


### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
  "registrationcenter": [
	{
		"registrationcentername":"",
		"centertypecode":"",
		"addressline1":"",
		"addressline2":"",
		"addressline3 ":"",
		"longitude ":"",
		"latitude":"",
		"contactphone":"",
		"numberofkiosks":"",
		"workinghours":"",
		"perkioskprocesstime":"",
		"officestarttime":"",
		"officeendtime":"",
		"holidaylocationcode":"",
		"isactive":"",
		"centertype":"",
		"address":"",
		"workinghours":"",
		"contactnumber":"",
		"pincode":"",
		"locationcode":"",
		"holidays": [
			"holiday" : {
				"holidayID": "string",
				"holidayDate": "string",
				"holidayName": "string",
				"holidayDay": "string",	
				"holidayMonth": "string",
				"holidayYear": "string",
				"languagecode":"string"
			           }
		            ]		
	  }
     ]
   }
}
```
200


## GET /getlocspecificregistrationcenters/{langcode}/{locationcode}
This service will return a list of enrollment center details based on the location code 

### Resource URL
`GET /getlocspecificregistrationcenters/{langcode}/{locationcode}`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
locationcode|Yes|The location code for which the list of enrollment centers are needed| | 


### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
  "registrationCenters": [
    {
          "addressLine1": "string",
          "addressLine2": "string",
          "addressLine3": "string",
          "centerEndTime": "HH:mm:ss",
          "centerStartTime": "HH:mm:ss",
          "centerTypeCode": "string",
          "contactPerson": "string",
          "contactPhone": "string",
          "holidayLocationCode": "string",
          "id": "string",
          "isActive": true,
          "languageCode": "string",
          "latitude": "string",
          "locationCode": "string",
          "longitude": "string",
          "lunchEndTime": "HH:mm:ss",
          "lunchStartTime": "HH:mm:ss",
          "name": "string",
          "numberOfKiosks": 0,
          "perKioskProcessTime": "HH:mm:ss",
          "timeZone": "string",
          "workingHours": "string"
       }
   ]
 }
}
```
200

Description: OK

## GET /getcoordinatespecificregistrationcenters/{languagecode}/{longitude}/{latitude}/{proximitydistance}
This service will return a list of enrollment center details based on the coordinates

### Resource URL
`GET /getcoordinatespecificregistrationcenters/{languagecode}/{longitude}/{latitude}/{proximitydistance}`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
languagecode|Yes|Language code in Language code in ISO 639-2 format| | 
longitude|Yes|The longitude for which the list of enrollment centers are needed| | 
latitude|Yes|The latitude code for which the list of enrollment centers are needed| | 
proximitydistance|Yes|The proximity diameter in meter| | 


### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
  "registrationcenter": [
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
	   }
     ]
  }
}
```
200

Description: Success

## GET /registrationcentershistory/{id}/{languagecode}/{eff_dtimes}

This service will provides the service for the List of Registration Centers History. 

### Resource URL
`GET /registrationcentershistory/{id}/{languagecode}/{eff_dtimes}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-


### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response":{
  "registrationcenters": [
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
	},
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
	}
    ]
  }
}
```
200

Description: Success

## GET /getregistrationmachineusermappinghistory/{eff_dtimes}/{registrationcenterid}/{machineid}/{userid}

This service will provides the history of mappings of mapping History of Registration, Machine and User based on Registration Center ID, Machine ID, User ID, Date and Language Code 

### Resource URL
`GET /getregistrationmachineusermappinghistory/{eff_dtimes}/{registrationcenterid}/{machineid}/{userid}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
languagecode|Yes|Language code in Language code in ISO 639-2 format| | 
eff_dtimes|Yes|From which date this change is with effective| | 2018-11-02T05:20:31.075
registrationcenterid|Yes|ID of the registration center| | 
machineid|Yes|ID of the machine| | 

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response":{
  "registrationcenters": [
	{
		"registrationcenterid":"string",
		"machineid":"string",
		"userid":"string"
	},
	{
		"registrationcenterid":"string",
		"machineid":"string",
		"userid":"string"
	}
    ]
  }
}
```
200

Description: Success

## GET /getlocspecificregistrationcenters/{hierarchylevel}/{textvalue}/{languagecode}
This service will return a list of enrollment center details based on hierarchy level, text value and language code

### Resource URL
`GET /getlocspecificregistrationcenters/{hierarchylevel}/{textvalue}/{languagecode}`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
hierarchylevel|Yes|The hierarchy level for which the list of enrollment centers are needed| | 
textvalue|Yes|This is a free text. The search will happen with the combination of hierarchy level, language code and this free text. The enrollment centers which satisfy these 3 criteria will be returned| | 
languagecode|Yes|The enrollment center description will be returned in this language code | | 

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response":{
  "registrationcenter": [
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
	 }
     ]
  }
}
```
200

Description: Success

### Failure Response:
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
  "response" : null
}
```

### Failure details
Error Code | Error Message | Error Description
------------|------------------------------|-------------
KER-MSD-041 | Error occurred while fetching Registration Centers | registration center fetch exception
KER-MSD-111 | Error occurred while updating Registration Center details | registration center update exception
KER-MSD-112 | Error occurred while deleting Registration Center details | registration center delete exception
KER-MSD-042 | Registration Center not found | registration center not found
KER-MSD-149 | Cannot delete as dependency found | dependency exception
KER-MSD-043 | Invalid date format | date time parse exception
KER-MSD-XXX | start/end time Data not configured in database | data to be validated with not found

# Registration Center User Machine Mapping API

These APIs includes map and un-map API. Both these APIs are used by the Administrator Portal for the Create and Remove Center-Machine Mapping functionality.

* [POST /registrationmachineusermappings](#post-registrationmachineusermappings)
* [GET /getregistrationmachineusermappinghistory/{effdtimes}/{registrationcenterid}/{machineid}/{userid}](#get-getregistrationmachineusermappinghistoryeffdtimesregistrationcenteridmachineiduserid-1)
* [PUT /registrationmachineusermappings](#put-registrationmachineusermappings-1)

## POST /registrationmachineusermappings
This service will create a Registration Center-User-Machine Mapping which are used in the MOSIP platform. 

### Resource URL
`POST /registrationmachineusermappings`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
cntrId|Yes|Registration Center Id for request| | 
machineId|Yes|Machine Id for request| | 
usrId|Yes|User Id for request| | 
isActive|Yes|Mapping is active or not| | 

### Example Request
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
    "cntrId": "RC001",
    "isActive": true,
    "machineId": "MC001",
    "usrId": "QC001"
  }
}
```

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
            "cntrId": "RC001",
            "machineId": "MC001",
            "usrId": "QC001"
            }
}
```

### Response codes
200

Description: Success

## GET /getregistrationmachineusermappinghistory/{effdtimes}/{registrationcenterid}/{machineid}/{userid}
This service will provides the service for the Center-User-Machine with their history. 

### Resource URL
`GET /getregistrationmachineusermappinghistory/{effdtimes}/{registrationcenterid}/{machineid}/{userid}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
ID|Yes|Machine History Id|
effdtimes|Yes|Effective Date and Time of the Machine|
registrationcenterid|Yes|Registration Center Id|
machineid|Yes|Machine Id |
userid|Yes|User Id|

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response":  {
      "registrationCenters": [
             {
              "cntrId": "string",
              "effectivetimes": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
              "isActive": true,
              "langCode": "string",
              "machineId": "string",
              "usrId": "string"
             }
        ]
    }
}
```
200

Description: Success

## PUT /registrationmachineusermappings
This service will create or update a Registration Center-User-Machine Mapping which are used in the MOSIP platform. 

### Resource URL
`PUT /registrationmachineusermappings`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
cntrId|Yes|Registration Center Id for request| | 
machineId|Yes|Machine Id for request| | 
usrId|Yes|User Id for request| | 
isActive|Yes|Mapping is active or not| | 

### Example Request
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
      "cntrId": "RC001",
      "isActive": true,
      "langCode": "string",
      "machineId": "MC001",
      "usrId": "QC001"
  }
}
```
### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
    "mapped": [
      {
        "cntrId": "string",
        "machineId": "string",
        "usrId": "string"
      }
    ],
    "notmapped": [
       {
        "cntrId": "string",
        "machineId": "string",
        "usrId": "string"
      }
    ]
  }
}
```
### Response codes
201

### Failure Response:
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
  "response" : null
}
```

### Failure details
Error Code | Error Message | Error Description
------------|------------------------------|-------------
KER-MSD-078 | Error occurred while inserting mapping of Center, User and Machine details | registration center user machine mapping insert exception
KER-MSD-131 | Registration Center, Machine and User Mapping not found | registration center user machine not found
KER-MSD-108 | Error occurred while deleting mapping of Center, User and Machine details | registration center user machine delete exception
KER-MSD-136 | Error occurred while updating mapping of Center, User and Machine details | registration center user machine update exception

# Registration Center Machine API
These APIs includes map and un-map API. Both these APIs are used by the Administrator Portal for the Create and Remove Center-Machine Mapping functionality.

* [POST /registrationcentermachine](#post-registrationcentermachine)
* [DELETE /registrationcentermachine/{regCenterId}/{machineId}](#deleteregistrationcentermachineregcenteridmachineid)

## POST /registrationcentermachine
This service will create the mapping of registration canter and machine in the RegistrationCenterMachine Master module. 

### Resource URL
`POST /registrationcentermachine`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
machineId|Yes|Available machine id| | 
regCenterId|Yes|Available registration center| | 

### Example Request
```JSON  
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
    "isActive": true,
    "langCode": "string",
    "machineId": "MC001",
    "regCenterId": "RC001"
  }
}


```
### Example Response
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response": {
      "machineId": "string",
      "regCenterId": "string"
  }
}
```
### Response codes
201

Description: Created

## DELETE/registrationcentermachine/{regCenterId}/{machineId}
This service will provides the service for delete mapping of  Center-Machine. 

### Resource URL
`DELETE /registrationcentermachine/{regCenterId}/{machineId}`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
regCenterId|Yes|Registration Center Id|
machineId|Yes|Machine Id |

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":  {
  "machineId": "MC001",
  "regCenterId": "RC001"
   }
}
```
200

Description: Success

### Failure Response:
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
  "response" : null
}
```

### Failure details
Error Code | Error Message | Error Description
------------|------------------------------|-------------
KER-MSD-074 | Error occurred while inserting a mapping of Machine and Center | registration center machine create exception
KER-MSD-114 | Mapping for Machine and Center not found | registration center machine data not found
KER-MSD-106 | Error occurred while deleting a mapping of Machine and Center | registration center machine delete exception

# Registration Center Device API
These APIs includes map and un-map API. Both these APIs are used by the Administrator Portal for the Create and Remove Center-Device Mapping functionality.

* [GET /registrationcenterdevice/map/{regCenterId}/{deviceId}](#get-registrationcenterdevicemapregcenteriddeviceid)
* [PUT /registrationcenterdevice/unmap/{deviceId}/{regCenterId}](#put-registrationcenterdeviceunmapdeviceidregcenterid)

## GET /registrationcenterdevice/map/{regCenterId}/{deviceId}
This service will create the mapping of registration canter and device in the RegistrationCenterDevice Master module. 

### Resource URL
`GET /registrationcenterdevice/map/{regCenterId}/{deviceId}`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
deviceId|Yes|Available device id| | 
regCenterId|Yes|Available registration center| | 

### Example Request
```https://mosip.io/v1/masterdata/registrationcenterdevice/map/10001/4cb310e3-965a-4afd-a28e-0db6b3db5423```

### Example Response
```JSON
{
  "id": null,
  "version": null,
  "responsetime": "2020-02-06T06:06:52.037Z",
  "metadata": null,
  "response": {
    "status": "Success",
    "message": "DeviceId 4cb310e3-965a-4afd-a28e-0db6b3db5423 has been mapped to registration center 10001"
  },
  "errors": null
}
```
### Response codes
200

### Failure Response:
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
  "response" : null
}
```

### Failure details
Error Code | Error Message | Error Description
------------|------------------------------|-------------
KER-MSD-411 | Admin not authorized to map/un-map this Registration Center | when user zone doesn't belong to the same zone of center
KER-MSD-415 | Admin not authorized to map/un-map this Device | when user zone doesn't belong to the same zone of device
KER-MSD-418 | Cannot map as the Registration Center/Device is Decommissioned | When center/device trying to map is decomissioned
KER-MSD-419 | Cannot map the Device as it is mapped to another Registration Center | When the center/device are already mapped to center
KER-MSD-416 | Device cannot be mapped to the Center as Center and Device does not belong to the same Administrative Zone | When the device doesn't belong to same category

## PUT /registrationcenterdevice/unmap/{deviceId}/{regCenterId}
This service will provides the service for un map the mapping of Device and Registration Center. 

### Resource URL
`PUT /registrationcenterdevice/unmap/{deviceId}/{regCenterId}`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
regCenterId|Yes|Registration Center Id|
deviceId|Yes|Device Id |

### Request
```
https://mosip.io/v1/masterdata/registrationcenterdevice/unmap/4cb310e3-965a-4afd-a28e-0db6b3db5423/10001
```
### Example Response
```JSON
{
  "id": null,
  "version": null,
  "responsetime": "2020-02-06T06:57:11.596Z",
  "metadata": null,
  "response": {
    "status": "un-mapped",
    "message": "Device 4cb310e3-965a-4afd-a28e-0db6b3db5423 is successfully Un-Mapped to the Registration Center 10001 "
  },
  "errors": null
}
```
### Failure Response:
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
  "response" : null
}
```
### Failure details
Error Code | Error Message | Error Description
------------|------------------------------|-------------
KER-MSD-411 | Admin not authorized to map/un-map this Registration Center | when user zone doesn't belong to the same zone of center
KER-MSD-415 | Admin not authorized to map/un-map this Device | when user zone doesn't belong to the same zone of device
KER-MSD-435 | Device Id %s - Center Id %s mapping does not exist | when center/device trying to unmap doesn't exist
KER-MSD-434 | Device-Registration Center un-mapping already exist | When the center/device mapping already exists
KER-MSD-416 | Device cannot be mapped to the Center as Center and Device does not belong to the same Administrative Zone | When the device doesn't belong to same category
KER-MSD-436 | Error occurred while mapping Device to Registration Center | Exception while mapping device to registration center

# Registration Center Machine Device API
These APIs includes map, un-map and fetch mapping APIs. The Map and Un-Map APIs are used to create/remove Center-Machine-Device mapping.

* [POST /registrationcentermachinedevice](#post-registrationcentermachinedevice)
* [DELETE /registrationcentermachinedevice/{regcenterid}/{machineid}/{deviceid}](#delete-registrationcentermachinedeviceregcenteridmachineiddeviceid)

## POST /registrationcentermachinedevice
This service will create the mapping of registration center, machine and device in the RegistrationCenterMachineDevice Master module. 

### Resource URL
`POST /registrationcentermachinedevice`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
machineId|Yes|Available machine id| | 
regCenterId|Yes|Available registration center| | 
deviceId|Yes|Available device id| | 

### Example Request
```JSON  
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
    "deviceId": "string",
    "isActive": true,
    "langCode": "string",
    "machineId": "string",
    "regCenterId": "string"
  }
}
```
### Example Response
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":   {
   "deviceId": "string",
   "machineId": "string",
   "regCenterId": "string"
  }
}
```
### Response codes
201

Description: Created

## DELETE /registrationcentermachinedevice/{regcenterid}/{machineid}/{deviceid}
This service will delete the mapping of registration center, machine and device in the RegistrationCenter-Machine-Device Master module. 

### Resource URL
`DELETE /registrationcentermachinedevice/{regcenterid}/{machineid}/{deviceid}`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
NA

### Example Response
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":  {
   "deviceId": "string",
   "machineId": "string",
   "regCenterId": "string"
  }
}
```
### Response codes
200

Description: Success

### Failure Response:
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
  "response" : null
}
```

### Failure details
Error Code | Error Message | Error Description
------------|------------------------------|-------------
KER-MSD-076 | Error occurred while inserting a mapping of Center, Machine and Device | registration center machine device create exception
KER-MSD-107 | Error occurred while deleting a mapping of Center, Machine and Device | registration center machine device delete exception
KER-MSD-116 | Mapping for Center, Machine and Device not found | registration center machine device data not found exception

# Registration Center search APIs
This API is used by the Administrator Portal to fetch the list of Registration Centers based on a given filter criteria to display the list of Registration Centers on the Portal UI.

* [POST /registrationcenters/search](#post-registrationcenterssearch)

## POST /registrationcenters/search
This service is for the registration centers search functionality. All the filter parameters are passed and the registration centers are searched and the matching results are returned. 

### Resource URL
`POST /registrationcenters/search`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
filters|No|Array of the filter applied. In case of "list" screen, this array will be empty| -NA- |
columnName|No|The column name in the JSON response| -NA- |
type|No|The value have to be in ["contains","startsWith","equals","between"]| -NA- |
value|No|Value or id selected in the filter by the end user| -NA- |
fromValue|No|If the type is "between", this field is the start value| -NA- |
toValue|No|If the type is "between", this field is the end value| -NA- |
languagecode|Yes|Language code in Language code in ISO 639-2 format| | 
sort|No|This is an array of the sort field and type| | 
sortfield| The field on which the sort is applied | | modifiedDate
sorttype| This should be either of ['ASC','DESC']| | ASC
pagination|The pagination parameter object| |
pageStart|This is the start index | 0 | 0
pageFetch| This is the amount of records to be fetched | 10 | 10

### Filter Columns
Please find the filter columns used in search:

1. id
2. name
3. centerTypeCode
4. locationCode
5. status

### Example Request
```JSON
{
	"id": "string",
	"metadata": {},
	"requesttime": "2018-12-10T06:12:52.994Z",
	"version": "string",
	"request": {
		"filters" : [
			{
				"columnName": "",
				"type": "",
				"value": "",  
				"fromValue": "",
				"toValue": "",
				"languageCode":""
			}
		],
		"sort":[
			{
				"sortfield":"string",
				"sorttype":"ASC"
			}
		],
		"pagination":{
			"pageStart":"number",
			"pageFetch":"number"
		}
		
	}
}
```

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
  "data": [
	{
        "addressLine1": "string",
        "addressLine2": "string",
        "addressLine3": "string",
        "administrativeZone": "string",
        "administrativeZoneCode": "string",
        "centerEndTime": "HH:mm:ss",
        "centerStartTime": "HH:mm:ss",
        "centerTypeCode": "string",
        "centerTypeName": "string",
        "city": "string",
        "cityCode": "string",
        "contactPerson": "string",
        "contactPhone": "string",
        "createdBy": "string",
        "devices": "number",
        "holidayLocation": "string",
        "holidayLocationCode": "string",
        "id": "string",
        "isActive": "boolean",
        "isDeleted": "boolean",
        "langCode": "string",
        "latitude": "string",
        "locationCode": "string",
        "longitude": "string",
        "lunchEndTime": "HH:mm:ss",
        "lunchStartTime": "HH:mm:ss",
        "machines": "number",
        "name": "string",
        "numberOfKiosks": "number",
        "perKioskProcessTime": "HH:mm:ss",
        "postalCode": "string",
        "province": "string",
        "provinceCode": "string",
        "region": "string",
        "regionCode": "string",
        "timeZone": "string",
        "updatedBy": "string",
        "users": "number",
        "workingHours": "string",
        "zone": "string",
        "zoneCode": "string"
      }
   ],
	"fromRecord" : "number",
	"toRecord":"number",
	"totalRecord":"number"
 }
}
```
# Registration Center filter values
This API is used by the Administrator Portal to fetch the list of Registration Centers based on a given filter criteria to display the list of Registration Centers on the Portal UI.

* [POST /registrationcenters/filtervalues](#post-registrationcentersfiltervalues)

## POST /registrationcenters/filtervalues

This service returns the filter values which are required in the dropdown entries of the filter screen.  

### Resource URL
`POST /registrationcenters/filtervalues`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
filters|No|Array of the filter applied. In case of "list" screen, this array will be empty| -NA- |
columnName|No|The column name in the JSON response| -NA- |
type|No|The value have to be in ["unique","all"]| unique | unique
languagecode|Yes|Language code in Language code in ISO 639-2 format| | 

### Example Request
```JSON
{
	"id": "string",
	"metadata": {},
	"requesttime": "2018-12-10T06:12:52.994Z",
	"version": "string"
	"request": {
		"filters" : [
			{
				"columnName": ""
				"type": "unique"
			}
		],
		"languageCode": "string",
	}
}
```

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
  "filters": [
	{
		"fieldID": "string",
		"fieldCode":"string",
		"fieldValue": "string"
	}
   ]
 }
}
```
# Registration Center Type Search APIs
This API is used by the Administrator Portal to fetch the list of Registration Center Types based on a given filter criteria to display the list of Registration Center Types on the Portal UI.

* [POST /registrationcentertypes/search](#post-registrationcentertypessearch)

## POST /registrationcentertypes/search
This service is for the registration center types search functionality. All the filter parameters are passed and the registration center types are searched and the matching results are returned. 

### Resource URL
`POST /registrationcentertypes/search`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
filters|No|Array of the filter applied. In case of "list" screen, this array will be empty| -NA- |
columnName|No|The column name in the JSON response| -NA- |
type|No|The value have to be in ["contains","equals","startsWith","between"]| -NA- |
value|No|Value or id selected in the filter by the end user| -NA- |
fromValue|No|If the type is "between", this field is the value of the start range| -NA- |
toValue|No|If the type is "between", this field is the value of the end range| -NA- |
languagecode|Yes|Language code in Language code in ISO 639-2 format| | 
sort|No|This is an array of the sort field and type| | 
sortfield| The field on which the sort is applied | | modifiedDate
sorttype| This should be either of ['ASC','DESC']| | ASC
pagination|The pagination parameter object| |
pageStart|This is the start index | 0 | 0
pageFetch| This is the amount of records to be fetched | 10 | 10

### Filter Values
Filter Name| Search Values
-----|----------
status|["contains","equals","startsWith"]

### Example Request
```JSON
{
	"id": "string",
	"metadata": {},
	"requesttime": "2018-12-10T06:12:52.994Z",
	"version": "string",
	"request": {
		"filters" : [
			{
				"columnName": "",
				"type": "in",
				"value": "", 
				"fromValue": "",
				"toValue": ""
			}
		],
		"sort":[
			{
				"sortfield":"string",
				"sorttype":"ASC"
			}
		],
		"pagination":{
			"pageStart":"number",
			"pageFetch":"number"
		},
		"languageCode":""
		
	}
}
```

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
  "registrationcentertypes": [
	{
		"code": "string",
                "langCode": "string",
                "name": "string",
                "descr": "string",
                "isActive": true
	}
   ],
	"fromRecord" : "number",
	"toRecord":"number",
	"totalRecord":"number"
 }
}
```

# Registration Center Types Filter values
This API is used by the Administrator Portal UI to populate filter dropdowns on the Registration Center Type List View UI Screen.

* [POST /regcentertypes/filtervalues](#post-regcentertypesfiltervalues)

## POST /regcentertypes/filtervalues
This service returns the filter values which are required in the dropdown entries of the filter screen.  

### Resource URL
`POST /regcentertypes/filtervalues`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
filters|No|Array of the filter applied. In case of "list" screen, this array will be empty| -NA- |
columnName|No|The column name in the JSON response| -NA- |
type|No|The value have to be in ["unique","all"]| unique | unique
languagecode|Yes|Language code in Language code in ISO 639-2 format| | 

### Example Request
```JSON
{
	"id": "string",
	"metadata": {},
	"requesttime": "2018-12-10T06:12:52.994Z",
	"version": "string"
	"request": {
		"filters" : [
			{
				"columnName": "",
				"type": "unique"
			}
		],
		"languageCode": "string"
	}
}
```

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
  "filters": [
	{
		"fieldID": "string",
		"fieldCode":"string",
		"fieldValue": "string"
	}
   ]
 }
}
```

# Create/Update API
This API is a utility used by all the Create and Update APIs to perform multi-language data validation on the input received from Administrator Portal UI.

All the Create API's use the common class to create masterdata, Please find the important points to be taken care 

Create : 
* Primary language must be created first and then id must be passed in the secondary language request.
* Primary id must be passed blank for primary language request.
* Primary language will not be activated unless Secondary language is created.
* Primary Id for Center/Machine will be sequential Id's and other masterdata's will be auto generated values.

Update :
* Activation and deactivation will be done , If we only pass the primary language with active/deactivate in the request.

# Search API
This API is a utility used by all the Masterdata Search APIs to accept the filter criteria and form a query to fetch data from the Database.
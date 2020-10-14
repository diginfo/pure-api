# Pure Manufacturing API

## Introduction
API requests in Pure Manufacturing are calls that are made via secure https POST requests, to the backend HTTP Server.

For security reasons, raw SQL requests are NOT exposed directly either via http request, or via direct SQL connections to the database TCP socket on the server.

It is not possible through the API to execute an SQL statement directly, all requests must be performed by calling a pre-defined sqlid.

## API Requests

### Overview
All API requests call backend functions know as **SQLIDs** (_sqlid), these are unique, pre-defined functions that translate requests sent via http, into SQL queries, that are performed on the database.

SQLID functions also contain code that performs data validation, and often complex calculations on data queried, before being returned to the request, and / or before being saved to the database.

Request id's that are prefixed with an underscore '_' are commands / options, and all other fields not prefixed with an underscore are data field IDs that are used in record selection / filtering.

For security reasons, we do not publish a list of all sqlids and the data and filter fields they contain or require. This information is available through our support / helpdesk system on a case by case basis.

### Request Example

```javascript
{
	_userid: 'myuser',
	_passwd: 'mypass',
	_sqlid: 'inv^partall',
	_func: 'get',
	_format: 'json'

	PART_ID: '001-0002-003',

}
```

### API Request Fields

#### _passwd
- description: password authentication for the user
- example: _passwd = 'mypass'

#### _userid
- description: A unique user ID managed though the system user manager.
- example: _userid = 'myuser'

#### _sqlid
- description: A pre-defined backend function id that queries the database and / or performs actions on the data requested or sent. Each sqlid is prefixed with the module ID and the carat '^' delimter. In other systems, these are often known as 'endpoints'.
- example: inv^partall = module^function-name

#### _func
- description: The action to perform, get a record, add a new record, delete a record, update a record.
- example: _func=get, _func=add, _func=del, _func=upd

#### _format
- description: The format of the response data, either the default JSON or XML.
- example: _format=json, format=xml

#### PART_ID
- example: PART_ID=001-0002-003
- description: This has no underscore prefix and so is a data field. It is the key field used to select / filter the required record. There might be multiple keys to filter the request to return the requested data, and each sqlid has diferent filter fields.


## API Response

## Overview
Response data is returned by default as JSON, but may optionaly be returned as XML using the _format: 'xml' option above.

A response may be either a JSON Object `{}` or a JSON array `[]` Depending upon the type of data requested.

Generally, if a response contains a single record, then it will be returned as an object `{}` and if the response contains multiple records then it is returned as an array of objects `[{},{},{}]`.


### Example Response: 

The following is a JSON response for the example API request above.

It returns an object `{}` as this is a single record.

```javascript

{"ROWID":2352,"ID":"001-0002-003","DESCRIPTION":"Gripper Clamp Body","ALIAS_DESC":"CLAMP","USER_1":"","USER_2":"","USER_3":"","USER_4":"","USER_5":"","USER_6":"","USER_7":"","USER_8":"","USER_9":"","USER_10":"","PART_CLASS_ID":"MAKE_STAGED","TRACEABLE":"N","LOT_SIZE":0,"TRACE_USER_1_LBL":"","TRACE_USER_2_LBL":"","TRACE_USER_3_LBL":"","TRACE_USER_4_LBL":"","TRACE_USER_5_LBL":"","TRACE_USER_6_LBL":"","TRACE_USER_7_LBL":"","TRACE_USER_8_LBL":"","TRACE_USER_9_LBL":"","TRACE_USER_10_LBL":"","UDF_LAYOUT_ID":"PART","BAL_QTY":0,"PART_REV_NO":"NA","ACTIVE":"Y","UNIT_MATERIAL_COST":0,"PRODUCT_CODE":"XCODE","USER_ID":"MYUSER","CREATE_DATE":"2017-02-06T12:57:28.000Z","LAST_MODIFIED_USER_ID":"","LAST_MODIFIED_DATE":"","SITE_ID":"","UOM_ID":"EA","DIM_TRACKED":"N","LENGTH":"N","WIDTH":"N","HEIGHT":"N","DIM_UOM":"","UNIT_CONSUMABLE_COST":0,"LOCKED":"N","LAST_COUNT_DATE":"","CYCLE_COUNT":0,"ECN_ID":"","SAFETY_STOCK_QTY":0,"UDF_1":"","UDF_2":"","UDF_3":"","UDF_4":"","UDF_5":"","UDF_6":"","UDF_7":"","UDF_8":"","UDF_9":"","UDF_10":""}

```

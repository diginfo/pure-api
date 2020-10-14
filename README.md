<h1>Pure Manufacturing API</h1>

<h2>Introduction</h2>
<p>
API requests in Pure Manufacturing are calls that are made via http POST requests, to the backend HTTP Server.
</p>
<p>
All API requests call functions know as SQLIDs (_sqlid), these are pre-defined functions that translate requests sent via http, into SQL queries, that are performed on the database.
</p>
<p>
SQLIDs may also contain code that performs data validation, and complex calculations on data queried, before being returned to the request, and / or before being saved to the database.
</p>
<p>
For security reasons, direct, raw SQL requests are NOT exposed directly either via http request, or via connections to the database TCP port on the server.
</p>
<p>
API requests are made through secure (https) POST requests using standard JSON notation, and data is returned by default as JSON, and may optionaly be returned as XML using the _format: 'xml' option.
</p>
<p>
Request id's that are prefixed with an underscore '_' are command / option ids, and all other fields not prefixed with an underscore are data field IDs.
</p>

<h2>Requests</h2>

# pure-api
[Web-Based MES production scheduling & WIP tracking software](https://www.puremfg.net)

API POST Request format:
========================
API requests in Pure Manufacturing are calls that are made via http POST requests, to the backend HTTP Server.

All API requests call functions know as SQLIDs (_sqlid), these are pre-defined functions that translate requests sent via http, into SQL queries, that are performed on the database.

SQLIDs may also contain code that performs data validation, and complex calculations on data queried, before being returned to the request, and / or before being saved to the database.

For security reasons, direct, raw SQL requests are NOT exposed directly either via http request, or via connections to the database TCP port on the server.

API requests are made through secure (https) POST requests using standard JSON notation, and data is returned by default as JSON, and may optionaly be returned as XML using the _format: 'xml' option.

Request id's that are prefixed with an underscore '_' are command / option ids, and all other fields not prefixed with an underscore are data field IDs.

Example POST request: 
{
	_userid: 'myuser',
	_passwd: 'mypass',
	_sqlid: 'inv^trace_trans',
	_func: 'get',
	_format: 'xml'
	
	PART_ID: '001-DM-0002-003',
	
}

query id: _userid
description: A unique user ID managed though the system user manager.
example: _userid = 'myuser'

query id: _passwd
description: password for the user
example: _passwd = 'mypass'

query id: _sqlid
description: A pre-defined backend function id that queries the database and / or performs actions on the data requested or sent.
example: inv^trace_trans = module^function-name

query id: _func
description: The action to perform, get a record, add a new record, delete a record, update a record.
example: _func=get, _func=add, _func=del, _func=upd

query id: PART_ID
example: PART_ID=ADBD-12345-000
description: This is the key field used to select the required record. There might be multiple keys.

example response: {"trace":[],"part":[{"ROWID":"","ID":"","DESCRIPTION":"Clamp Body","ALIAS_DESC":"CLAMP","USER_1":"","USER_2":"","USER_3":"","USER_4":"","USER_5":"","USER_6":"","USER_7":"","USER_8":"","USER_9":"","USER_10":"","PART_CLASS_ID":"MAKE_STAGED","TRACEABLE":"N","LOT_SIZE":0,"TRACE_USER_1_LBL":"","TRACE_USER_2_LBL":"","TRACE_USER_3_LBL":"","TRACE_USER_4_LBL":"","TRACE_USER_5_LBL":"","TRACE_USER_6_LBL":"","TRACE_USER_7_LBL":"","TRACE_USER_8_LBL":"","TRACE_USER_9_LBL":"","TRACE_USER_10_LBL":"","UDF_LAYOUT_ID":"","BAL_QTY":"","PART_REV_NO":"NA","ACTIVE":"Y","UNIT_MATERIAL_COST":0,"PRODUCT_CODE":"TURNKEY","USER_ID":"","CREATE_DATE":"","LAST_MODIFIED_USER_ID":"","LAST_MODIFIED_DATE":"","SITE_ID":"","UOM_ID":"EA","DIM_TRACKED":"N","LENGTH":"N","WIDTH":"N","HEIGHT":"N","DIM_UOM":"","UNIT_CONSUMABLE_COST":0,"LOCKED":"N","LAST_COUNT_DATE":"","CYCLE_COUNT":0,"ECN_ID":"","SAFETY_STOCK_QTY":0,"UDF_1":"","UDF_2":"","UDF_3":"","UDF_4":"","UDF_5":"","UDF_6":"","UDF_7":"","UDF_8":"","UDF_9":"","UDF_10":"","DATA_TYPE_1":"","DATA_OPTIONS_1":""}]}


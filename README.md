# Pure Manufacturing API

## Introduction
API requests in Pure Manufacturing are calls that are made via http POST requests, to the backend HTTP Server.

All API requests call functions know as SQLIDs (_sqlid), these are pre-defined functions that translate requests sent via http, into SQL queries, that are performed on the database.

SQLIDs may also contain code that performs data validation, and complex calculations on data queried, before being returned to the request, and / or before being saved to the database.

For security reasons, direct, raw SQL requests are NOT exposed directly either via http request, or via connections to the database TCP port on the server.

API requests are made through secure (https) POST requests using standard JSON notation, and response data is returned by default as JSON, and may optionaly be returned as XML using the _format: 'xml' option.

Request id's that are prefixed with an underscore '_' are command / option ids, and all other fields not prefixed with an underscore are data field IDs.

<h2>API Request Format</h2>
```{
	_userid: 'myuser',
	_passwd: 'mypass',
	_sqlid: 'inv^trace_trans',
	_func: 'get',
	_format: 'xml'
	
	PART_ID: '001-DM-0002-003',
	
}```

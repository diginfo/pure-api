# Pure Manufacturing API

## Introduction
API requests in Pure Manufacturing are calls that are made via https POST requests, to the backend HTTP Server.

For security reasons, raw SQL requests are NOT exposed directly either via http request, or via connections to the database TCP port on the server.

## Request Overview
All API requests primarily call backen functions know as **SQLIDs** (_sqlid), these are unique, pre-defined functions that translate requests sent via http, into SQL queries, that are performed on the database.

SQLIDs may also contain code that performs data validation, and complex calculations on data queried, before being returned to the request, and / or before being saved to the database.

Request id's that are prefixed with an underscore '_' are command / option ids, and all other fields not prefixed with an underscore are data field IDs.

## API Request Example

```javascript
{
	_userid: 'myuser',
	_passwd: 'mypass',
	_sqlid: 'inv^trace_trans',
	_func: 'get',
	_format: 'xml'

	PART_ID: '001-DM-0002-003',

}
```

## API Request Fields

### query id: _passwd
- description: password authentication for the user
- example: _passwd = 'mypass'


## API Response
Response data is returned by default as JSON, but may optionaly be returned as XML using the _format: 'xml' option above.

A response may be either a JSON Object `{}` or a JSON array `[]` Depending upon the type of data requested.

Generally, if a response contains a single record, then it will be returned as an object `{}` and if the response contains multiple records then it is returned as an array `[]`.






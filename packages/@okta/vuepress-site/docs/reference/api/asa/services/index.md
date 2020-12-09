---
title: ASA Services
category: asa
---

# ASA Services API

## Get started

The [Advanced Server Access (ASA) API](/docs/reference/api/asa/introduction/) is logically separate from the rest of the Okta APIs and uses a different API namespace:

`https://app.scaleft.com/v1/`


Advanced Server Access (ASA) Services allow you to authenticate and login to servers using a Service User. This enables you to leverage the security of ephemeral certificates when building automation that requires access to remote servers.

Explore the Services API: [![Run in Postman](https://run.pstmn.io/button.svg)](https://www.getpostman.com/run-collection/fba803e43a4ae53667d4).


## Services API operations


The Services API has the following operations:
* [List Services available for a Server](#list-services-available-for-a-server)
* [Create a Service for a Server](#create-a-service-for-a-server)
* [Delete a Service from a Server](#delete-a-service-from-a-server)
* [List Services for a Team](#list-services-for-a-team)
* [Fetch a Service](#fetch-a-service)
* [Delete a Service](#delete-a-service)


### List Services available for a Server

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/servers/${server_id}/services" />
Lists Services available for a Server

This endpoint requires one of the following roles: `access_user`, `access_admin`, `server_admin`, or `reporting_user`.

#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name |
| `server_id`   | string | The UUID of the Server |
| `team_name`   | string | The name of your Team |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a list of objects with the following fields and a `200` code on a successful call.
| Properties | Type        | Description          |
|----------|-------------|----------------------|
| `id`   | string | The UUID of the Service |
| `server_id`   | string | The UUID of the Server that the Service provides authentication to |
| `server_uid`   | string | The UID of the user on the Server that the Service User uses |
| `service_user_id`   | string | The UUID of the Service User that uses the Service |
| `service_user_name`   | string | The username of the Service User that uses the Service |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/servers/${server_id}/services
```

##### Response

```json
{
	"list": [
		{
			"id": "6414fa11-289f-4aa0-b67e-dcef072af92e",
			"server_id": "5a3af768-063f-4a12-a056-8ef24e555556",
			"server_uid": "9001",
			"service_user_id": "aa225c16-af6e-4ab4-9150-456fd472e2d7",
			"service_user_name": "shreve"
		},
		{
			"id": "99006ae2-db7e-4735-b6bc-c726e6ae81c3",
			"server_id": "5a3af768-063f-4a12-a056-8ef24e555556",
			"server_uid": "9002",
			"service_user_id": "aa225c16-af6e-4ab4-9150-456fd472e2d7",
			"service_user_name": "shreve"
		}
	]
}
```
### Create a Service for a Server

<ApiOperation method="POST" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/servers/${server_id}/services" />
Creates a Service for a Server

This endpoint requires the `access_admin` role.

#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name |
| `server_id`   | string | The UUID of the Server |
| `team_name`   | string | The name of your Team |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint requires an object with the following fields.
| Properties | Type        | Description          |
|----------|-------------|----------------------|
| `server_uid`   | string | The UID of the user on the Server that the Service User uses |
| `service_user_id`   | string | The UUID of the Service User that uses the Service |

#### Response body
This endpoint returns an object with the following fields and a `201` code on a successful call.
| Properties | Type        | Description          |
|----------|-------------|----------------------|
| `id`   | string | The UUID of the Service |
| `server_id`   | string | The UUID of the Server that the Service provides authentication to |
| `server_uid`   | string | The UID of the user on the Server that the Service User uses |
| `service_user_id`   | string | The UUID of the Service User that uses the Service |

#### Usage example

##### Request

```bash
curl -v -X POST \
-H "Authorization: Bearer ${jwt}" \
--data '{
	"server_uid": "9001",
	"service_user_id": "aa225c16-af6e-4ab4-9150-456fd472e2d7"
}' \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/servers/${server_id}/services
```

##### Response

```json
{
	"id": "6414fa11-289f-4aa0-b67e-dcef072af92e",
	"server_id": "5a3af768-063f-4a12-a056-8ef24e555556",
	"server_uid": "9001",
	"service_user_id": "aa225c16-af6e-4ab4-9150-456fd472e2d7"
}
```
### Delete a Service from a Server

<ApiOperation method="DELETE" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/servers/${server_id}/services/${service_id}" />
Deletes a Service from a Server, preventing a Service User to authenticate against the specified Server using the deleted Service

This endpoint requires the `access_admin` role.

#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name |
| `server_id`   | string | The UUID of the Server |
| `service_id`   | string | The UUID of the Service |
| `team_name`   | string | The name of your Team |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a `204 No Content` response on a successful call.


#### Usage example

##### Request

```bash
curl -v -X DELETE \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/servers/${server_id}/services/${service_id}
```

##### Response

```json
HTTP 204 No Content
```
### List Services for a Team

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/services" />
Lists Services available for a Team

This endpoint requires one of the following roles: `access_admin`, `reporting_user`, or `access_user`.

#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `team_name`   | string | The name of your Team |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a list of objects with the following fields and a `200` code on a successful call.
| Properties | Type        | Description          |
|----------|-------------|----------------------|
| `id`   | string | The UUID of the Service |
| `server_id`   | string | The UUID of the Server that the Service provides authentication to |
| `server_uid`   | string | The UID of the user on the Server that the Service User uses |
| `service_user_id`   | string | The UUID of the Service User that uses the Service |
| `service_user_name`   | string | The username of the Service User that uses the Service |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/services
```

##### Response

```json
{
	"list": [
		{
			"id": "6414fa11-289f-4aa0-b67e-dcef072af92e",
			"server_id": "5a3af768-063f-4a12-a056-8ef24e555556",
			"server_uid": "9001",
			"service_user_id": "aa225c16-af6e-4ab4-9150-456fd472e2d7",
			"service_user_name": "shreve"
		},
		{
			"id": "99006ae2-db7e-4735-b6bc-c726e6ae81c3",
			"server_id": "5a3af768-063f-4a12-a056-8ef24e555556",
			"server_uid": "9002",
			"service_user_id": "aa225c16-af6e-4ab4-9150-456fd472e2d7",
			"service_user_name": "shreve"
		}
	]
}
```
### Fetch a Service

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/services/${service_id}" />
Fetches a Service

This endpoint requires one of the following roles: `access_admin`, `reporting_user`, or `access_user`.

#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `service_id`   | string | The UUID of the Service |
| `team_name`   | string | The name of your Team |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns an object with the following fields and a `200` code on a successful call.
| Properties | Type        | Description          |
|----------|-------------|----------------------|
| `id`   | string | The UUID of the Service |
| `server_id`   | string | The UUID of the Server that the Service provides authentication to |
| `server_uid`   | string | The UID of the user on the Server that the Service User uses |
| `service_user_id`   | string | The UUID of the Service User that uses the Service |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/services/${service_id}
```

##### Response

```json
{
	"id": "6414fa11-289f-4aa0-b67e-dcef072af92e",
	"server_id": "5a3af768-063f-4a12-a056-8ef24e555556",
	"server_uid": "9001",
	"service_user_id": "aa225c16-af6e-4ab4-9150-456fd472e2d7"
}
```
### Delete a Service

<ApiOperation method="DELETE" url="https://app.scaleft.com/v1/teams/${team_name}/services/${service_id}" />
Deletes a Service. This endpoint provides the same functionality as [Delete a Service from a Server](#delete-a-service-from-a-server), but without the need to supply Project and Server information

This endpoint requires the `access_admin` role.

#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `service_id`   | string | The UUID of the Service |
| `team_name`   | string | The name of your Team |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a `204 No Content` response on a successful call.


#### Usage example

##### Request

```bash
curl -v -X DELETE \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/services/${service_id}
```

##### Response

```json
HTTP 204 No Content
```



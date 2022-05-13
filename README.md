# **nubceo connect** documentation

![nubceo connect](https://raw.githubusercontent.com/nubceo/nubceo-connect-doc/master/nubceo_connect_logo_1024w.png)

Here you can find technical documentation to use our **nubceo connect** REST API.

## Authentication

The authentication process uses a JWT token that you should request prior to using any of the secured endpoints, by providing your **API Key** and **API Secret**.

### Authentication Flow
  
1. Request the JWT by using the credentials with the `/authenticate` endpoint.  
   Request:
   ```
   POST https://connectapi.nubceo.com/authenticate
   ```
   Request body:
   ```json
   {
     "API_KEY": "xxxxxx",
     "API_SECRET": "xxxxxx"
   }
   ```
2. Get and save the JWT token  
   Keep in mind that the JWT token expires in 1 hour after issuance. You will need to request a new one to continue using the API.
3. Include the JWT token in the `Authentication` HTTP header on each request.
   The HTTP Header to use is `Authentication` with the Bearer token authentication scheme.  
   Example:  
   `Authentication: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6...`

### Errors

These are the possible errores the authentication endpoint can throw:

| HTTP Status Code  | Name  | Description  |
| ------------- | ------------- | ------------- |
| 400  | Invalid request | The request body has invalid or incomplete data. |
| 401  | INVALID_CREDENTIALS | The API Key and/or API Secret is invalid or nonexistent. |

## API reference

Swagger API reference with list of available endpoints:  
https://connectapi.nubceo.com/v1/documentation/static/index.html

### Response structure

All responses from the API share the same base structure:
```jsonc
{
  "status": 200, // status of the response
  "meta": {  // meta data about the content
    "count": 1, // returned items count
    "total": 1  // total items available (useful in case of lists, when the quantity returned is paginated)
  },
  "data": ... // data requested, which could be an object or an array depending on the endpoint
}
```

### Filters

All endpoints that query for a list of objects have the capability to be filtered. The filters should be passed as GET query params in the following format:
```
?filters[fieldName][operator]=value
```
Being:
- `fieldName` the field to filter by
- `operator` one of the supported operators (see below)
- `value` the value to filter by

Current available operators:
- `eq`: 1 == 1
- `ne`: 1 != 1
- `is`: 1 is 1
- `not`: 1 is not 1
- `or`: 1 or 1
- `gt`: 1 > 1
- `gte`: 1 >= 1
- `lt`: 1 < 1
- `lte`: 1 <= 1
- `between`: 1 between [1]
- `notBetween`: 1 not between [1]
- `in`: 1 in (1)
- `notIn`: 1 not in (1)
- `like`: 1 like '%1%'
- `notLike`: 1 not like '%1%'

Examples:
- `?filter[name][like]=%nubceo%`
- `?filters[platformExternalCode][eq]=card_processor
- `?filters[id][in]=[1,2]`

## Requesting access

If you want to get your credentials to use **nubceo connect** contact us at consultas@nubceo.com.

# **nubceo connect** documentation

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

Swagger API reference:  
https://connectapi.nubceo.com/v1/documentation/index.html


## Requesting access

If you want to get your credentials to use **nubceo connect** contact us at consultas@nubceo.com.
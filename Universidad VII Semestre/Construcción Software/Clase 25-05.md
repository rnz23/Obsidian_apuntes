Autenticación básica
* Lo más básico
* Actualmente es lo mas vulnerable y no se usa

Api Key - (SerpApi)
* identifica la aplicación no al usuario
* Larga vida
	Donde usarla:
		Api's solo para leer

Bearer Token
* Tiene mejor estructura y es más seguro, obliga a tener un server de verificación

JWT
* Similar a Bearer Token, pero con mucha mejor estructura

Riesgos
* Tokens almacenados en la base de datos, pueden ser hackeados
* Tiempo de vida larga
* BLAST RADIUS - Si no hay fecha de expiración del token tendré acceso de por vida, se tiene que usar autorización y se debe definir que aplicaciones se puede usar con el acceso.


# OAuth 2.0
Access Token / Refresh Token / id token

Acá se hace uso de Scopes & Consent (Autorización)

### Authorization Code Flow (loggin with google / github)
* Es el que más se usa y más seguro actualmente.


# nginx-reverseproxy-wso2am

## 1.- Lo primero que necesitamos es crear una clave privada en nuestro servidor:

    sudo openssl genrsa -des3 -out server.key 2048

## 2.- Con nuestra clave privada generada, creamos un Certificate Signing Request (CSR) para solicitar nuestro certificado SSL a una entidad de autorización reconocida. Este proceso nos pedirá una serie de datos que son importantes para solicitar el certificado SSL:

Country Name (C): Un código de dos letras para determinar el país, en nuestro caso ponemos US ya que la entidad que lo va a manejar (RapidSSL) es de Estados Unidos. 
State or Province (S): Estado o provincia, este campo puede quedar vacío
Locality or City (L): Localidad o ciudad, tambiÃ©n se puede dejar vacio.
Organization (O): Nombre de la organización que maneja tu certificado SSL, en nuestro caso RapidSSL opera a través de GeoTrust, Inc. y ponemos ese nombre.
Common Name (CN): Nuestro nombre de dominio, tudominio.com. sin las www delante.

    sudo openssl req -new -key server.key -out server.csr

# 3.- Convertir csr a crt:

    openssl x509 -req -in server.csr -signkey server.key -out server.crt
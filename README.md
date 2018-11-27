Custom Password   
===============

Es una libreria para generar contraseñas, agregando obligatoriamente el uso de salt.
Se puede crear mediante el CustomEnconder que se integra dentro de la seguridad de Symfony 3 y 4
o mediante la clase BuildPassword.

## Instalacion

```
composer require antoniosam/custom-password
```

###  Enconder Symfony
Se agrega la clase CustomEnconder como serivicio en el archio services.yml y ese servicio se vincula con la tabla destino usando el encoder del archivo security.yml 

```
(services.yml)
    app.my_custom_encoder:
        class: Ast\CustomPassword\CustomEnconder
  
        
(security.yml)         
    security:
        encoders:
          AppBundle\Entity\User:
              id: app.my_custom_encoder
        

```
### Clase BuildPassword

Si se necesita crear la contraseña y no se puede acceder al encoder la clase BuildPassword puede generar las contraseñas con el mismo resultado que el encoder 
```
$bp = new BuildPassword()
$bp->generate($pass,BuildPassword::randomSalt());
$hashpass = $bp->getPass();
$salt = $bp->getSalt();

BuildPassword::create($pass,$salt)

```

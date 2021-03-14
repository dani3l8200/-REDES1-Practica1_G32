#####  Universidad De San Carlos de Guatemala
##### Facultad de Inegnieria
##### Escuela de Ciencias y sistemas
##### Redes de computadoras 1  
> ##### Grupo 32
> .

> .

> > **Practica No1**\
> > Manual de Contstruccion y Configuracion 

> > > > Integrantes 

| Nombres  | Carnet |
| ------------- |:-------------:|
| Yovany Enrique Samines Orozco	      | 201403689  |
| Esdras Jonatan Noj Larios	      | 201513699     |
| Juan Daniel Enrique Roman Barrientos	      | 201801364    |
| José Luis Herrera Martínez	|  201807431 |
> .

> .

# Manual de construccion y configuracion 
[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)
## Introduccion   
- En la actualidad la conexión de computadores(nodos) es indispensable en la vida cotidiana de la humanidad, es por eso que se han desarrollado e implementado distintas formas para el intercambio de paquetes de datos, viniendo estas desde hace varios años ya. Lo que comenzó con una idea básica ha ido evolucionando hasta convertirse en lo que hoy conocemos como Redes.

- En este manual se explica brevemente la configuración y construcción de ciertas topoligías, encontrandose fotos y algunas descripciones de cada una. Es importante recalcar que para simular un router se utilizó una VPN la cual nos provee servicio por medio de una red privada virtual.

## Construccion de topologia 1
Configuracion de los clientes de cada departamento de los cuales fueron informatica, contabilidad y ventas.
### Se instalaron maquinas virtuales en vmware
  > - visualizacion de las pc instaladas 
 >> ![This is a alt text.](https://i.imgur.com/kdy7evo.png "This is a sample image.").
### Se clonaron maquinas virtuales para los demas clientes
 > - opciones en vmware para clonar las maquinas 
 >> ![](https://i.imgur.com/9hPfGrX.png)
> - Una vez clonada realizamos el mismo procedimiento a los tres clientes
> - Obtenemos lo siguiente 
>> ![](https://i.imgur.com/nJt2DoD.png)
### Configuracion de VMWARE en GNS3
> - Ingresamos en preferencias 
 >> ![](https://i.imgur.com/EuyYezK.png)
> - seleccionamos la opcion new 
 >> ![](https://i.imgur.com/w9HjFHE.png)
> - Agregamos nuestras maquinas a GNS3
>> ![](https://i.imgur.com/FYPuPLh.png)
> #### Una vez agregado podemos visualizar en end devices para poder agregar a nuestro prototipo
>> ![](https://i.imgur.com/2aasE94.png)
> #### esto con la finalidad de que podamos arrancar la maquina desde GNS3 y realiza ping en nuestras virtuales

## Configuracion de los Vlans y los modos de acceso en los switch
> ##### En la imagen que vemos se configuro el vlan que se requeria por los departamentos, switch en GNS3 trae por default vlan1 y el modo de acceso lo dejamos en acces para tener comunicacion con la pc conectado a este switch
>> ![](https://cdn.discordapp.com/attachments/656872654287929386/820170540434194472/unknown.png)
> ##### Ahora veremos lo que es la configuracion de modo troncal entre switch, esto con la finalidad de tener comunicacion por departamentos y no se cruce informacion entre ellos
>> ![](https://cdn.discordapp.com/attachments/656872654287929386/820171313380327424/unknown.png)

## Configuracion de Cloud en GNS3 para coneccion a VPN
> ##### En la imagen podemos ver el puerto que se actualizo de acuerdo a las configuraciones de nuestro servidor en la nube, una vez actualizado estos campos se presiono el boton add para agregar las configuraciones. Estas configuraciones se realizo teniendo desconectado el cable que se conecta con nuestro switch para evitar errores de conexion
>> ![](https://cdn.discordapp.com/attachments/656872654287929386/820174681955893308/unknown.png)
## Topologia Final de los clientes
> ##### La topologia final queda conectado de la siguiente manera con los ip configuradas
>> ![](https://cdn.discordapp.com/attachments/656872654287929386/820482855217004584/unknown.png)
##### El principal objetivo en esta topología es conectar a cada departamento permitiendo así la comunicación entre cada nodo interno más no entre nodos externos. Existe cierta peculiaridad en estas máquinas puesto que las tres máquinas virtuales tienen sistema operativo Windows. La configuración de las IP quedó de la siguiente forma
- ```{r fig.align="center"}
    192.168.32.15 -> Contabilidad 1 
    192.168.32.30 -> Contabilidad 2
    192.168.132.15 -> Informática 1
    192.168.132.30 -> Informática 2
    192.168.232.15 -> Ventas 1
    192.168.232.30 -> Ventas 2 
    ``` 
## Topologia 2 (Servidores)
>> ![](https://cdn.discordapp.com/attachments/656872654287929386/820484649230532668/unknown.png)
##### En esta topología se configuraron los servidores con sistema operativo Linux, esto para un mejor desempeño en seguridad y en eficiencia. En cada servidor existe una página la cual se sirve para las peticiones de cada cliente. Cada servidor tiene una IP en específico, las cuales quedaron de la siguiente forma:
- ```{r fig.align="center"}
    192.168.32.150 -> Contabilidad 
    192.168.132.150 -> Informática
    192.168.232.150 -> Ventas
    ```
## Configuracion VPN 
>> En esto se genero un archivo en azure con extension .rpd con la finalidad de poder hacer conexion de las dos topologias que estuvieran en diferenes maquinas.
>> una vez creado el archivo cargamos este archivo al programa **OpenVpnConect** para luego encender la maquina quedando el siguiente estado de esta forma: 
>> ![](https://cdn.discordapp.com/attachments/656872654287929386/820489518385856522/unknown.png)

>>  teniendo la **VPN** de esa forma podemos tener comunicacion de nuestra maquina fisica al servidor en la nube y con los clientes de **GNS3** teniendo en cuenta que se desactivaran los firewall en cada equipo de los clientes y nuestra maquina fisica
## Conclusion 
- La VPN actua como router debido a la limitante de distancia, la VPN crea una nueva red para todos los dispositivos dentro de ella.
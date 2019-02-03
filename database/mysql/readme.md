# MySql 
###### Fonte [IMASTER](https://imasters.com.br/data/utilizando-docker-com-mysql)

## Comando docker mysql 

    docker run --name mysql -e MYSQL_ROOT_PASSWORD=root -d mysql/mysql-server:latest

## Entrando no Shell do MySql

        docker exec -it {id do container} bash
        
## Ja dentro do container 
        
        mysql -uroot -p

###Vai ser ser solicitado a senha então digite:
    
        root
          
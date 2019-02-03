# MySql 
###### Fonte [rodrigozc/oracle12c](https://hub.docker.com/r/rodrigozc/oracle12c)

## Instalando

    docker pull rodrigozc/oracle12c
    
## Comando docker oracle 

    docker run -p 1521:1521 -v /home/develop/Documentos/docker-images/database/oracle/data:/u01/app/oracle rodrigozc/oracle12c

## Dando acesso e garantias 

        grant connect, all privileges to NOMEDOPROJETO identified by NOMEDOPROJETO
        
## Login e senha 
        
        Login: system
        Senha: oracle


# Autenticação com OpenID Connect e Keycloak

  - [Golang](https://golang.org/)

  - [Docker](https://www.docker.com/)

  - [Keycloak](https://www.keycloak.org/)

  - [OpenID Connect](https://openid.net/connect/)


## Execução

1. Start container com o Keycloak

    $ docker run -p 8080:8080 -e KEYCLOAK_USER=admin -e KEYCLOAK_PASSWORD=admin quay.io/keycloak/keycloak:11.0.1

2. Login no [Administration Console](http://localhost:8080)

    user=admin, password=admin

3. Criar um realm
    
    - Clique "Add realm" no menu suspenso onde diz "Master"

    - Name: local_realm_dev

    - Clique "Create"

    Verificar se está no realm recém criado

4. Criar client

    - Clique "Clients" \ "Create"

    - Preencher os campos

      - Client ID: local_client_dev
      - Client Protocol: openid-connect
      - Root URL: http://localhost:8081

    - Clique "Save"  

    - Aba "Settings"

      - Access Type: confidential
      - Clique "Save"


5. Criar usuário

    - Clique "Users" \ "Add user"

    - Preencher os campos

      - Username: loca_user_dev
      - Email: 
      - First Name: Rafael
      - Last Name: Silva
      - User Enabled (usuário ativo): ON
      - Email Verified (usuário já verificado): ON      

    - Clique "Save"      

    - Clique "Credentials"
      - Preencher "Password"
      - Temporary (se o password é temporário): OFF
      - Clique "Set password"

6. Configurar os campos no arquivo main.go

    clientID: local_client_dev

    clientSecret: "Secret" no Keycloak
    
7. Executar os comandos para subir a aplicação na porta 8081

    $ go mod init goclient

    $ go run goclient/main.go

8. Acessar o navegador http://localhost:8081/    
# Autenticação com OpenID Connect e Keycloak

  - [Golang](https://golang.org/)

  - [Docker](https://www.docker.com/)

  - [Keycloak](https://www.keycloak.org/)

  - [OpenID Connect](https://openid.net/connect/)


## Execução
   
1. Start container com o Keycloak

    ```sh
    $ docker-composer up -d 
    ```

2. Login no [Administration Console](http://localhost:8082)
    ```sh
    $ user=admin 
    $ password=admin
    ```

3. Criar um realm
    
    - Clique **"Add realm"** no menu suspenso onde diz **"Master"**

    - **Name:** dev-realm

    - Clique em  **"Create"**

    Verificar se está no realm recém criado

4. Criar client

    - Clique em **"Clients"** \ **"Create"**

    - Preencher os campos

      - **Client ID:** dev-client
      - **Client Protocol:** openid-connect
      - **Root URL:** http://localhost:8081

    - Clique em  **"Save"**  

    - Aba **"Settings"**

      - **Access Type:** confidential
      - Clique em **"Save"**

5. Criar usuário

    - Clique em **"Users"** \ **"Add user"**

    - Preencher os campos

      - **Username:** dev-user
      - **Email:** 
      - **First Name:** Rafael
      - **Last Name:** Silva
      - **User Enabled (usuário ativo):** ON
      - **Email Verified (usuário já verificado):** ON      

    - Clique em **"Save"**      

    - Clique em **"Credentials"**
      - Preencher o **"Password"**
      - **Temporary (se o password é temporário):** OFF
      - Clique em **"Set password"** e confirme!

6. Configurar os campos no arquivo main.go no Keycloak em Clients **ClientID** e na aba Credentials **Secret**

    - **clientID:** dev-client

    - **clientSecret:** **"Secret"**
    
7. Executar os comandos para subir a aplicação na porta 8082
    ```sh
    $ go mod init goclient

    $ go run goclient/main.go
    ```

8. Acessar o navegador http://localhost:8081/    
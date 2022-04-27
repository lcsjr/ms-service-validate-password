# Iniciando Aplicação

### Componentes

Esta aplicação foi desenvolvida utilizando os componentes listados abaixo:

* [Java OpenJDK 11 - Amazon Corretto (Distribuição gratuita da OpenJDK)](https://docs.aws.amazon.com/corretto/latest/corretto-11-ug/what-is-corretto-11.html)
* [Apache Maven 3.8.2 Documentation](https://maven.apache.org/guides/index.html)
* [Git 2.33.0 Documentation](https://git-scm.com/doc)
* [Spring Boot 2.5.5](https://spring.io/projects/spring-boot)
* [Spring Web](https://docs.spring.io/spring-boot/docs/2.5.5/reference/htmlsingle/#boot-features-developing-web-applications)
* [Swagger - Open API](https://swagger.io/tools/open-source/getting-started/)
* [Jacoco - Code Coverage](https://www.jacoco.org/jacoco/trunk/doc/mission.html)

### Repositório

O repositório deste projeto esta disponível no gitHub e pode ser clonado para sua 
workspace local utilizando a instrução abaixo:

(Certifique-se que o Git esteja instalado)
* Abra seu terminal (Prompt de Comando, PowerShell ou Git Bash)
```
git clone https://github.com/lcsjr/iti-service-validate-password.git
```

### Iniciar a Aplicação

A inicialização da aplicação pode ser executada através de sua IDE de preferência 
ou através da instrução abaixo:

* Abra seu terminal (Prompt de Comando, PowerShell ou Git Bash)
* Acesar a pasta do projeto clonado, conforme:
````
cd c:\<SUA_WORKSPACE>\iti-service-validate-password
````
* Executar a instrução abaixo para o Maven baixar as dependências e criar o build do projeto
````
./mvnw clean package
````
* Executar a instrução abaixo para iniciar o serviço da aplicação
````
./mvnw spring-boot:run
````

### Testes e Análise da Cobertura de Código
Para esta API foi implementada o **Jacoco** como recurso de analise e cobertura de teste do código 

Os testes integrados da aplicação foram escritos utilizando **JUnit**. A idéia de fato foi testar 
a aplicação utilizando o MockMvc para disponibilizar um recurso http para teste do controller.

Para executar os testes, siga os passos abaixo:

* Abra seu terminal (Prompt de Comando, PowerShell ou Git Bash)
* Acesar a pasta do projeto, conforme:
````
cd c:\<SUA_WORKSPACE>\iti-service-validate-password
````
* Executar a instrução abaixo para iniciar os testes
````
./mvnw clean test
````

Após a execução dos testes, o relatório poderá ser conferido em: 
````
C:\<SUA_WORKSPACE>\iti-service-validate-password\target\site\jacoco\index.html
````

Foram realizados 14 testes e a cobertura de código para a classe de negócio é de 100% 
e para a aplicação ficou em 93%.



### Acessando Documentação e Testando o Endpoint

Com o serviço rodando, seguindo os passos anteriores, acesse o link do Swagger através da URL [http://localhost:8081/iti/swagger-ui.html](http://localhost:8081/iti/swagger-ui.html)

A documentação da API para Validação de Senha estará disponível no swagger, conforme acesso da URL acima informado.

Através desta mesma URL será possível testar a API, seguindo os passos:

* validate-controller -> POST /api/v1/valid (clique nesta opção para expandir a tela)
* clique em 'Try it out' (botão ao lado direito)
* No header tem a opção 'password', este campo é de preenchimento obrigatório. 
* Após informar uma senha, clique em 'Execute'.
* Se a senha for válida, você receberá no json a proriedade "valid_password" como 'true', do contrário como 'false'

#### Adicional 

Nesta implementação, foi adicionada a ocorrência por regra que esta ou não válida, 
como por exemplo: Tem caractere especial ? Sim/Não, através da elemento **"has_special_character": true**

Esta opção foi incluída como forma de mostrar ao consumidor desta API qual dos critérios de aceite não foi satisfeito para que uma senha possa ser válida.

```
Response Body

{
  "valid_password": false, 
  "has_length_character": false,
  "has_digit": false,
  "has_letter_upper": false,
  "has_letter_lower": true,
  "has_special_character": false,
  "has_repeated_character": true,
  "has_space_character": false
}
```

### Considerações

Na construção desta API, 
foi utilizado o framework Spring boot para disponibilizar os recusos web rodar facilmente o serviço desta API. 
Recursos da própria linguagem Java, como a API Stream, foram utilizados para facilitar a implementação das regras de validação de uma string assim como também a iteração funcional.


Validação:

* **REQUEST**, o consumidor da API deverá enviar o 'password' no header.

* **RESPONSE**, retornará se o password contém uma string válida para uma senha e quais foram os critérios de aceite utilizados para a validação. 



#  Cadastro de Equipamentos

API desenvolvida em **Spring Boot 3.5** para o **cadastro, consulta,
atualização, exclusão e geração de relatórios Excel** de equipamentos de
TI visando um controle de quando foi entregue e mensurando tempo de uso, a fim de avaliar equipamentos que se desgastam mais rapidamente, substituindo por marcas e modelos de melhor durabilidade em compras futuras reduzindo custos. Utiliza banco de dados **H2**, documentação com **Swagger/OpenAPI**
e exportação de dados com **Apache POI**.

------------------------------------------------------------------------

##  Tecnologias Utilizadas

-   **Java 21**
-   **Spring Boot 3.5**
    -   Spring Web
    -   Spring Data JPA
    -   Spring Validation
-   **H2 Database**
-   **Apache POI** (geração de Excel)
-   **Swagger / Springdoc OpenAPI**
-   **Maven**

------------------------------------------------------------------------

##  Estrutura do Projeto

    src/main/java/io/github/filipecrodrigues/
    ├── controller/        → Endpoints REST
    ├── model/
    │   ├── entity/        → Entidade Equipamento
    │   └── repository/    → Interface JPA
    ├── service/           → Regras de negócio
    └── CadastroEquipamentosApplication.java

------------------------------------------------------------------------

##  Banco de Dados H2

A aplicação utiliza um banco local H2 em arquivo.

**Acesso ao console:** - URL: `/h2-console` - JDBC:
`jdbc:h2:file:./data/equipamentosdb` - Usuário: `sa` - Senha: (vazio)

------------------------------------------------------------------------

##  Endpoints da API

Base URL: `/api/equipamentos`

### 🔹 Criar equipamento

**POST** `/api/equipamentos`

### 🔹 Listar todos

**GET** `/api/equipamentos`

### 🔹 Buscar por número de série

**GET** `/api/equipamentos/{id}`

### 🔹 Atualizar equipamento

**PUT** `/api/equipamentos/{id}`

### 🔹 Excluir equipamento

**DELETE** `/api/equipamentos/{id}`

### 🔹 Exportar Excel

**GET** `/api/equipamentos/excel`

------------------------------------------------------------------------

##  Entidade `Equipamento`

``` java
@Entity
public class Equipamento {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private String numeroDeSerie;

    @Column(nullable = false)
    private String marca;

    @Column(nullable = false)
    private String modelo;

    @JsonFormat(pattern = "dd/MM/yyyy")
    private LocalDate dataDeEntrega;
}
```

------------------------------------------------------------------------

##  Relatório Excel

``` java
public byte[] generateExcel() throws IOException {
    Workbook workbook = new XSSFWorkbook();
    Sheet sheet = workbook.createSheet("Equipamentos");
    return out.toByteArray();
}
```

------------------------------------------------------------------------

##  Como Executar

    git clone https://github.com/seu-repositorio/cadastro-equipamentos.git
    cd cadastro-equipamentos
    mvn spring-boot:run

### Acessar Swagger:

    http://localhost:8080/swagger-ui.html

------------------------------------------------------------------------

##  Build do Projeto

    mvn clean package
    java -jar target/cadastro-equipamentos-0.0.1-SNAPSHOT.jar

------------------------------------------------------------------------

##  Autor

**Filipe C Rodrigues**

# Acesso a Dados com JDBC em Java

Projeto baseado no curso **Programação Orientada a Objetos com Java**, do professor [Dr. Nelio Alves](http://educandoweb.com.br), com foco em acesso a banco de dados utilizando JDBC (Java Database Connectivity).

## 📌 Objetivos

- Aplicar os principais recursos do JDBC na prática
- Criar a estrutura básica de um projeto com JDBC
- Implementar o padrão de projeto DAO manualmente com JDBC

## 🎯 Objetivo Detalhado

Além de aplicar conceitos práticos de acesso a dados com JDBC, este projeto também visa desenvolver boas práticas de organização e versionamento de código utilizando o **Git** e o **GitHub**. A proposta é que o aluno ou desenvolvedor seja capaz de:

- 💡 **Entender o papel do JDBC** na comunicação entre uma aplicação Java e o banco de dados relacional (MySQL).
- 🛠️ **Implementar o padrão DAO (Data Access Object)** manualmente, promovendo uma separação clara entre lógica de negócios e acesso a dados.
- 🗃️ **Organizar a estrutura de pacotes** de forma modular, separando entidades, DAO, e camadas de aplicação.
- 🌐 **Utilizar o GitHub como repositório remoto**, garantindo backup, rastreabilidade e colaboração no código.

### 🧠 Boas Práticas de Uso com Git e GitHub

Durante o desenvolvimento, recomenda-se:

- Criar um repositório Git local com `git init`
- Fazer commits frequentes a cada alteração relevante no código:
  - Exemplo: `git commit -m "Implementa método findById na SellerDaoJDBC"`
- Usar `branches` (ramificações) para implementar novas funcionalidades ou corrigir bugs sem afetar a versão principal (`main` ou `master`)
- Fazer `push` regular para o GitHub: `git push origin main`
- Documentar mudanças no README ou via mensagens de commit claras e objetivas

Esse fluxo garante:

✔️ Histórico detalhado do desenvolvimento  
✔️ Maior controle de versões  
✔️ Facilidade em reverter mudanças indesejadas  
✔️ Profissionalismo e maturidade no desenvolvimento de software

## 🛠️ Tecnologias Utilizadas

- **Java 8+**
- **JDBC API** (`java.sql`, `javax.sql`)
- **MySQL Server**
- **MySQL Workbench**
- **Eclipse IDE**
- **MySQL Connector/J**

## 🗃️ Estrutura do Projeto

- `db/`
  - `DB.java`: métodos auxiliares para conexão e fechamento de recursos
  - `DbException.java`: exceção personalizada para erros de banco
  - `DbIntegrityException.java`: exceção para violação de integridade referencial

- `model/entities/`
  - `Department.java`: classe entidade Departamento
  - `Seller.java`: classe entidade Vendedor

- `model/dao/`
  - `DepartmentDao.java`: interface DAO para Departamento
  - `SellerDao.java`: interface DAO para Vendedor

- `model/dao/impl/`
  - `DepartmentDaoJDBC.java`
  - `SellerDaoJDBC.java`

- `application/`
  - `Program.java`: testes com vendedores
  - `Program2.java`: testes com departamentos

## 📄 Scripts e Dados

Banco de dados `coursejdbc` criado a partir do [script oficial](https://github.com/acenelio/demo-dao-jdbc/blob/master/database.sql)

## ⚙️ Configuração Inicial

1. Crie o banco de dados `coursejdbc` no MySQL
2. Execute o script SQL disponível no link acima para criar e popular as tabelas
3. Baixe o MySQL Connector/J e adicione como `User Library` no Eclipse
4. Crie um arquivo `db.properties` na raiz do projeto com o seguinte conteúdo:

```properties
user=developer
password=1234567
dburl=jdbc:mysql://localhost:3306/coursejdbc
useSSL=false
```

5. Configure a `User Library`:
   - **Eclipse** → Window → Preferences → Java → Build Path → User Libraries
   - Crie uma biblioteca chamada `MySQLConnector` e adicione o `.jar` do driver
   - Adicione a biblioteca ao projeto

## ▶️ Como Executar

1. Certifique-se de que o MySQL Server está ativo
2. No Eclipse, execute as classes a partir do pacote `application`:
   - `Program.java`: realiza testes com a entidade `Seller`
   - `Program2.java`: realiza testes com a entidade `Department`
3. Observe o console para os resultados de inserção, atualização, deleção e listagens

> ⚠️ Certifique-se de atualizar os dados de conexão (`user`, `password`, `dburl`) conforme sua instalação local do MySQL.

## 🧪 Funcionalidades Testadas

- Recuperação de registros com `ResultSet`
- Inserção com `PreparedStatement` e `getGeneratedKeys`
- Atualização e exclusão com tratamento de exceções
- Transações com controle manual (`commit` / `rollback`)
- Implementação do padrão DAO com `DaoFactory`

## 📚 Referências

- [Documentação JDBC - Oracle](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/)
- [Padrão DAO - DevMedia](https://www.devmedia.com.br/dao-pattern-persistencia-de-dados-utilizando-o-padrao-dao/30999)
- [Curso - EducandoWeb](http://educandoweb.com.br)

## 🧩 Explicação das Aplicações Demonstradas

Este projeto é dividido em várias demonstrações práticas, cada uma com foco em uma funcionalidade específica do JDBC e do padrão DAO. Abaixo, estão listadas e explicadas as principais aplicações:

---

### 📥 Recuperar Dados (jdbc2)

Demonstra como conectar-se ao banco de dados e recuperar informações utilizando `Statement` e `ResultSet`.

**Objetivos:**
- Executar uma consulta SQL (SELECT)
- Iterar sobre os resultados
- Entender o funcionamento do cursor (first, next, beforeFirst, etc.)

---

### ➕ Inserir Dados (jdbc3)

Demonstra como inserir novos registros utilizando `PreparedStatement`.

**Objetivos:**
- Utilizar parâmetros de entrada (?)
- Executar `executeUpdate()`
- Obter a chave primária gerada automaticamente com `getGeneratedKeys()`

---

### ✏️ Atualizar Dados (jdbc4)

Exemplo de atualização de registros existentes no banco.

**Objetivos:**
- Usar `PreparedStatement` para UPDATE
- Atualizar os dados de um vendedor já existente
- Identificar o registro pelo ID

---

### ❌ Deletar Dados (jdbc5)

Demonstra a exclusão de dados com tratamento de integridade referencial.

**Objetivos:**
- Implementar exclusão com `DELETE FROM`
- Criar `DbIntegrityException` para capturar erros ao tentar excluir registros referenciados

---

### 🔄 Transações (jdbc6)

Mostra como manipular transações manualmente.

**Objetivos:**
- Controlar commits e rollbacks com `setAutoCommit(false)`
- Garantir atomicidade de múltiplas operações
- Evitar inconsistência de dados em falhas parciais

---

### 🏗️ Implementação do Padrão DAO

Apresenta como aplicar o padrão de projeto DAO na prática.

**Objetivos:**
- Criar interfaces DAO (`SellerDao`, `DepartmentDao`)
- Implementar as interfaces com JDBC (`SellerDaoJDBC`, `DepartmentDaoJDBC`)
- Utilizar `DaoFactory` para instanciar os objetos DAO
- Encapsular o acesso a dados, promovendo independência e testabilidade

---

### 🔍 Consultas Avançadas

**findById**  
Busca um vendedor pelo ID, incluindo o nome do departamento relacionado.

**findByDepartment**  
Lista todos os vendedores de um determinado departamento, ordenados pelo nome.

**findAll**  
Lista todos os vendedores cadastrados no banco de dados, também ordenados por nome.

**insert / update / delete**  
Permitem manipulação completa dos registros de vendedores, com base em parâmetros fornecidos pela aplicação.

---

Cada uma dessas etapas está disponível como demonstração nos repositórios de apoio do curso e pode ser testada diretamente pelos arquivos `Program.java` e `Program2.java`, conforme o módulo.

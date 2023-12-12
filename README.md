  # Consultas MySQL 🐬

Este repositório contém atividades realizadas no MySQL para praticar conceitos de consultas entre os registros de uma banco de dados no MySQL.
https://github.com/luishenriquebk/mysql_consultas/assets/102004702/63bb0005-9548-4850-ac0c-86a33eb4c224

#### Link do projeto: 
https://drive.google.com/drive/folders/13PKKlVuqgOfs1IIky15FT2VTBiOdG_Jw?usp=drive_link

## Atividades Realizadas:

Antes de iniciar as atividades devemos criar o DATABASE ao qual vamos usar nesse projeto introdutório:

```sql
CREATE DATABASE IF NOT EXISTS consultas_avancadas;
USE consultas_avancadas;
```

Agora vamos criar nossas tabelas?

```sql
CREATE TABLE CLIENTE ( -- CRIANDO TABLE CLIENTE;
	id_cliente INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100), 
    idade INT,
    genero VARCHAR(1),
    cidade VARCHAR(45) NOT NULL
);

CREATE TABLE VENDA ( -- CRIANDO TABLE VENDA;
	id_venda INT AUTO_INCREMENT PRIMARY KEY,
    valor DECIMAL(4, 2) NOT NULL,
    forma_pagamento VARCHAR(25),
    data_compra DATE
);
```
Vamos inserir alguns registros em nossas tabelas?

```
INSERT INTO CLIENTE(nome, email, idade, genero, cidade, id_venda) -- INSERINDO VALORES EM CLIENTE;
VALUES 
('Lucas Castro', 'lccastro@gmail.com', 25, 'M', 'Vila Velha', 1),
('Arthur Pacheco', 'pacheco@gmail.com', 24, 'M', 'Vila Velha', 2),
('Alexia', 'alexia@gmail.com', 23, 'F', 'Montes Claros', 3),
('Henrique', 'henrique@gmail.com', 25, 'M', 'Montes Claros', 4),
('Joao', 'joao@gmail.com', 25, 'M', 'Vitorai', 5);

INSERT INTO VENDA(valor, forma_pagamento, data_compra, id_cliente) -- INSERINDO VALORES EM VENDA;
VALUES 
(50.00, 'Debito', '2023-12-07', 3),
(30.00, 'PIX', '2023-12-10', 7),
(45.00, 'Debito', '2023-12-11', 5),
(50.00, 'Debito', '2023-12-12', 5),
(75.00, 'Credito', '2023-12-14', 4);
```
Exibindo os valores das duas TABELAS criadas exibidos:

```
SELECT * FROM CLIENTE;
SELECT * FROM VENDA;

| id_cliente | nome_cliente    | email_cliente         | idade_cliente | genero | cidade_cliente     | id_venda | -- CLIENTE
|------------|-----------------|-----------------------|---------------|--------|--------------------|----------|
| 1          | Lucas Castro    | lccastro@gmail.com    | 25            | M      | Vila Velha         | 1        |
| 2          | Arthur Pacheco  | pacheco@gmail.com     | 24            | M      | Vila Velha         | 2        |
| 3          | Alexia          | alexia@gmail.com      | 23            | F      | Montes Claros      | 3        |
| 4          | Henrique        | henrique@gmail.com    | 25            | M      | Montes Claros      | 4        |
| 5          | Joao            | joao@gmail.com        | 25            | M      | Vitorai            | 5        |

| id_venda | valor_total | forma_pagamento | data_compra | -- VENDA
|----------|-------------|-----------------|-------------|
| 1        | 50.00       | Debito          | 2023-12-07  |
| 2        | 30.00       | PIX             | 2023-12-10  |
| 3        | 45.00       | Debito          | 2023-12-11  |
| 4        | 50.00       | Debito          | 2023-12-12  |
| 5        | 75.00       | Credito         | 2023-12-14  |
```

### 1. UTILIZANDO WHERE PARA FILTRAR COM BASE EM DIFERENTES CONDIÇÕES:

Para realizar a consulta com diferentes condições foi utilizado o seguinte comando e condições:

```sql
SELECT * FROM VENDA
WHERE forma_pagamento = 'Debito' AND valor >= 35;

| id_venda | valor_total | forma_pagamento | data_compra |
|----------|-------------|-----------------|-------------|
| 3        | 45.00       | Debito          | 2023-12-11  |
| 4        | 50.00       | Debito          | 2023-12-12  |

```

### 2. SELECIONANDO DADOS DE MÚLTIPLAS TABELAS USANDO INNER JOIN:

Para selecionar esses registros utilizando foi usado o seguint comando:

```sql
SELECT * FROM CLIENTE
INNER JOIN VENDA ON CLIENTE.id_venda = VENDA.id_venda;

| id_cliente | nome_cliente    | email_cliente         | idade_cliente | genero | cidade_cliente     | id_venda || id_venda | valor_total | forma_pagamento | data_compra | 
|------------|-----------------|-----------------------|---------------|--------|--------------------|----------||----------|-------------|-----------------|-------------|
| 4          | Arthur Pacheco  | pacheco@gmail.com     | 24            | M      | Vila Velha         | 2        || 2        | 30.00       | PIX             | 2023-12-10  |
| 5          | Alexia          | alexia@gmail.com      | 23            | F      | Montes Claros      | 3        || 3        | 45.00       | Debito          | 2023-12-11  |
| 6          | Henrique        | henrique@gmail.com    | 25            | M      | Montes Claros      | 4        || 4        | 50.00       | Debito          | 2023-12-12  |
| 7          | Joao            | joao@gmail.com        | 25            | M      | Vitorai            | 5        || 5        | 75.00       | Credito         | 2023-12-14  |

```

### 3. UTILIZANDO LEFT JOIN PARA RETORNAR TODOS OS REGISTROS DE UMA TABELA, E OS CORRESPONDENTES DA TABELA RELACIONADA:

Para realizar essa conusulta foram realizados os seguintes comandos:


```sql
SELECT * FROM CLIENTE
LEFT JOIN VENDA ON CLIENTE.id_cliente = VENDA.id_cliente;

| id_cliente | nome_cliente    | email_cliente         | idade_cliente | genero | cidade_cliente     | id_venda || id_venda | valor_total | forma_pagamento | data_compra | 
|------------|-----------------|-----------------------|---------------|--------|--------------------|----------||----------|-------------|-----------------|-------------|
| 4          | Arthur Pacheco  | pacheco@gmail.com     | 24            | M      | Vila Velha         | 2        || 2        | 30.00       | PIX             | 2023-12-10  |
| 5          | Alexia          | alexia@gmail.com      | 23            | F      | Montes Claros      | 3        || 3        | 45.00       | Debito          | 2023-12-11  |
| 6          | Henrique        | henrique@gmail.com    | 25            | M      | Montes Claros      | 4        || 4        | 50.00       | Debito          | 2023-12-12  |
| 7          | Joao            | joao@gmail.com        | 25            | M      | Vitorai            | 5        || 5        | 75.00       | Credito         | 2023-12-14  |
```

### 4. UTILIZANDO FUNÇÕES DE AGREGAÇÃO:

Para realizar esse tipo de consulta foi executado o seguinte comando:

```sql
SELECT COUNT(*) AS TOTAL_CLIENTES FROM CLIENTE;
SELECT SUM(VALOR) AS TOTAL_RECEITA FROM VENDA;
SELECT ROUND(AVG(IDADE), 2) AS IDADE_MEDIA FROM CLIENTE;
SELECT MIN(VALOR) AS VALOR_MININO FROM VENDA;
SELECT MAX(VALOR) AS VALOR_MAXIMO FROM VENDA;

| TOTAL_CLIENTES | TOTAL_RECEITA  | IDADE_MEDIA | VALOR_MININO | VALOR_MAXIMO |
|----------------|--------------- |-------------|--------------|--------------|
| 4              | 250.00         | 24.25       | 30.00        | 75.00        |
```

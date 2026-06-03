# Banco de Dados - Locadora de Carros 🚗

Este repositório contém a modelagem, a estrutura de tabelas e os dados iniciais de um banco de dados desenvolvido em **MySQL** para o gerenciamento de clientes, marcas e inventário de uma locadora de veículos.

---

## 🛠️ Tecnologias Utilizadas
* **SGBD:** MySQL (Versão 8.0)
* **Ferramenta de Modelagem:** MySQL Workbench
* **Linguagem:** SQL (DDL / DML)

---

## 📊 Estrutura do Banco de Dados

O banco de dados é composto por três tabelas principais interligadas:

* **`marcas`**: Armazena o cadastro das fabricantes, contendo o nome da marca e seu país de origem.
* **`inventario`**: Controla a frota de veículos disponíveis, registrando o modelo, tipo de transmissão (câmbio), motorização, combustível e o vínculo com sua respectiva marca.
* **`clientes`**: Registra as informações dos locatários, armazenando nome, sobrenome e endereço.

### 🔗 Relacionamentos
* A tabela `inventario` possui uma chave estrangeira (**FK**) chamada `marcas_id` que faz referência ao ID da tabela `marcas`, garantindo a integridade referencial dos dados.

---

## 🔍 Exemplos Práticos de Consultas (Queries)

Para demonstrar a usabilidade do banco em cenários reais, abaixo estão alguns exemplos de consultas que utilizam conceitos fundamentais do SQL:

### 1. Relatório Completo de Veículos e Fabricantes (INNER JOIN)
Esta consulta unifica os dados do inventário com as informações da tabela de marcas, exibindo de forma clara quais carros pertencem a quais fabricantes e suas respectivas origens:

```sql
SELECT 
    i.modelo AS 'Modelo do Veículo',
    i.motor AS 'Motor',
    i.transmissao AS 'Câmbio',
    i.combustivel AS 'Combustível',
    m.nome_marca AS 'Marca',
    m.origem AS 'Origem da Fabricante'
FROM inventario i
INNER JOIN marcas m ON i.marcas_id = m.id;

SELECT 
    combustivel AS 'Tipo de Combustível',
    COUNT(*) AS 'Quantidade em Estoque'
FROM inventario
GROUP BY combustivel
ORDER BY COUNT(*) DESC;

SELECT 
    id AS 'Código',
    CONCAT(nome, ' ', sobrenome) AS 'Nome Completo',
    endereco AS 'Endereço Residencial'
FROM clientes
ORDER BY nome ASC;

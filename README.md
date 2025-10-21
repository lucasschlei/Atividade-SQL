# Atividade SQL — Exercícios e Dataset de Exemplo

Bem-vindo! Este repositório reúne um conjunto de tabelas, dados de exemplo e 25 exercícios práticos para treinar consultas SQL (JOINs, agregações, tratamento de dados faltantes e clausulas condicionais). O material foi pensado para ser didático, reutilizável em aulas e apresentável ao público.

Principais objetivos:
- Entender e praticar diferentes tipos de JOINs (INNER, LEFT, RIGHT).
- Trabalhar com agregações (COUNT, GROUP BY).
- Lidar com dados incompletos ou inconsistentes (NULLs, chaves ausentes).
- Montar consultas completas que integrem clientes, pedidos, pagamentos, entregas, produtos, setores e funcionários.

---

## Conteúdo deste repositório
- DDL (CREATE TABLE) com a modelagem relacional.
- Inserts com dados de exemplo para testar os exercícios.
- Conjunto de 25 consultas (cada uma resolvendo um dos exercícios solicitados).
- Instruções rápidas para rodar em MySQL ou PostgreSQL.

---

## Modelo de dados (visão resumida)
Tabelas principais:
- clientes (id, nome)
- produtos (id, nome, preco)
- pedidos (id, cliente_id, produto_id, data_pedido)
- pagamentos (id, pedido_id, forma_pagamento, data_pagamento)
- transportadoras (id, nome)
- entregas (id, pedido_id, transportadora_id, status)
- setores (id, nome_setor)
- funcionarios (id, nome, setor_id)

Exemplo de DDL (use este bloco para criar as tabelas):
```sql
CREATE TABLE clientes (
  id INT PRIMARY KEY,
  nome VARCHAR(50)
);

CREATE TABLE produtos (
  id INT PRIMARY KEY,
  nome VARCHAR(50),
  preco DECIMAL(10,2)
);

CREATE TABLE pedidos (
  id INT PRIMARY KEY,
  cliente_id INT,
  produto_id INT,
  data_pedido DATE,
  FOREIGN KEY (cliente_id) REFERENCES clientes(id),
  FOREIGN KEY (produto_id) REFERENCES produtos(id)
);

CREATE TABLE pagamentos (
  id INT PRIMARY KEY,
  pedido_id INT,
  forma_pagamento VARCHAR(30),
  data_pagamento DATE,
  FOREIGN KEY (pedido_id) REFERENCES pedidos(id)
);

CREATE TABLE transportadoras (
  id INT PRIMARY KEY,
  nome VARCHAR(50)
);

CREATE TABLE entregas (
  id INT PRIMARY KEY,
  pedido_id INT,
  transportadora_id INT,
  status VARCHAR(20),
  FOREIGN KEY (pedido_id) REFERENCES pedidos(id),
  FOREIGN KEY (transportadora_id) REFERENCES transportadoras(id)
);

CREATE TABLE setores (
  id INT PRIMARY KEY,
  nome_setor VARCHAR(50)
);

CREATE TABLE funcionarios (
  id INT PRIMARY KEY,
  nome VARCHAR(50),
  setor_id INT,
  FOREIGN KEY (setor_id) REFERENCES setores(id)
);
```

Dados de exemplo (inserts):
```sql
-- Clientes
INSERT INTO clientes VALUES
(1, 'Ana'),
(2, 'Bruno'),
(3, 'Carlos'),
(4, 'Daniela'),
(5, 'Eduardo');

-- Produtos
INSERT INTO produtos VALUES
(1, 'Celular', 1500.00),
(2, 'Notebook', 3000.00),
(3, 'Teclado', 200.00),
(4, 'Mouse', 100.00),
(5, 'Monitor', 900.00);

-- Pedidos
INSERT INTO pedidos VALUES
(1, 1, 1, '2025-01-10'),
(2, 2, 2, '2025-02-15'),
(3, 2, 3, '2025-03-01'),
(4, 4, 5, '2025-04-22'),
(5, 5, 4, '2025-04-25');

-- Pagamentos
INSERT INTO pagamentos VALUES
(1, 1, 'Cartão', '2025-01-11'),
(2, 2, 'Pix', '2025-02-16'),
(3, 4, 'Boleto', '2025-04-23');

-- Transportadoras
INSERT INTO transportadoras VALUES
(1, 'TransSpeed'),
(2, 'LogMais'),
(3, 'Rápido Sul');

-- Entregas
INSERT INTO entregas VALUES
(1, 1, 1, 'Entregue'),
(2, 2, 2, 'A caminho'),
(3, 3, 3, 'Cancelada'),
(4, 5, 1, 'Erro');

-- Setores
INSERT INTO setores VALUES
(1, 'TI'),
(2, 'RH'),
(3, 'Financeiro'),
(4, 'Marketing');

-- Funcionários
INSERT INTO funcionarios VALUES
(1, 'Felipe', 1),
(2, 'Gabriela', 2),
(3, 'Henrique', NULL);


---

## Licença & Contato
Uso livre para fins educacionais. Para dúvidas ou melhorias, abra uma issue ou entre em contato: lucasschlei (GitHub).

Obrigado por usar este material — bom estudo!

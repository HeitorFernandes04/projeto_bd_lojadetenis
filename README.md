# projeto_bd_lojadetenis

# Sistema de Loja de Tênis Online – CRUD com SQLite

Este repositório contém o projeto de banco de dados e a aplicação CRUD de uma **loja de tênis online**, desenvolvido como trabalho prático da disciplina de Banco de Dados.

O foco do projeto é aplicar, na prática, as principais etapas de projeto de banco de dados: levantamento de requisitos, modelagem conceitual, modelo relacional, normalização, implementação física em **SQLite** e desenvolvimento de uma aplicação CRUD com interface (web) utilizando **Django**.

---

## 1. Descrição Geral do Sistema (Minimundo)

A aplicação representa uma **loja virtual de tênis**, onde:

- A loja vende apenas **online**.
- São cadastrados **tênis** com:
  - modelo, marca, cor, tamanho, preço de venda e quantidade em estoque.
- Cada tênis pertence a **uma marca**, e uma marca pode ter vários modelos de tênis.
- A loja mantém cadastro de **clientes**, armazenando dados pessoais para emissão de vendas.
- As **vendas** são realizadas diretamente pelo sistema, sem vendedor vinculado:
  - cada venda possui cliente, data, valor total, forma de pagamento e status.
- Cada venda possui **itens de venda**, relacionando os tênis vendidos, suas quantidades e preços no momento da compra.
- Ao registrar uma venda, o sistema deve **dar baixa no estoque** dos produtos vendidos.

---

## 2. Objetivos do Trabalho

- Aplicar o processo completo de **projeto de banco de dados**:
  - Levantamento e análise de requisitos
  - Análise funcional
  - Projeto conceitual (MER)
  - Projeto lógico (modelo relacional)
  - Normalização
  - Projeto físico (SQLite)
  - Implementação da aplicação CRUD
- Utilizar **SQLite** como SGBD.
- Desenvolver uma aplicação CRUD funcional em **Django**.
- Entregar um sistema organizado, documentado e coerente com o checklist da disciplina.

---

## 3. Requisitos Funcionais Implementados

A aplicação deve permitir:

### 3.1. Clientes
- Cadastrar cliente
- Listar clientes
- Editar dados do cliente
- Excluir cliente
- Consultar cliente por nome ou CPF

### 3.2. Marcas
- Cadastrar marca
- Listar marcas
- Editar marca
- Excluir marca  
  > (Ideal: bloquear exclusão se houver tênis associados)

### 3.3. Tênis (Produtos)
- Cadastrar tênis (modelo, marca, cor, tamanho, preço, estoque)
- Listar tênis
- Editar dados do tênis
- Excluir tênis
- Consultar por:
  - modelo
  - marca
  - tamanho
  - faixa de preço
- Visualizar tênis com **estoque baixo**

### 3.4. Vendas
- Registrar venda (cabeçalho + itens)
- Listar vendas realizadas
- Visualizar detalhes de uma venda (itens, quantidades, valores)
- Consultar vendas por:
  - cliente
  - período (intervalo de datas)
- (Opcional) Cancelar venda e estornar estoque

---

## 4. Modelagem de Dados

A modelagem foi feita em etapas, seguindo o checklist do trabalho:

### 4.1. Diagrama Entidade–Relacionamento (MER)
Entidades principais:

- **CLIENTE**
- **MARCA**
- **TENIS**
- **VENDA**
- **ITEM_VENDA** (tabela associativa VENDA × TENIS)

Relacionamentos principais:

- MARCA 1 — N TENIS  
- CLIENTE 1 — N VENDA  
- VENDA N — N TENIS (via ITEM_VENDA)

> O MER completo está documentado no arquivo correspondente na pasta `docs/` (por exemplo, `docs/mer_loja_tenis.pdf`).

### 4.2. Modelo Relacional

Tabelas principais:

- `CLIENTE(id_cliente, nome, cpf, telefone, email, data_cadastro)`
- `MARCA(id_marca, nome)`
- `TENIS(id_tenis, modelo, cor, tamanho, preco_venda, qtd_estoque, codigo_barra, id_marca)`
- `VENDA(id_venda, data_venda, valor_total, forma_pagamento, status, id_cliente)`
- `ITEM_VENDA(id_venda, id_tenis, quantidade, preco_unitario, subtotal)`

Com chaves primárias, estrangeiras e restrições adequadamente definidas.

### 4.3. Normalização

As tabelas foram organizadas de forma a evitar:

- redundância de dados
- anomalias de inserção, atualização e exclusão

O modelo foi normalizado até **3FN**, o que é suficiente para o contexto do projeto. A justificativa da normalização está descrita no documento de projeto na pasta `docs/`.

---

## 5. Tecnologias Utilizadas

- **Linguagem:** Python 3.x  
- **Framework Web:** Django  
- **Banco de Dados:** SQLite3  
- **Interface:** HTML / CSS (e, opcionalmente, Bootstrap ou similar)  

---

## 6. Estrutura do Projeto (Sugestão)

```text
.
├── docs/
│   ├── 01_requisitos_minimundo.pdf
│   ├── 02_analise_funcional.pdf
│   ├── 03_mer_loja_tenis.pdf
│   ├── 04_modelo_relacional.pdf
│   ├── 05_normalizacao.pdf
│   └── 06_script_sql_sqlite.sql
├── loja_tenis/              # pasta do projeto Django
│   ├── manage.py
│   ├── loja_tenis/          # config do projeto
│   └── core/                # app principal (models, views, templates)
├── db.sqlite3               # banco de dados SQLite
├── requirements.txt
└── README.md


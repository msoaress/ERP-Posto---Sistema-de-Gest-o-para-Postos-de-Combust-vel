# ⛽ ERP Posto - Sistema de Gestão para Postos de Combustível

O **ERP Posto** é uma aplicação em Python via linha de comando (CLI) integrada a um banco de dados **MySQL**, desenvolvida para o gerenciamento de estoque, vendas, custos e lucratividade de postos de combustível.

---

## 🛠️ Tecnologias Utilizadas

* **Linguagem:** Python 3.x
* **Banco de Dados:** MySQL
* **Biblioteca Principal:** `mysql-connector-python`
* **Modelagem:** brModelo (Conceitual e Lógico)

---

## 📁 Estrutura do Projeto

```text
.
├── app_posto.py               # Código principal da aplicação (CRUD + Autenticação CLI)
├── app_posto.spec             # Arquivo de configuração do PyInstaller para build
├── database_ERP_POSTO.sql     # Script DDL e DML para criação e carga inicial do banco MySQL
├── Conceptual_model.pdf       # Diagrama de Modelagem Conceitual do banco de dados
└── Logic_model.pdf            # Diagrama de Modelagem Lógica do banco de dados
```

---

## 🗄️ Estrutura do Banco de Dados (`ERP_POSTO`)

O sistema trabalha com 5 tabelas principais interligadas:

1. **`LOGIN`**: Autenticação dos usuários do sistema.
   * `ID` (PK), `CNPJ`, `SENHA_APP`
2. **`ESTOQUE_SAÍDA`**: Controle das saídas de combustíveis por bomba.
   * `ID` (PK), `CÓD_BOMBA`, `DIESEL`
3. **`VENDAS`**: Registro de vendas detalhadas por tipo de combustível.
   * `ID` (PK), `BOMBAS_POSTO`, `DATA_HORAS`, `CÓD_BOMBA`, `DIESEL`, `ÁLCOOL`, `GASOLINA`, `GNV`
4. **`CUSTOS`**: Gestão de custos com funcionários, produtos e operação.
   * `ID` (PK), `FUNCIONÁRIOS`, `PRODUTOS`, `CÓD_BOMBA`, `ALCOOL`
5. **`LUCRO_MENSAL`**: Fechamento mensal de lucros e custos agregados.
   * `ID` (PK), `DATA_MÊS`, `LUCRO_REAL`, `CUSTOS`, `CÓD_BOMBA`

---

## 🚀 Como Executar o Projeto

### 1. Pré-requisitos
* Python 3.x instalado.
* Servidor MySQL em execução local (`127.0.0.1`).

### 2. Configurar o Banco de Dados
Execute o script SQL no seu cliente MySQL (MySQL Workbench, phpMyAdmin ou via CLI):

```bash
mysql -u root -p < database_ERP_POSTO.sql
```

### 3. Instalar Dependências
Instale o conector MySQL para Python:

```bash
pip install mysql-connector-python
```

### 4. Executar a Aplicação
No terminal, navegue até a pasta do projeto e execute:

```bash
python app_posto.py
```

---

## 💻 Funcionalidades do Sistema

* **Autenticação de Usuários:** Validação de login por CNPJ e senha cadastrada na tabela `LOGIN`.
* **Operações CRUD Completa:**
  1. **Ler dados:** Consulta registros cadastrados em qualquer uma das 5 tabelas.
  2. **Alterar dados:** Atualização de registros específicos via parâmetro `ID`.
  3. **Inserir dados:** Cadastro interativo via CLI.
  4. **Deletar dados:** Remoção de registros pelo `ID`.
* **Alertas Sonoros:** Notificações de áudio do sistema (`winsound`) durante a autenticação e finalização.

---

## 📦 Gerar Executável (`.exe`)

Para compilar o script Python em um arquivo executável standalone utilizando o arquivo `.spec` fornecido:

```bash
pip install pyinstaller
pyinstaller app_posto.spec
```
O executável compilado estará disponível na pasta `dist/app_posto/`.
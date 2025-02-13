# Tutorial prático sobre SQLite no Debian 12

## 1. Instalando o SQLite
SQLite já vem incluído na maioria das distribuições Linux, mas caso precise instalá-lo, use o seguinte comando:

```sh
sudo apt update && sudo apt install sqlite3
```

Para verificar se a instalação foi concluída com sucesso, execute:

```sh
sqlite3 --version
```

---

## 2. Criando um Banco de Dados
Para criar um novo banco de dados SQLite, abra o terminal e execute:

```sh
sqlite3 meu_banco.db
```
Isso criará um arquivo chamado `meu_banco.db` e abrirá o prompt interativo do SQLite.

---

## 3. Criando uma Tabela
Dentro do prompt do SQLite, use a seguinte sintaxe para criar uma tabela:

```sql
CREATE TABLE clientes (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    email TEXT UNIQUE,
    idade INTEGER,
    cidade TEXT
);
```

---

## 4. Inserindo Dados na Tabela

```sql
INSERT INTO clientes (nome, email, idade, cidade) VALUES ('João Silva', 'joao@email.com', 30, 'São Paulo');
INSERT INTO clientes (nome, email, idade, cidade) VALUES ('Maria Souza', 'maria@email.com', 25, 'Rio de Janeiro');
```

---

## 5. Consultando Dados
Para visualizar todos os registros da tabela:

```sql
SELECT * FROM clientes;
```

Para filtrar os resultados:

```sql
SELECT * FROM clientes WHERE cidade = 'São Paulo';
```

---

## 6. Alterando Campos
Para adicionar uma nova coluna:

```sql
ALTER TABLE clientes ADD COLUMN telefone TEXT;
```

Para modificar um dado existente:

```sql
UPDATE clientes SET telefone = '11987654321' WHERE nome = 'João Silva';
```

---

## 7. Excluindo Campos
SQLite não permite remover colunas diretamente. A solução é criar uma nova tabela sem a coluna desejada, copiar os dados e renomear a tabela:

```sql
CREATE TABLE clientes_novo (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    email TEXT UNIQUE,
    idade INTEGER
);

INSERT INTO clientes_novo (id, nome, email, idade) SELECT id, nome, email, idade FROM clientes;
DROP TABLE clientes;
ALTER TABLE clientes_novo RENAME TO clientes;
```

---

## 8. Excluindo Tabelas
Para excluir uma tabela:

```sql
DROP TABLE clientes;
```

---

## 9. Criando Índices
Para melhorar a performance das consultas, crie um índice:

```sql
CREATE INDEX idx_clientes_email ON clientes (email);
```

---

## 10. Consultas Comuns
### Selecionar apenas alguns campos:
```sql
SELECT nome, email FROM clientes;
```

### Contar registros:
```sql
SELECT COUNT(*) FROM clientes;
```

### Ordenar resultados:
```sql
SELECT * FROM clientes ORDER BY idade DESC;
```

### Limitar resultados:
```sql
SELECT * FROM clientes LIMIT 5;
```

---

## 11. Exportando e Importando Dados
### Exportando para CSV:
```sql
.mode csv
.output clientes.csv
SELECT * FROM clientes;
.output stdout
```

### Importando CSV:
```sql
.mode csv
.import clientes.csv clientes
```

---

## 12. Saindo do SQLite
Para sair do prompt do SQLite, digite:

```sql
.exit
```

Agora você tem um conhecimento sólido para trabalhar com SQLite no Debian 12!



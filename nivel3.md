# Nível 3 – Recursos Humanos

## 3.1 Funcionários com cônjuge
Query:
```js
db.funcionarios.countDocuments({ "dependentes.conjuge": { $exists: true } })
```
Resultado: 7 funcionários.

## 3.2 Funcionários com filhos
Query:
```js
db.funcionarios.countDocuments({ "dependentes.filhos": { $exists: true } })
```
Resultado: 7 funcionários.

## 3.3 Funcionário com mais tempo na empresa
Query:
```js
db.funcionarios.find().sort({ dataAdmissao: 1 }).limit(1)
```
Resultado: Irene Adler (1980-09-28).

## 3.4 Funcionário com menos tempo na empresa
Query:
```js
db.funcionarios.find().sort({ dataAdmissao: -1 }).limit(1)
```
Resultado: Vitória Silva (2025-01-01).

## 3.5 Top 5 funcionários mais antigos
Query:
```js
db.funcionarios.find().sort({ dataAdmissao: 1 }).limit(5)
```
Resultado:
1. Irene Adler (1980)
2. Jennifer Whalen (1987)
3. Den Raphaely (1994)
4. Payam Kaufling (1995)
5. Normam Osborn (1995)

## 3.6 Contratados de 1990 a 1999
Query:
```js
db.funcionarios.countDocuments({
  dataAdmissao: { $gte: "1990-01-01", $lte: "1999-12-31" }
})
```
Resultado: 8 funcionários.

## 3.7 Evolução da média salarial por ano
Query:
```js
db.funcionarios.aggregate([
  { $addFields: { ano: { $substr: ["$dataAdmissao", 0, 4] } } },
  { $group: { _id: "$ano", media: { $avg: "$salario" } } },
  { $sort: { _id: 1 } }
])
```
Resultado: Média salarial por ano exibida.

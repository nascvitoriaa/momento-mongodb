# Nível 8 – Otimização e Desafios

## 8.1 Vendas com dependentes
Várias formas, exemplo:
```js
db.funcionarios.find({
  departamento:ObjectId("85992103f9b3e0b3b3c1fe71"),
  $or:[ { "dependentes.conjuge":{$exists:true} }, { "dependentes.filhos":{$exists:true} } ]
})
```

## 8.2 Funcionários com escritório diferente do departamento
```js
db.funcionarios.aggregate([
  { $lookup:{ from:"departamentos", localField:"departamento", foreignField:"_id", as:"dep" }},
  { $unwind:"$dep" },
  { $match:{ $expr:{ $ne:["$escritorio","$dep.escritorio"] }} }
])
```

## 8.3 Relatório por escritório
Campos como nome, funcionários, custo etc com aggregations e lookup.

## 8.4 Departamento mais equilibrado (menor diferença salarial)
```js
db.funcionarios.aggregate([
  { $group:{ _id:"$departamento", diff:{ $subtract:[ { $max:"$salario" }, { $min:"$salario" } ] } }},
  { $sort:{ diff:1 } }
])
```

## 8.5 Busca por "Uniforme"
```js
db.vendas.find({ produto:/Uniforme/ })
```

## 8.6 Vendas no 2º trimestre de 2023
```js
db.vendas.find({
  dataVenda:{ $gte:"2023-04-01", $lte:"2023-06-30" }
})
```

# Nível 9 – Ninja

## 9.1 Salários entre 6000 e 10000 (3 jeitos)
```js
db.funcionarios.find({ salario:{ $gte:6000, $lte:10000 } })
db.funcionarios.find({ salario:{ $between:[6000,10000] } }) // pseudo
db.funcionarios.find({ $and:[ {salario:{$gte:6000}}, {salario:{$lte:10000}} ] })
```

## 9.2 Query mais eficiente
A correta é com filtro direto no find, não filtrando depois em memória.

## 9.3 Funcionários sem email ou telefone
```js
db.funcionarios.find({
  $or:[ {email:{$exists:false}}, {telefone:{$exists:false}} ]
})
```

## 9.4 Funcionários únicos no cargo por departamento
Aggregation com group e match size = 1.

## 9.5 Relatório por país
lookup + group somando escritórios, funcionários e custos.

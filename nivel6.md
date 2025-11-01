# Nível 6 – Operações de Atualização

## 6.1 Criar departamento Inovações
Query:
```js
db.departamentos.insertOne({
  nome: "Inovações",
  escritorio: ObjectId("5f8b3f3f9b3e0b3b3c1e3e3e")
})
```

## 6.2 Transferir 2 funcionários de Tecnologia para Inovações
Query (exemplo com 2 IDs):
```js
db.funcionarios.updateMany(
  { departamento: ObjectId("85992103f9b3e0b3b3c1fe74") },
  { $set: { departamento: ObjectId("NOVO_ID_INOVACOES") } },
  { limit: 2 }
)
```

## 6.3 Aumento de 10% para Tecnologia
```js
db.funcionarios.updateMany(
  { departamento: ObjectId("85992103f9b3e0b3b3c1fe74") },
  [ { $set: { salario: { $multiply: ["$salario", 1.10] } } } ]
)
```

## 6.4 Atualizar Bruce Ernst
```js
db.funcionarios.updateOne(
  { nome: "Bruce Ernst" },
  { $set: { cargo: "Senior Web Developer", salario: 5000 } }
)
```

## 6.5 Adicionar Headsets ao Wayne Offices
```js
db.escritorios.updateOne(
  { nome: "Wayne Offices" },
  { $push: { suprimentos: { produto:"Headsets", quantidade:15, precoUnitario:150 } } }
)
```

## 6.6 Remover funcionários contratados antes de 1990
Primeiro visualizar:
```js
db.funcionarios.find({ dataAdmissao:{ $lt:"1990-01-01" } })
```

Depois apagar:
```js
db.funcionarios.deleteMany({ dataAdmissao:{ $lt:"1990-01-01" } })
```

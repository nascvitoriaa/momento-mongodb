# Relatório Momento – Nível 2
## Análise Financeira Básica

### 2.1 Funcionários no Departamento de Vendas
**Descrição:** Quantidade de colaboradores no departamento de Vendas.

**Query:**
```js
db.funcionarios.countDocuments({
  departamento: ObjectId("85992103f9b3e0b3b3c1fe71")
})
```

**Resultado:** 9 funcionários.

---

### 2.2 Custo Total com Salários do Departamento de Vendas
**Descrição:** Soma dos salários de todos os funcionários do departamento de Vendas.

**Query:**
```js
db.funcionarios.aggregate([
  { $match: { departamento: ObjectId("85992103f9b3e0b3b3c1fe71") } },
  { $group: { _id: null, totalSalarios: { $sum: "$salario" } } }
])
```

**Resultado:** $67.200

---

### 2.3 Média Salarial da Empresa (excluindo CEO, CMO, CFO)
**Descrição:** Média salarial excluindo cargos executivos.

**Query:**
```js
db.funcionarios.aggregate([
  { $match: { cargo: { $nin: ["CEO", "CMO", "CFO"] } } },
  { $group: { _id: null, mediaSalarial: { $avg: "$salario" } } }
])
```

**Resultado:** $10.382,35

---

### 2.4 Média Salarial do Departamento de Tecnologia
**Descrição:** Cálculo da média salarial apenas para funcionários do departamento de Tecnologia.

**Query:**
```js
db.funcionarios.aggregate([
  { $match: { departamento: ObjectId("85992103f9b3e0b3b3c1fe74") } },
  { $group: { _id: null, mediaTecnologia: { $avg: "$salario" } } }
])
```

**Resultado:** $4.766,66

---

### 2.5 Departamento com Maior Média Salarial
**Descrição:** Identificar qual departamento possui maior média salarial.

**Query:**
```js
db.funcionarios.aggregate([
  { $lookup: { from: "departamentos", localField: "departamento", foreignField: "_id", as: "dep" } },
  { $unwind: "$dep" },
  { $group: { _id: "$dep.nome", mediaSalario: { $avg: "$salario" } } },
  { $sort: { mediaSalario: -1 } }
])
```

**Resultado:** Departamento Executivo.

---

### 2.6 Departamento com Menor Número de Funcionários
**Descrição:** Encontrar o departamento com menos colaboradores.

**Query:**
```js
db.funcionarios.aggregate([
  { $group: { _id: "$departamento", totalFuncionarios: { $count: {} } } },
  { $sort: { totalFuncionarios: 1 } }
])
```

**Resultado:** Departamento de Marketing.

---

## Conclusão Geral
Esta etapa forneceu uma visão clara dos custos de pessoal e estrutura salarial da Momento. Identificamos o peso do departamento de Vendas, a forte média salarial da liderança executiva e insights para potenciais análises de eficiência e alocação futura.


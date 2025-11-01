# Nível 10 – Casos Reais

## 10.1 Criar escritório no Brasil
```js
db.escritorios.insertOne({
  nome:"Momento Brasil",
  pais:"Brasil",
  suprimentos:[{produto:"Café",quantidade:30,precoUnitario:15}]
})
```

## 10.2 Novo departamento LATAM
```js
db.departamentos.insertOne({
  nome:"Operações LATAM",
  escritorio:ObjectId("ID_DO_BRASIL")
})
```

## 10.3 Contratar 5 pessoas
insertMany com seus dados e colegas.

## 10.4 3 escritórios com maior custo
Aggregation com group e sort.

## 10.5 Suprimentos com mais de 50 unidades
```js
db.escritorios.find({ "suprimentos.quantidade":{ $gt:50 } })
```

## 10.6 Economia com corte salarial
Somar *0.2 salários > 15000 (só calcular)

## 10.7 Vendas sem vendedor
```js
db.vendas.find({ vendedor:{ $exists:false } })
```

## 10.8 Vendedor inexistente
lookup inverso

## 10.9 Produtos com variação >10%
aggregate comparando max vs min

## 10.10 Query geral executiva
aggregate with count, sum, group, top product

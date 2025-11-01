# Relatório Momento – Nível 1

## 1.1 Inclusão do Funcionário
 Inserção de novo colaborador na base de dados da Momento.

Query:

db.funcionarios.insertOne({
  nome: "Vitória",
  sobrenome: "Silva",
  data_nascimento: "2006-11-16",
  data_contratacao: "2025-01-01",
  salario: 5000,
  departamento: "Tecnologia",
  cargo: "Desenvolvedora",
  escritorio: "São Paulo"
})
--------------------------------------------------------------

1.2 Total de Funcionários
Quantidade total de colaboradores da empresa.

Query:
db.funcionarios.countDocuments()

Resultado:
23 funcionários.

---------------------------------------------------------------

## 1.3 Funcionários no Departamento de Tecnologia
Total de colaboradores alocados em Tecnologia.

Query:
db.funcionarios.countDocuments({
  departamento: ObjectId("85992103f9b3e0b3b3c1fe74")
})

Resultado:
 6 funcionários.

-------------------------------------------------------------

1.4 Departamentos Existentes
Listar departamentos e a quantidade total.

Query:
db.departamentos.distinct("nome")
db.departamentos.distinct("nome").length

Resultado:
 7 departamentos.
--------------------------------------------------------------
1.5 Escritórios e Países
Identificar escritórios e países onde a empresa atua.

Query:
db.escritorios.distinct("pais")
db.escritorios.distinct("pais").length

Resultado: 
4 escritórios em: USA, Irlanda, Inglaterra e Equador.


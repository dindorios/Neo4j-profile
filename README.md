# Neo4j-profile - Projeto Grafos de um Serviço de Streaming
Projetos feito no Neo4j - Banco de dados por Grafos

# 🚀 Desafio DIO - Perfil de Destaque com Neo4j

## 📌 Contexto
Este projeto foi desenvolvido como parte do desafio da [DIO.me](https://www.dio.me), com o objetivo de aplicar conceitos de **banco de dados em grafos** utilizando o **Neo4j**.  
A proposta é criar um repositório profissional que demonstre habilidades práticas em modelagem, carga de dados e consultas de negócio.

---

## 🎯 Objetivos
- Construir um modelo de grafo representando Modelagem de Dados em Grafos de um Serviço de Streaming.
- Carregar dados reais ou simulados no Neo4j.
- Criar queries de negócio que mostrem insights relevantes.
- Documentar todo o processo de forma clara e organizada.
- Modelar conexões entre usuários, suas avaliações, atores, diretores e gêneros.
- Demonstrar consultas de negócio que exploram essas relações.
  
🧩 Modelagem do Grafo
Labels utilizadas:
- User
- Film
- Actor
- Director
- Genre
Relacionamentos:
- ASSISTIU → Usuário assistiu um filme
- AVALIOU → Usuário avaliou um filme com nota
- ATUOU → Ator participou de um filme
- DIRIGIDO_POR → Diretor responsável pelo filme
- PERTENCE_A → Filme pertence a um gênero
📷 Veja o esquema visual em /images/schema.png.
📂 Dataset e Scripts
- dataset/filmes.cypher → Script Cypher com todos os filmes e relacionamentos.
- dataset/filmes.csv → (opcional) versão em CSV para uso com LOAD CSV.
- queries/carga.cypher → Script de carga inicial.
- queries/consultas.cypher → Exemplos de consultas de negócio.
🔎 Queries de Negócio
Exemplos de perguntas que o grafo responde:
- Quais filmes Diego assistiu e avaliou?
MATCH (u:User {nome:"Diego"})-[:ASSISTIU]->(f:Film)
OPTIONAL MATCH (u)-[r:AVALIOU]->(f)
RETURN f.titulo AS Filme, f.ano AS Ano, r.nota AS Nota
- Quais atores estão conectados aos filmes que Diego assistiu?
MATCH (u:User {nome:"Diego"})-[:ASSISTIU]->(f:Film)<-[:ATUOU]-(a:Actor)
RETURN DISTINCT a.nome AS Ator
- Qual gênero é mais popular entre os filmes avaliados com nota 5?
MATCH (u:User)-[r:AVALIOU {nota:5}]->(f:Film)-[:PERTENCE_A]->(g:Genre)
RETURN g.nome AS Genero, COUNT(*) AS qtd
ORDER BY qtd DESC





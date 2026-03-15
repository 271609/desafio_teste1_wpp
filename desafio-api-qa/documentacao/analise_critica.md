1. Comportamentos Inesperados ou Inconsistências Identificadas 
1.1. Falta de Validação de Payload 
A API aceita qualquer estrutura de JSON, mesmo com: 
Campos obrigatórios ausentes 
Tipos incorretos 
Exemplo: 
Ao enviar um POST /posts sem userId, a API retorna 201, mesmo que o payload seja inválido. 
Esse comportamento é inconsistente com sistemas reais, onde validações de contrato são 
obrigatórias. 
Mensagem de validação informando que userId é obrigatório. 
{ 
} 
"error": "Validation Error", 
"message": "The field 'userId' is required.", 
"status": 400 
1.2. Operações de Escrita Não São Persistidas 
Chamadas como: 
POST /posts 
PUT /posts/1 
PATCH /posts/1 
DELETE /posts/1 
retornam status de sucesso, mas não alteram o estado real da API, pois a plataforma simula 
respostas. 
Embora seja esperado do JSONPlaceholder, isso deve ser registrado como comportamento não 
persistente. 
Exemplo: Ao Criar o Post não persiste no banco de dados  
Resposta da consulta  
1.3. Consultas por ID Inexistente Retornam {} 
Ao consultar um ID inválido (ex.: /posts/9999), a API retorna: 
Status: 404 
Corpo: {} (objeto vazio) 
APIs reais geralmente retornam mensagens mais consistentes, como: 
{ 
} 
"error": "Resource not found", 
"status": 404 
2. Cenários Priorizados e Justificativas 
Quais cenários você priorizou e por quê? 
A priorização dos testes foi realizada com base em: 
Risco funcional 
Dependência de outros cenários 
Relevância para entender o comportamento da API 
Frequência de uso em sistemas reais 
2.1. Prioridade Alta 
GET /posts 
GET /posts/{id} 
GET /comments 
GET /users 
Consultas por filtros (userId, email) 
Consultas de comentários por post 
Motivo: 
São os endpoints mais frequentemente utilizados para validação estrutural da API. Garantem 
que a leitura de dados essenciais funciona corretamente. 
2.2. Prioridade Média 
POST /posts 
POST /comments 
PUT /posts/{id} 
PATCH /posts/{id} 
DELETE /posts/{id} 
Motivo: 
Embora a API não persista dados, é importante validar os fluxos de escrita, pois essas 
operações fazem parte de um CRUD completo e representam comportamentos essenciais em 
APIs REST. 
2.3. Prioridade Baixa 
Testes avançados de erros 
Motivo: 
Esses testes são relevantes, mas não essenciais para a primeira fase de análise. 
3. O que Seria Testado com Mais Tempo 
O que você testaria a mais se tivesse mais tempo? 
Se houvesse mais tempo para ampliar a análise, seriam incluídos: 
3.1. Testes de Contrato (JSON Schema Validation) 
Mapeamento de cada campo da resposta usando JSON Schema: 
tipos (string, number, boolean) 
campos obrigatórios 
estrutura de objetos 
arrays 
Isso garantiria que nenhum campo seria removido ou alterado sem aviso. 
3.2. Testes de Performance e Carga 
Usando ferramentas como: 
Newman CLI 
3.3. Testes de Segurança 
Como: 
CORS 
Métodos indevidos 
Cabeçalhos obrigatórios 
Rate limit 
4. Melhorias Sugeridas para a API 
Existe alguma melhoria que você sugeriria para essa API, seja em contrato, documentação ou 
comportamento? 
4.1. Padronização de Erros 
Sugestão usar o padrão: 
Formato sugerido: 
{ 
"type": "https://api.exemplo.com/errors/not-found", 
"title": "Resource not found", 
"status": 404, 
"detail": "The post with id 9999 was not found." 
} 
5. Como Garantir a Sustentabilidade dos Testes em Projeto Real 
Como você garantiria a sustentabilidade desses testes num projeto real? 
Se esse conjunto de testes fosse usado em um projeto corporativo, a sustentabilidade seria 
garantida com: 
5.1. Automatização dos Testes 
Rodando em: 
CI/CD (GitHub Actions, GitLab CI, Jenkins) 
Rotinas diárias de regressão 
Pipelines automatizados com Newman ou Cypress API

# Análise Crítica
Durante os testes, identifiquei os seguintes comportamentos não convencionais:
1.1 Falta de validação de campos
A API aceita qualquer payload, inclusive:
Campos ausentes
Campos inválidos
Tipos incorretos
Mesmo com payload inconsistente, a API retorna 201 sem validar nada.



1.2 Operações de escrita não persistem
POST, PUT, PATCH e DELETE não alteram o recurso real, pois a API é apenas simulada.
Esse comportamento é esperado, porém precisa ser comunicado no contexto real de QA.
1.3 GET inexistente retorna "{}" e 404
Algumas rotas retornam corpo vazio {} mesmo com 404.
Não é padrão do mercado.

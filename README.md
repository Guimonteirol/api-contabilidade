<h1 align="center" >  Contabil </h1>
<h2 align="center">API Gerência de despesas e receitas </h2>

> ## Requesitos da aplicação:
- Construir uma REST API com o MongoDB que gerencia as despesas e rendas de uma empresa particular;
 - Realizar CRUD de despesas e receitas;
 - Gerar relatórios em JSON de despesas mensais com:
   - Cada despesa e cada receita do mês.
   - A média de despesas e receitas.
   - O balanço mensal.
	<br>

> ## Tecnologias:
![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=for-the-badge&logo=mongodb&logoColor=white)
![Express.js](https://img.shields.io/badge/express.js-%23404d59.svg?style=for-the-badge&logo=express&logoColor=%2361DAFB)
![NodeJS](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white)
![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)

<br>

> ## Formato do JSON: 			

	"date": "YYYY-MM-DD", 	
	"value": 999.99, 	
	"title": "1", 	
	"description": "Descrição do rubrica do lançamento", 	
	"opcode": boolean (false ou true) 	
	


	Descrição dos campos: 
		date - Data do lançamento. 
		value - Valor do lançamento. 
		title - Classificação do lançamento. 
		description - Descrição da rubrica do lançamento ou observação sobre o mesmo. 
		opcode - 0:despesa 1:receita

<br>

> ## Operações com a API:


###### AddRegistroContabilidade 
	Descricão: Adicionar registro de despesa ou receita <br>
	POST http://localhost:3000/cont/add <br>
	Resultado: Adiciona registros através de POST, abaixo o formato do JSON para a operação: <br>
	
	"date": "YYYY-MM-DD", 	
	"value": 999.99, 	
	"title": "1", 	
	"description": "Descrição do rubrica do lançamento", 	
	"opcode": boolean (false ou true) 	


###### ShowRegistros 
	GET http://localhost:3000/cont/show <br>
	Resultado: Mostra todos os registros cadastrados, tanto de despesas como receitas. </p>

###### ShowOp <br>
	GET http://localhost:3000/cont/showop/:opcode <br>
	Parâmetro na URI {opcode} 0:Despesas 1:Receitas <br>
	Resultado: Mostra todos os registros cadastrados de despesas ou de receitas, conforme opcode 0 ou 1, respectivamente. <br>
	Exemplo: ShowOp - Despesas: <br>  http://localhost:3000/cont/showop/0 <br>
	Exemplo: ShowOp - Receitas: <br>  http://localhost:3000/cont/showop/1 <br> </p>
			
###### ReportRev 
	GET http://localhost:3000/cont/reportRev  <br>
	Resultado: Valor da média de todos as receitas registradas. </p>
	
###### ReportExp 
	GET http://localhost:3000/cont/reportExp <br>
	Resultado: Valor médio de todas as despesas registradas. </p>

###### Remove 
	POST http://localhost:3000/cont/remove <br>
	Parâmetro JSON: { "_id": "código do registro do mongoDB" } <br>
	Resultado: Remoção do documento contido no _id do JSON. Caso não exista o código _id informado ou seja nulo recebe resposta informativa.

###### Update
	POST http://localhost:3000/cont/update <br>
	Exemplo Parâmetro JSON: <br>

	"_id": "CÓDIGO DO REGISTRO DO MONGODB",
	"date": "2021-10-13T00:00:00.000Z", 
	"value": 100.00,
	"title": "1",
	"description": "Teste do update",
	"opcode": true 

	Observações:  
	1. A propriedade _id é obrigatório e a referência para a atualização do registro.
	2. As demais propriedade date, value, title, description ou opcode seguem o formato demonstrado no exemplo acima.
	a. Podem ser alteradas para os valores, dados necessários, de acordo como os seus formatos. 

Resultado: O código _id precisa ser válido, caso inválido recebe mensagem de orientação. Sendo o código _id válido e havendo a declaração dos demais campos, receberá a mensagem de confirmação de atualização do documento. 

###### MonthReport - Relatório Mensal
	GET http://localhost:3000/cont/:month/:year/:opcode  <br>
	:month - Mês para a extração do relatório. <br>
	:year - Ano para a extração do relatório. <br>
	:opcode - 0 para relatório de despesas, 1 para relatório de receitas. <br>

	Exemplo: http://localhost:3000/cont/monthReport/10/2021/0 <br>
	Extração do relatório do mês 10 do ano 2021 despesas (opcode 0).

	Exemplo do JSON de resposta: 

	{
	"histórico_despesas": [ 
    { 
        "_id": "62143383e0911a08d38255ce", 
        "date": "2021-10-30T00:00:00.000Z", 
        "value": 30, 
        "title": "1",
        "description": "Tratamento de data", 
        "opcode": false,
        "__v": 0 
    }, 
    {  
        "_id": "6214d8821fc54c0ee3efcf78", 
        "date": "2021-10-01T00:00:00.000Z",
        "value": 30, 
        "title": "1", 
        "description": "Filtro de período de datas.", 
        "opcode": false, 
        "__v": 0 
    } 
	], 
	"despesas": "DESPESAS 10/2021 : R$ 60" 


Em caso de código de operação inválida é enviada mensagem de orientação. <br> 

###### Balanço Mensal
	GET http://localhosta:3000/cont/:month/:year  <br>
	:month - Mês para a extração do relatório.  <br>
	:year - Ano para a extração do relatório. <br>

	Exemplo: http://localhost:3000/cont/balance/10/2021 Extração do relatório do mês 10 do ano de 2021
<br>
Exemplo do JSON de resposta: <br>

     { <br>
       "despesas": "DESPESAS 10/2021 : R$ 60", <br>
       "receitas": "RECEITAS 10/2021 : R$ 61", <br>
       "resultado": 1 <br>
     } <br>

## Desenvolvedor:

<a href="https://www.linkedin.com/in/guilhermemonteirol/">Guilherme Monteiro</a> |	 


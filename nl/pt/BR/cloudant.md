---

copyright:
  years: 2017-2018
lastupdated: "2018-10-01"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Armazenando documentos no  {{site.data.keyword.cloud_notm}}
{: #cloudant}

O {{site.data.keyword.cloudantfull}} é um Banco de dados como um serviço (DBaaS) orientado a documentos. Ele armazena dados como documentos no formato JSON. O {{site.data.keyword.cloudant_short_notm}} é construído com escalabilidade, alta disponibilidade e durabilidade em mente, além de ser fácil de configurar para uso em aplicativos Node.js. Ele é fornecido com uma ampla variedade de opções de indexação, que incluem o MapReduce, o {{site.data.keyword.cloudant_short_notm}} Query, o índice de texto total e a indexação geoespacial. Os recursos de replicação facilitam a manutenção de dados em sincronia entre os
clusters de banco de dados, PCs desktop e dispositivos móveis.
{:shortdesc}

Para obter mais informações, consulte  [ {{site.data.keyword.cloudant_short_notm}}  Básico ](/docs/services/Cloudant/basics/index.html#cloudant-nosql-db-basics){:new_window}.

## Antes de começar
{: #before}

Verifique se os pré-requisitos a seguir estão prontos:
 * Biblioteca do cliente [Nodejs-cloudant ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudant/nodejs-cloudant){:new_window} 2.3.0+.
 * Deve-se ter uma conta do [{{site.data.keyword.cloud}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/registration/?target=%2Fdeveloper%2Fappservice%2Fcreate-app){: new_window}.
 * Para acessar o {{site.data.keyword.cloudant_short_notm}}, deve-se criar um serviço no [Painel do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/dashboard/apps){: new_window} e, em seguida, ativar o Painel do {{site.data.keyword.cloudant_short_notm}} por meio dessa instância de serviço.
 * Os fragmentos de código nessas instruções usam a autenticação do IAM.
 
### Ativando o IAM com o  {{site.data.keyword.cloudant_short_notm}}
{: #enable_IAM}

Apenas novas instâncias de serviço do {{site.data.keyword.cloudant_short_notm}} podem ser usadas com o {{site.data.keyword.cloud_notm}} IAM.

Todas as novas instâncias de serviço do {{site.data.keyword.cloudant_short_notm}} são ativadas para usar o {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) quando provisionado. Ao provisionar uma nova instância do Catálogo do {{site.data.keyword.cloud_notm}}, escolha o método de autenticação **Usar apenas IAM**. Esse modo significa que somente as credenciais do IAM são fornecidas pela ligação de serviço e a geração de credenciais. É possível localizar mais informações em [{{site.data.keyword.cloud_notm}} Identity and Access Management (IAM)](/docs/services/Cloudant/guides/iam.html).

## Etapa 1. Criando uma instância do  {{site.data.keyword.cloudant_short_notm}}
{: #create-instance}

Quando você cria uma instância do {{site.data.keyword.cloudant_short_notm}}, também cria o banco de dados.

1. Efetue login em sua conta do {{site.data.keyword.cloud_notm}}.
2. No [Painel do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/dashboard/apps){: new_window}, clique em **Criar recurso**. O Catálogo do  {{site.data.keyword.cloud_notm}}  é aberto.
3. No [Catálogo do {{site.data.keyword.cloud_notm}}](https://console.bluemix.net/catalog/), selecione a categoria **Bancos de dados** e, em seguida, clique em {{site.data.keyword.cloudant_short_notm}}. A página de configuração de serviço é aberta.
4. Preencha as informações nos campos a seguir:
  * **Nome do serviço** - Digite um nome para sua instância de serviço ou use o nome pré-configurado.
  * **Escolhe uma região/local no qual implementar** - Selecione uma região na qual implementar seu serviço.
  * **Selecionar um grupo de recursos** - Selecione um grupo de recursos ou aceite o padrão.
  * **Métodos de autenticação disponíveis** - Selecione **Usar apenas IAM** para o método de autenticação.
5. Selecione seu plano de precificação e, em seguida, clique em **Criar**. A página para sua instância de serviço é aberta.
6. Para criar uma credencial de serviço, conclua essas etapas:
  1. No menu de navegação, selecione **Credenciais de serviço**.
  2. Clique em  ** Nova credencial **. A página Incluir nova credencial é aberta.
  3. Na página Incluir nova credencial, preencha os campos e, em seguida, clique em **Incluir**. A nova credencial de serviço é incluída na instância de serviço.
  4. Se desejar visualizar os detalhes da credencial de serviço, clique em **Visualizar credenciais** na coluna **Ações** da nova credencial.
7. No menu de navegação, selecione **Gerenciar** e, em seguida, clique em **Ativar Painel do Cloudant**.
8. No menu de navegação, clique no ícone **Bancos de dados**.
9. Clique em **Criar banco de dados**, forneça um nome de banco de dados e, em seguida, clique em **Criar.** A página do banco de dados é aberta

Se desejar ver informações relacionadas sobre o fornecimento de uma instância do serviço {{site.data.keyword.cloud_notm}}, consulte [Criando uma instância do IBM Cloudant no tutorial do IBM Cloud ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/docs/services/Cloudant/tutorials/create_service.html#creating-a-cloudant-nosql-db-instance-on-ibm-cloud){: new_window}.

## Etapa 2. Instalando o SDK
{: #install}

<!--From github.com/cloudant/nodejs-cloudant#installation-and-usage-->

Comece com seu próprio projeto Node.js e defina esse trabalho como sua dependência. Em outras palavras, coloque o {{site.data.keyword.cloudant_short_notm}} nas dependências do package.json. Use o gerenciador de pacote [npm](https://nodejs.org/) da linha de comandos para instalar o SDK:
```
npm install -- save @cloudant/cloudant
```
{: codeblock}

Observe que o arquivo `package.json` agora mostra o pacote do Cloudant.

## Etapa 3. Inicializando o SDK
{: #initialize}

Depois de inicializar o SDK em seu app, é possível usar o {{site.data.keyword.cloudant_short_notm}} para armazenar dados. Para inicializar sua conexão, insira suas credenciais e forneça uma função de retorno de chamada para ser executada quando tudo estiver pronto.

1. Carregue a biblioteca do cliente incluindo a definição `require` a seguir em seu arquivo `server.js`.
  ```js
  var Cloudant = require ('@cloudant/cloudant');
  ```
  {: codeblock}

2. Inicialize a biblioteca do cliente fornecendo suas credenciais. Use o plug-in `iamauth` para criar um cliente de banco de dados com uma chave API do IAM. 
  ```js
  var cloudant = new Cloudant({ url: 'https://examples.cloudant.com', plugins: { iamauth: { iamApiKey: 'xxxxxxxxxx' } } });
  ```
  {: codeblock}

3. Liste os bancos de dados incluindo o código a seguir em seu arquivo `server.js`.
  ```javascript
  cloudant.db.list (function (err, body) {
  body.forEach (function (db) {
    console.log(db);
    });
  });
  ```
  {: codeblock}

O `Cloudant` em maiúsculas é o pacote que você carrega usando `require()`. O `cloudant` em minúsculas é a conexão autenticada com seu serviço {{site.data.keyword.cloudant_short_notm}}.
{: tip}

### Gerenciando dados com operações básicas
{: #basic_operations}
<!--Borrowed from https://github.com/cloudant/nodejs-cloudant/blob/master/example/crud.js-->

Essas operações básicas ilustram as ações para criar, ler, atualizar e excluir seus documentos usando o cliente inicializado.

#### Criando um Documento
```js
var createDocument = function (callback) {
  console.log("Creating document 'mydoc'");
  // specify the id of the document so you can update and delete it later
  db.insert({ _id: 'mydoc', a: 1, b: 'two' }, function(err, data) {
    console.log('Error:', err);
    console.log('Data:', data);
    callback(err, data);
  });
};
```
{: codeblock}

#### Lendo um documento
```js
var readDocument = function (callback) {
  console.log("Reading document 'mydoc'");
  db.get('mydoc', function(err, data) {
    console.log('Error:', err);
    console.log('Data:', data);
    // keep a copy of the doc so you know its revision token
    doc = data;
    callback(err, data);
  });
};
```
{: codeblock}

#### Atualizando um Documento
```js
var updateDocument = function (callback) {
  console.log("Updating document 'mydoc'");
  // make a change to the document, using the copy we kept from reading it back
  doc.c = true;
  db.insert(doc, function(err, data) {
    console.log('Error:', err);
    console.log('Data:', data);
    // keep the revision of the update so we can delete it
    doc._rev = data.rev;
    callback(err, data);
  });
};
```
{: codeblock}

#### Excluindo um documento
```js
var deleteDocument = function (callback) {
  console.log("Deleting document 'mydoc'");
  // supply the id and revision to be deleted
  db.destroy(doc._id, doc._rev, function(err, data) {
    console.log('Error:', err);
    console.log('Data:', data);
    callback(err, data);
  });
};
```
{: codeblock}

## Etapa 4. Testando o app
{: #test}

Está tudo configurado corretamente? Teste-o para fora!

1. Execute seu aplicativo, certificando-se de iniciar a inicialização e as respectivas operações, como criar um documento.
2. No [Painel do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/dashboard/apps){: new_window}, clique na instância de serviço do {{site.data.keyword.cloudant_short_notm}} criada anteriormente. Quando a instância de serviço for aberta, clique em **Ativar o Painel do Cloudant**.
3. No Painel do {{site.data.keyword.cloudant_short_notm}}, selecione o banco de dados no qual você criou os novos documentos.

Tendo problemas? Verifique a [Referência de API do {{site.data.keyword.cloudant_short_notm}}](/docs/services/Cloudant/api/index.html#api-reference-overview){:new_window}.

## Etapas seguintes
{: #next notoc}

Ótimo trabalho! Você incluiu um nível de persistência segura em seu app. Tente uma das opções a seguir para manter o ritmo:

* Visualize o código-fonte do [{{site.data.keyword.cloudant_short_notm}} SDK for Node.js ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudant/nodejs-cloudant){: new_window}.
* Verifique o [código de exemplo para operações de banco de dados e de documento ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudant/nodejs-cloudant/tree/master/example){: new_window}.
* Os Starter Kits são uma das maneiras mais rápidas de usar os recursos do {{site.data.keyword.cloud}}. Visualize os kits de iniciador disponíveis no [Painel do desenvolvedor de dispositivos móveis ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/developer/mobile/dashboard){: new_window}. Faça download do código. Execute o app!
* Para saber mais e aproveitar todos os recursos oferecidos pelo {{site.data.keyword.cloudant_short_notm}}, [verifique os docs](/docs/services/Cloudant/getting-started.html).
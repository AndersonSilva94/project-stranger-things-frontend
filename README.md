![CAPA LINKEDIN_PERFIL PESSOAL03](https://user-images.githubusercontent.com/52717632/123512102-9546b200-d653-11eb-8b6c-f6c1dd19143e.png)
# Projeto Stranger Things - Front-End :zombie:

Esta é a segunda parte do projeto Stranger Things, para ver o Back-End, basta acessar [aqui](https://github.com/AndersonSilva94/project-stranger-things-backend).

# Habilidades

Nesse projeto, você será capaz de:
  - Publicar aplicações através do `Heroku`;
  - Visualizar logs das suas aplicações publicadas;
  - Monitorar suas aplicações publicadas;
  - Utilizar variáveis de ambiente dentro do `Heroku`;
  - Instalar, utilizar e aproveitar os principais recursos do `PM2`;
  - Fazer deploy no `Heroku` aproveitando recursos de um process manager.

---

## Instruções para clonar o projeto

1. Clone o repositório
  ```bash
  $ git clone https://github.com/AndersonSilva94/project-stranger-things-frontend.git`.
  ```

2. Entre na pasta do repositório que você acabou de clonar:
    ```bash
    $ cd project-stranger-things-frontend
    ```

3. Instale as dependências
  ```bash
  $ npm install
  ```

4. Rode a aplicação
  ```bash
  $ npm start
  ```

---

## O que deverá ser desenvolvido

Você vai adaptar e configurar os projetos descritos nesse README para que seja feito o deploy deles. Você vai colocar os projetos frontend e backend no ar com o `Heroku`, utilizando o `PM2` para gerenciar e monitorar os processos. Além disso, você vai alterar alguns comportamentos aplicando os conceitos vistos no conteúdo.

---

## Testes

### Frontend

Todos os requisitos do projeto serão testados **automaticamente** por meio do `Cypress`. Basta executar um dos comandos abaixo:

```bash
npm run cypress:open // (Com interface)
npm run cy // (via CLI)
```

---

## Deploy - Stranger Things


### Frontend

O frontend consiste em um projeto simples utilizando React, que renderizará o seguinte layout:

<img src="assets/frontend.png" width="800px" >

Trata-se de um frontend bem simples que vai se comunicar com a nossa API. Ele possui as seguintes funcionalidades:

- Uma tabela para exibição da resposta da nossa API;

- Um campo de pesquisa para filtro de **nome**;

- Botões de navegação para paginação;

- Um botão para ativar o modo `Mundo Invertido` no frontend.

Todas essas funcionalidades estão implementadas no componente `StrangerThings`.

---

#### Comunicação com o backend

Na estrutura do projeto, temos um diretório `services`. Nesse diretório, há um arquivo `charactersAPI.js`, onde são feitas as chamadas `HTTP` para a nossa API, utilizando o `axios`.

O service é uma classe que espera receber a URL da nossa API e um timeout para a requisição:

```javascript
{
  url: 'localhost:3003',
  timeout: 30000
}
```

Esses parâmetros estão pré-programados de maneira fixa no componente (alteraremos esse comportamento durante o projeto):

```javascript
const strangerThingsConfig = {
  url: 'localhost:3002',
  timeout: 30000,
};

const upsideDownConfig = {
  url: 'localhost:3003',
  timeout: 30000,
};

const charactersService = new CharactersService(strangerThingsConfig);
const charactersUpsideDownService = new CharactersService(upsideDownConfig);
```

---

#### Modo `upside down` - Frontend

Assim como no backend, o frontend também possui um modo "Mundo Invertido". Esse modo é ativado e desativado com o botão "Mudar de Realidade".

A ideia é a seguinte: inicialmente, o frontend possui uma imagem de background e utiliza o service instanciado com a configuração contida na variável `strangerThingsConfig`. Ao ativar o Mundo Invertido, a imagem de background é alterada e passamos a utilizar o serviço instanciado com a configuração `upsideDownConfig`.

Desse modo, ao "alternar entre os universos", vamos realizar chamadas a API's diferentes.

No exemplo pré-programado, em um dos "universos", chamamos um serviço na porta `3002` e o outro serviço na porta `3003`. Exploraremos esse comportamento durante o projeto.

---

#### Monitoramento

Para monitorar sua aplicaçao no heroku usando o dashboard do PM2, siga os passos abaixo:

1.Crie um novo `bucket` no dashboard de monitoramento web do `PM2`. Em seguida, pelo dashboard, adicione as chaves criadas aos `apps` do Heroku criados anteriomente.

2.Deverão ser adicionadas três variáveis para cada app:

   - O nome do server. No caso, utilizaremos um nome diferente para cada um dos apps;

   - Chave pública;

   - Chave privada.

3.Verifique no Dashboard se os processos estão sendo exibidos e monitorados.

---

## Desenvolvimento

O código não está utilizando variáveis de ambiente. Você vai configurá-lo para utilizá-las, tornando parametrizáveis a porta e o _modo upside down_.

Em seguida, você deverá adicionar o modulo `PM2` ao projeto utilizando o arquivo `ecosystem`, fazendos as adaptações necessárias no `package.json`.

Você vai realizar o deploy do projeto (frontend e backend) no _Heroku_. Para isso, você deverá prepará-los, adicionando os respectivos `Procfiles`. Eles deverão apontar para os scripts adicionados ao `package.json` que utilizam o `PM2`. Por último, você deverá realizar o deploy do projeto, conforme requisitos, no _Heroku_. Os comandos utilizados deverão ser adicionados no README.md de cada projeto. Para mais informações sobre - [Procfiles](https://app.betrybe.com/course/back-end/deployment/infraestrutura-deploy-com-heroku/30597149-145b-49a1-924c-bd8050a8f249/conteudo/dcb89fc5-1093-458d-9b2f-fbac0b18f9bc/introducao-ao-heroku/8e3bf957-decc-40b9-a854-eb406ede0ca9?use_case=side_bar) e [ecosystem](https://app.betrybe.com/course/back-end/deployment/deploy-gerenciadores-de-processos/915a6dce-162b-4015-b499-31ecae9e9411/conteudo/a3b991be-5a2d-4a82-9a38-d96eab5534b5/ecosystem-file/90d1dda4-555a-4cc3-9757-22d72836e230?use_case=side_bar) visite o Course.

Todos esses passos estão detalhados nos requisitos abaixos.

---


## Dicas

Para publicar seu frontend React, utilize o buildpack [mars/create-react-app](https://elements.heroku.com/buildpacks/mars/create-react-app-buildpack).

Lembre-se de que é possível testar o comportamento definindo as variáveis de ambiente em sua máquina. Você pode fazê-las apontar tanto para o backend rodando localmente em sua máquina, quanto para as APIs já publicadas nos requisitos anteriores.


⚠️ **Dica: Lembre-se que ao importar uma variável de ambiente com `process.env.nomeDaVariavel`, seu tipo é `string`.** ⚠️

---

# Requisitos do projeto

⚠️ Lembre-se que o seu projeto só será avaliado se estiver passando por **todos os _checks_** do **Linter**. Utilize o comando `npm run lint` no seu terminal para verificar os _checks_ do **Linter** 😉 ⚠️

Os requisitos estão agrupados por `frontend` e `backend`. Realize as alterações nos respectivos diretórios [disponbilizados para você](#Deploy---Stranger-Things).


### Frontend

#### 7 - Verifica as variáveis de ambiente do frontend

Altere o frontend para utilizar variáveis de ambiente para controlar as **URLs** e **Timeouts** de comunicação com a API.

Perceba que o código está esperando por duas **APIs**. Uma para o modo `upside-down` e a outra para o modo normal.

O nome das variáveis deve ser o seguinte:

- Para seu back-end hawkins:
  - REACT_APP_HAWKINS_URL para a URL;
  - REACT_APP_HAWKINS_TIMEOUT para o timeout;

- Para seu back-end UPSIDEDOWN:
  - REACT_APP_UPSIDEDOWN_URL para a URL;
  - REACT_APP_UPSIDEDOWN_TIMEOUT para o timeout;

O que será testado:
- Se existem as 4 variáveis de ambiente citadas acima.

**Importante**: Para esse projeto, as variáveis de ambiente devem ser definidas em um arquivo .env e o arquivo deve ser enviando no seu PR(Pull Request). ISSO NÃO É UMA PRÁTICA DE MERCADO, o arquivo .env deve ser sempre incluido do .gitignore pois contém informações sensíveis, aqui será enviado apenas por motivo de avaliação.

#### 8 - Verifica se foi feito o deploy do frontend no Heroku

**IMPORTANTE**: Assim como no backend, a variável de ambiente GITHUB_USER

deverá ser criada com o seu usuário do github.

Faça o deploy do front-end:

   1. Crie um app do Heroku com o front-end. Não é necessário a criação do `Procfile` aqui. Vamos deixar o Heroku utilizar as configurações padrões. No momento de criar o app do Heroku, utilize o `buildpack` descrito abaixo, em **Dicas**.

   2. O nome do seu app no heroku deve ser seu nome de usuário do github seguido de "-ft". Por exemplo, se o seu usuário do github for "student", o nome do seu app será "student-ft" e a url ***precisar ser*** https://student-ft.herokuapp.com/.

   2. Configure as variáveis de ambiente do app para apontar para as API's publicadas.

   3. Faça o deploy com o git.

**Dicas**:

Para publicar seu frontend React, utilize o buildpack [mars/create-react-app](https://elements.heroku.com/buildpacks/mars/create-react-app-buildpack).

Lembre-se de que é possível testar o comportamento definindo as variáveis de ambiente em sua máquina. Você pode fazê-las apontar tanto para o backend rodando localmente em sua máquina, quanto para as APIs já publicadas nos requisitos anteriores.

O que será testado:
  - Se ao visitar sua pagina no heroku, o botão de mudar de realidade existe.
  - Se a pesquisa funciona como deveria, fazendo chamada a API externa.
  - Se o botão de mudar de realidade funciona.
  - Se os botões de proxima pagina e pagina anterior funcionam.  

### Bônus

#### 9 - Verifica os multi-ambientes e modo de desenvolvimento.

Utilize a estratégia de multi-ambientes no frontend. Para isso:

   - Renomeie o *remote* atual para `development`;

   - Refaça o deploy com um item no frontend que identifique o layout como rodando em modo de "desenvolvimento". Esse tag item **deve** conter o texto "Em desenvolvimento"

   - Crie um novo app no heroku cujo nome deve ser seu nome de usuário do github seguido de "-pd". Por exemplo, se o seu usuário do github for "student", o nome do seu app será "student-pd" e a url ***precisar ser*** https://student-pd.herokuapp.com/.

   - Lembre-se que a boa prática para essa situação é criar uma variável de ambiente para controlar esse comportamento, configurando-a para ter um valor diferente em cada um dos ambientes.

O que será testado:
 - Se ao acessar o frontend de desenvolvimento, haverá a tag com o texto "Em desenvolvimento"
 - Se ao acessar o frontend de produção, não haverá a tag.

---
:keyboard: com :purple_heart: por [Anderson Silva (Andy)](https://www.linkedin.com/in/andssilva/) 😊

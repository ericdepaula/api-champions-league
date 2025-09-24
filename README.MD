# API de Jogadores e Clubes

Esta é uma API simples para gerenciar informações de jogadores e clubes de futebol, com um foco em dados de jogadores e clubes para a Liga dos Campeões. A API permite visualizar, adicionar, atualizar e deletar dados de jogadores e clubes.

## Arquitetura

O projeto segue uma arquitetura em camadas (n-layer) para separar as responsabilidades, o que facilita a manutenção e o desenvolvimento. As camadas principais são:

  * **Controllers**: Lidam com as requisições HTTP e as respostas, chamando os serviços apropriados.
  * **Services**: Contêm a lógica de negócio da aplicação.
  * **Repositories**: Responsáveis pela interação com a fonte de dados (neste caso, arquivos JSON).
  * **Models**: Definem as interfaces e a estrutura dos dados utilizados.

## Tecnologias Utilizadas

  * **Node.js**: Ambiente de execução.
  * **Express.js**: Framework para construção da API REST.
  * **TypeScript**: Linguagem de programação para garantir tipagem estática e um código mais robusto.
  * **tsup**: Para compilar o código TypeScript em JavaScript.
  * **tsx**: Para executar arquivos TypeScript diretamente.
  * **cors**: Middleware para habilitar o Cross-Origin Resource Sharing.

## Estrutura de Pastas

```
.
├── src/
│   ├── app.ts
│   ├── controllers/
│   │   ├── clubsController.ts
│   │   └── playerController.ts
│   ├── data/
│   │   ├── clubs.json
│   │   └── players.json
│   ├── models/
│   │   ├── clubModel.ts
│   │   ├── httpResponseModel.ts
│   │   ├── playerModel.ts
│   │   └── statisticsModel.ts
│   ├── repositories/
│   │   ├── clubsRepository.ts
│   │   └── playersRepository.ts
│   ├── services/
│   │   ├── clubsService.ts
│   │   └── playersService.ts
│   ├── utils/
│   │   └── httpHelper.ts
│   ├── routes.ts
│   └── server.ts
├── .env.example
├── .gitignore
├── package.json
├── package-lock.json
└── tsconfig.json
```

## Configuração e Instalação

### Pré-requisitos

  * Node.js (versão 18 ou superior)
  * npm

### Passos de Instalação

1.  Clone o repositório:
    ```sh
    git clone https://github.com/ericdepaula/api-soccer-club.git
    cd api-champions-league
    ```
2.  Instale as dependências do projeto:
    ```sh
    npm install
    ```
3.  Crie um arquivo `.env` na raiz do projeto, baseado no arquivo `.env.example`.
    ```sh
    cp .env.example .env
    ```
    O arquivo `.env.example` contém a variável `PORT`, que define a porta em que o servidor será executado.

## Como Executar

### Modo de Desenvolvimento

Para iniciar o servidor com recarga automática, execute o seguinte comando:

```sh
npm run start:watch
```

O servidor será executado na porta configurada no seu arquivo `.env` (padrão: `3000`).

### Modo de Produção

1.  Compile o código TypeScript para JavaScript:
    ```sh
    npm run dist
    ```
2.  Inicie o servidor a partir do código compilado:
    ```sh
    npm run start:dist
    ```

## Endpoints da API

A API está acessível em `http://localhost:<PORT>/api`. Abaixo estão os endpoints disponíveis:

### Jogadores

  * **GET `/api/players`**

      * **Descrição**: Retorna uma lista de todos os jogadores.
      * **Resposta**: `200 OK` com um array de objetos de jogador, ou `204 No Content` se não houver jogadores.

  * **GET `/api/players/:id`**

      * **Descrição**: Retorna um jogador específico com base no `id`.
      * **Parâmetros**: `id` (número inteiro).
      * **Resposta**: `200 OK` com o objeto do jogador, ou `204 No Content` se o jogador não for encontrado.

  * **POST `/api/players`**

      * **Descrição**: Adiciona um novo jogador.
      * **Corpo da requisição**: Um objeto JSON do tipo `PlayerModel`.
      * **Resposta**: `201 Created` se o jogador for adicionado com sucesso, ou `400 Bad Request` se o corpo da requisição estiver vazio.

  * **PATCH `/api/players/:id`**

      * **Descrição**: Atualiza as estatísticas de um jogador específico.
      * **Parâmetros**: `id` (número inteiro).
      * **Corpo da requisição**: Um objeto JSON com as estatísticas a serem atualizadas.
      * **Resposta**: `200 OK` com o objeto do jogador atualizado, ou `204 No Content` se o jogador não for encontrado.

  * **DELETE `/api/players/:id`**

      * **Descrição**: Deleta um jogador específico.
      * **Parâmetros**: `id` (número inteiro).
      * **Resposta**: `200 OK` com a mensagem `"Player deleted"` se o jogador for deletado, ou `400 Bad Request` se o jogador não for encontrado.

### Clubes

  * **GET `/api/clubs`**
      * **Descrição**: Retorna uma lista de todos os clubes.
      * **Resposta**: `200 OK` com um array de objetos de clube, ou `204 No Content` se a lista estiver vazia.


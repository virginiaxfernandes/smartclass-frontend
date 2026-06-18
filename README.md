# SIDAA – Sistema Inteligente e Descentralizado de Acesso Acadêmico
*Projeto Integrador – Análise e Desenvolvimento de Sistemas | Faculdade SENAC Pernambuco*

<br>

**Equipe**
- Allan Falcão
- Jorge Wilson
- Maria Eduarda
- Maria Isabela
- Lívia Frazão
- Thiago Vinícius
- Victoria Zambom
- Virgínia Fernandes

<br>

## Escopo do Projeto 
O sistema consiste em um claviculário inteligente voltado para o controle, monitoramento e
gerenciamento do uso de chaves em ambientes acadêmicos. A solução atende diferentes perfis
de usuários, como professores, funcionários (limpeza, manutenção, entre outros) e equipe de
gestão, garantindo o uso adequado das chaves conforme suas necessidades.

<br>

- **Problema:** O controle manual de chaves físicas gera desorganização, falta de rastreabilidade e
dificuldade na identificação de responsáveis, além de atrasos na retirada e devolução e
pouca visibilidade sobre a utilização das salas.

- **Solução:** Implementação de um claviculário inteligente baseado em tecnologias de Internet das
Coisas (IoT), utilizando um microcontrolador ESP32 integrado a um leitor RFID único e
tags associadas a cada chave. A autenticação dos usuários será realizada por meio de
e-mail e senha, e as movimentações (retirada e devolução) serão registradas a partir da
leitura das tags RFID.
O sistema permitirá o monitoramento em tempo real, controle do estado das chaves
(disponível ou em uso) e geração de alertas em caso de atrasos. Além disso, contará
com um painel administrativo para visualização do status das chaves, identificação dos
responsáveis e acompanhamento da utilização das salas.


- **Objetivo:** Garantir maior controle, segurança e organização no uso de chaves, possibilitando
rastreamento das movimentações, transparência na utilização dos espaços e apoio à
tomada de decisão pela equipe administrativa.

<br>

## Modelagem do Sistema
A modelagem foi desenvolvida com base nos seguintes diagramas UML:

<br>

- **Diagrama de Casos de Uso** – RF001 a RF004
<img width="983" height="616" alt="image" src="https://github.com/user-attachments/assets/783fc28a-f294-430a-ae33-070298c428f8" />

<br><br>

- **Diagrama de Classes** – estrutura das entidades do sistema
<img width="892" height="690" alt="image" src="https://github.com/user-attachments/assets/a9540952-ecb4-4bb3-ae74-405587496ab4" />

<br><br>
  
- **Diagrama de Sequência** – fluxo de retirada e devolução de chaves

<br><br>

- **Diagrama de Atividade** – ciclo de vida de uma movimentação
<img width="1087" height="631" alt="image" src="https://github.com/user-attachments/assets/3dce3ee4-17c0-498b-8ddc-bfc22565e8f4" />

<br>

## Protótipo Arduino / IoT 
O hardware foi desenvolvido com ESP32 (C++) integrado a sensores RFID, responsável por:

- Leitura das tags RFID associadas às chaves
- Envio dos dados ao backend via HTTP/REST + JSON
- Acionamento de buzzer para alertas sonoros
- Comunicação em tempo real com o sistema web

<br>

## Front-end
**Tecnologias:** React.js (PWA) + Tailwind CSS v4 + Vite

**Deploy:** [ smartclass-frontend-self.vercel.app](smartclass-frontend-self.vercel.app)

<br>

**Módulos da interface:**
- Dashboard de Monitoramento em tempo real
- Gestão de Usuários
- Gestão de Salas e Horários
- Relatórios de Movimentações

<br> 

**Como rodar localmente:**

`cd PI4-SmartClassFront-main` ->
`npm install` ->
`npm run dev`

<br>

**Estrutura do Front-end:**

PI4-SmartClassFront-main/

├── public/

├── src/

│   ├── components/

│   ├── pages/

│   └── main.jsx

├── index.html

├── package.json

├── vite.config.js

└── vercel.json

<br>

## Back-end 
**Tecnologias:** Node.js + Express.js + MySQL + JWT + Helmet + express-rate-limit

**Deploy:** 

<br>

**Princípios SOLID aplicados:**

| **Princípio** | **Aplicação** |
|---------------|---------------|
|SRP | `server.js` inicializa apenas a infraestrutura; controllers isolam regras de negócio |
|OCP | `middlewares/auth.js` permite adicionar novos níves de permissão sem alterar a lógica interna |
| SRP | `middlewares/normalizeCategory.js` dedicado exclusivamente à normalização de categorias |

<br>

**Estrutura do back-end:**

backend/

├── server.js          # Ponto de entrada

├── routes/            # Endpoints HTTP → controllers

├── controllers/       # Lógica de negócio (auth, IoT, users, rooms)

├── middlewares/       # JWT, rate limit, normalização

├── config/            # Conexão MySQL

├── utils/             # Scheduler de alertas de atraso

└── scripts/           # Migrate e seed do banco

<br>

**Como rodar localmente**

`npm install` ->
`` ->
`npm start`

<br>

**Variáveis de ambiente necessárias (`.env`):**

DB_HOST=

DB_USER=

DB_PASSWORD=

DB_NAME=

JWT_SECRET=

PORT=

<br>

## Testes de Desempenho e Segurança 
Avaliamos a estabilidade e o tempo de resposta da API do SmartClass ao processar consultas complexas (múltiplos JOINs no MySQL) sob tráfego simultâneo realista. O alvo escolhido foi a rota autenticada de Histórico de Movimentações.

<br>

**Teste de Carga (Load Test)** 

-	Alvo (URL): smartclass-backend-production.up.railway.app
-	Endpoint: GET /api/movements?limit=50&offset=0
-	Autenticação: Cabeçalho Authorization com Token JWT válido (Bearer).
-	Usuários Simultâneos (Threads): 15
-	Tempo de Entrada (Ramp-up): 10 segundos
-	Repetições por Usuário (Loop Count): 4
-	Carga Total Projetada: 60 requisições


















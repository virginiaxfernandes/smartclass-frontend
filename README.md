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
<img width="701" height="330" alt="image" src="https://github.com/user-attachments/assets/bf06b8cb-493f-427f-b02b-8140d847b66f" />


<br><br>

- **Diagrama de Atividade** – ciclo de vida de uma movimentação
<img width="1087" height="631" alt="image" src="https://github.com/user-attachments/assets/3dce3ee4-17c0-498b-8ddc-bfc22565e8f4" />

<br><br>

**Fluxograma**

``mermaid
flowchart TD
    A[Projeto Integrador: SIDAA] --> B[Modelagem do Sistema]
    A --> C[Protótipo Arduino / ESP32]
    A --> D[Front-end]
    A --> G[Back-end]
    A --> H[Testes]
    A --> R[Repositório GitHub]
    B --> B1[Diagrama de Casos de Uso]
    B --> B2[Diagrama de Classes]
    C --> C1[ESP32 e Leitor RFID]
    D --> D1[React]
    D --> D2[Tailwind CSS]
    G --> G1[Node.js / Express]
    G --> G2[MySQL]
    H --> H1[JMeter - Carga e Stress]
    R --> R1[README - conecta todos os artefatos]
    style A fill:#4F46E5,stroke:#312E81,stroke-width:2px,color:#FFF
    style R fill:#059669,stroke:#064E3B,stroke-width:2px,color:#FFF
    style R1 fill:#059669,stroke:#064E3B,stroke-width:2px,color:#FFF``

    <br>

## Protótipo Arduino / IoT 
O hardware foi desenvolvido com ESP32 (C++) integrado a sensores RFID, responsável por:

- Leitura das tags RFID associadas às chaves
- Envio dos dados ao backend via HTTP/REST + JSON
- Acionamento de buzzer para alertas sonoros
- Comunicação em tempo real com o sistema web

**Tinkercad:** 

<br>

## Front-end
**Tecnologias:** React.js (PWA) + Tailwind CSS v4 + Vite

**Deploy:https://smartclass-frontend-self.vercel.app/login** 

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

**Deploy:[https://smartclass-backend-production.up.railway.app](https://smartclass-backend-production.up.railway.app)** 

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

### Teste de Carga (Load Test)

-	Alvo (URL): smartclass-backend-production.up.railway.app
-	Endpoint: GET /api/movements?limit=50&offset=0
-	Autenticação: Cabeçalho Authorization com Token JWT válido (Bearer).
-	Usuários Simultâneos (Threads): 15
-	Tempo de Entrada (Ramp-up): 10 segundos
-	Repetições por Usuário (Loop Count): 4
-	Carga Total Projetada: 60 requisições

<br>

**Resultados Obtidos**

Após a execução do cenário, o painel Summary Report consolidou as seguintes métricas de desempenho:

| **Métrica** | **Resultado** | **Análise** | 
|-------------|---------------|-------------|
| Total de Amostras | 60 | Todas as requisições foram executadas | 
| Taxa de Erro (%) | 0.00% | O servidor processou todas as chamadas com sucesso (HTTP 200 OK), sem rejeições ou falhas de conexão |
| Tempo Médio (Average) | 218 ms | Execelente. Indica que a aplicação responde de forma rápida e responsiva para o usuário final | 
| Tempo Mínimo (Min) | 156ms | Reflete o tempo da resposta mais rápida registrada |
| Tempo Máximo (Max) | 1093ms | Um pico isolado aceitável (pouco mais de 1 segundo), comum em ambientes de nuvem devido à alocação de recursos do *Load Balancer* | 
| Vazão (Throughtput) | 6.0/seg | O sistema conseguiu entregar 6 requisições resolvidas por segundo de forma constante |

<br>

**Conclusão Técnica** 

O teste de carga foi um sucesso absoluto. A infraestrutura backend hospedada no Railway e a modelagem do banco de dados demonstraram alta resiliência e otimização para este volume de requisições.

<br>

### Teste de Stress (Segurança e Rate Limiting) 

Avaliamos a resiliência da infraestrutura de segurança da API do SmartClass sob uma simulação de ataque de força bruta, validando especificamente o funcionamento do middleware de limitação de tráfego (express-rate-limit) configurado para a rota de autenticação.

-	Alvo (URL): smartclass-backend-production.up.railway.app
-	Endpoint: POST /api/auth/login
-	Cabeçalhos: Content-Type: application/json
-	Carga Útil (Body): Credenciais estáticas (marina.souza@senac.br / senha123) -
-	Usuários Simultâneos (Threads): 30
-	Tempo de Entrada (Ramp-up): 2 segundos
-	Repetições por Usuário (Loop Count): 1

<br>

**Resultados Obtidos** 

Após a execução da simulação de ataque, o painel Summary Report apresentou as seguintes métricas consolidadas:

| **Métrica** | **Resultado** | **Análise** | 
|-------------|---------------|-------------|
| Total de Amostras | 30 | O JMeter disparou todas as 30 tentativas planeadas em 2 segundos | 
| Taxa de Erro (%) | 100.00% | Resultado esperado e positivo. O servidor rejeitou corretamente todas as tentativas, protegendo o acesso ao sistema | 
| Tempo médio (Average) | 359 ms | Desempenho excelente, considerando que a rota executa o algoritmo pesado de criptografia bcrypt antes do bloqueio | 
| Tempo Mínimo (Min) | 313 ms | Tempo da resposta mais rápida durante o pico | 
| Tempo Máximo (Max) | 665 ms | O maior tempo de espera registrado não ultrapassou 1 segundo |
| Vazão (Throughtput) | 13.3/seg | O servidor processou cerca de 13 tentativas de login por segundo sem falhas de infraestrutura | 

<br>

**Conclusão Técnica**

O Teste de Stress atesta o sucesso absoluto da arquitetura de segurança implementada. O mecanismo de proteção contra força bruta (loginLimiter) funcionou com total precisão em ambiente de produção, identificando a anomalia de tráfego e cortando o acesso do atacante (neste caso, o próprio JMeter) exatamente após o limite estabelecido, poupando os recursos de processamento e mantendo a estabilidade global da plataforma SmartClass.

<br>

**Prints das configurações e resultados obtidos no JMeter Apache:** 

[Teste de Carga](https://i.imgur.com/xUN55RW.png)

[Teste de Stress](https://i.imgur.com/pklpGVO.png)

<br>





















# AnonGuard 🛡️💬

**Chatbot + Agente Autônomo para suporte emocional e denúncias anônimas seguras.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

O AnonGuard é um sistema projetado para oferecer um espaço seguro e anônimo para vítimas buscarem apoio emocional e orientação. Ele combina um chatbot empático, desenvolvido com a IA generativa Google Gemini, com um agente autônomo capaz de realizar ações como a criação de relatórios de denúncia criptografados e o agendamento de lembretes.

**Funcionalidades Chave:**
* **Suporte Emocional Empático:** Utiliza o Gemini com técnicas de prompt engineering para fornecer respostas seguras e de apoio.
* **Identificação de Intenção:** Detecta a necessidade do usuário (suporte, denúncia, informação, agendamento).
* **Coleta de Dados Estruturada:** Conduz conversas para coletar informações relevantes para denúncias ou agendamentos.
* **Denúncias Anônimas Seguras:** Permite a criação de relatórios (atualmente simulado como texto, futuramente PDF) a partir da conversa, que são criptografados (AES-256) e enviados para o Google Drive (atualmente simulado).
* **Agendamento:** Coleta informações para agendar lembretes ou eventos no Google Calendar (atualmente simulado).
* **Orientação e Informação:** (Funcionalidade futura) Funcionará como uma base de conhecimento conversacional.

---

## ✨ Tecnologias Utilizadas

* **IA Generativa:** Google Gemini (via API `google-generativeai`)
* **Prototipagem de Prompts:** Google AI Studio (para design inicial dos prompts)
* **Ambiente de Desenvolvimento:** Python (inicialmente em Google Colab, migrando para scripts `.py`)
* **Bibliotecas Python Atuais e Planejadas:**
    * `google-generativeai`: Para interação com a API do Gemini.
    * `pycryptodome`: Para criptografia AES-256 (simulação da proteção de dados).
    * `python-dotenv` (planejado): Para gerenciar variáveis de ambiente localmente.
    * `google-api-python-client`, `google-auth-httplib2`, `google-auth-oauthlib` (planejado): Para integração com Google Drive & Calendar APIs.
    * `reportlab` ou `fpdf` (planejado): Para geração de relatórios em PDF.
* **APIs Google (Integração Futura):**
    * Google Drive API: Armazenamento seguro de relatórios.
    * Google Calendar API: Agendamento de lembretes/consultas.
* **Notificações:**
    * Discord Webhook: Alertas anonimizados.

---

## STATUS DO PROJETO
**Em Desenvolvimento Ativo.** Muitas funcionalidades centrais como a interação com o Gemini e a lógica de coleta de dados estão implementadas. As integrações com APIs externas (Google Drive, Calendar) e a geração de PDF são atualmente **simuladas** e estão em processo de desenvolvimento para implementação real.

---

## 📁 Estrutura do Projeto

Abaixo, a organização para os diretórios e arquivos principais do AnonGuard:

AnonGuard/
│
├── .github/
│   └── ISSUE_TEMPLATE/
│       ├── bug_report.md
│       └── feature_request.md
│
├── .gitignore
├── .env.example
├── LICENSE
├── README.md
├── requirements.txt
│
├── src/
│   ├── __init__.py
│   │
│   ├── chatbot/
│   │   ├── __init__.py
│   │   ├── gemini_interface.py
│   │   └── prompts.py
│   │
│   ├── agent/
│   │   ├── __init__.py
│   │   ├── orchestrator.py
│   │   ├── report_generator.py
│   │   └── action_handler.py
│   │
│   ├── core/
│   │   ├── __init__.py
│   │   ├── config.py
│   │   └── encryption.py
│   │
│   ├── apis/
│   │   ├── __init__.py
│   │   ├── google_drive_handler.py
│   │   ├── google_calendar_handler.py
│   │   └── discord_webhook_handler.py
│   │
│   └── utils/
│       ├── __init__.py
│       └── dialog_helpers.py
│
├── notebooks/
│   ├── AnonGuard_Pro_Development.ipynb
│   └── archive/
│       └── (outros notebooks de teste ou versões antigas)
│
├── docs/
│   └── architecture_overview.md
│
├── tests/
│   ├── __init__.py
│   ├── chatbot/
│   │   └── test_gemini_interface.py
│   ├── core/
│   │   └── test_encryption.py
│   └── agent/
│       └── test_orchestrator.py
│
└── main.py

*(Para uma descrição mais detalhada da estrutura e responsabilidades de cada módulo, consulte o código dentro de `src/`)*

---

## ⚙️ Configuração e Instalação (Desenvolvimento)

**Pré-requisitos:**
* Python 3.8+
* Conta Google e acesso à API do Google Gemini.
* Chave de API para o Google Gemini.
* (Futuramente) Credenciais OAuth2 para Google Drive e Calendar APIs.

**Passos:**

1.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/seu-usuario/AnonGuard-Pro.git](https://github.com/seu-usuario/AnonGuard-Pro.git)
    cd AnonGuard-Pro
    ```

2.  **Crie e ative um ambiente virtual (recomendado):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # No Windows: venv\Scripts\activate
    ```

3.  **Instale as dependências:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Configure as variáveis de ambiente:**
    * Copie o arquivo `.env.example` para `.env`:
        ```bash
        cp .env.example .env
        ```
    * Edite o arquivo `.env` e adicione suas chaves:
        ```dotenv
        # Chave da API do Google Gemini
        GEMINI_API_KEY="SUA_CHAVE_API_GEMINI_AQUI"

        # Chave de criptografia (DEVE ter 32 bytes para AES-256)
        # Exemplo (NÃO USE ESTA EM PRODUÇÃO, GERE UMA SEGURA):
        ENCRYPTION_KEY="uma_chave_segura_de_exatamente_32_bytes"

        # Futuramente: Caminho para o arquivo de credenciais do Google Cloud (OAuth2)
        # GOOGLE_APPLICATION_CREDENTIALS="caminho/para/seu/arquivo-de-credenciais.json"
        ```
    * **⚠️ Importante sobre `ENCRYPTION_KEY`:** Para produção, esta chave NUNCA deve ser codificada diretamente ou armazenada no repositório de forma insegura. Considere usar um sistema de gerenciamento de segredos. Para este protótipo, ela é definida via `.env`. **NÃO FAÇA COMMIT do arquivo `.env` com chaves reais.** Adicione `.env` ao seu `.gitignore` (já deve estar lá).
    * No código atual (Colab), a `GEMINI_API_KEY` é carregada via `userdata.get()`. A estrutura modularizada em `src/core/config.py` deve priorizar o uso de variáveis de ambiente do `.env` para desenvolvimento local fora do Colab.

5.  **Para desenvolvimento inicial em Colab (opcional):**
    * Faça upload dos arquivos `.py` relevantes para o seu ambiente Colab ou monte seu Google Drive.
    * Configure os "Secrets" do Colab para `GEMINI_API_KEY` e `ENCRYPTION_KEY` se preferir não usar um arquivo `.env` no Colab.

---

## 🚀 Como Usar (Versão Atual de Desenvolvimento)

1.  Certifique-se de que as configurações (passo 4 acima) estão corretas.
2.  Execute o ponto de entrada principal:
    ```bash
    python main.py
    ```
3.  O chatbot iniciará no console, e você poderá interagir com ele. As funcionalidades de denúncia e agendamento seguirão o fluxo de perguntas, com as ações finais (upload, criação de evento) sendo **simuladas** e exibidas no console.

**Exemplo de fluxo de interação:**
1.  Usuário inicia a conversa.
2.  Chatbot (AnonGuard) responde empaticamente e tenta identificar a intenção.
3.  Se a intenção for "Fazer Denúncia":
    * O chatbot inicia a coleta de dados estruturada.
    * Ao final, o agente simula a geração de um PDF, criptografa os dados e simula o upload para o Google Drive.
4.  Se a intenção for "Agendamento":
    * O chatbot coleta dados para o agendamento.
    * Ao final, o agente simula a criação do evento no Google Calendar.
5.  Se a intenção for "Suporte Emocional":
    * O chatbot mantém uma conversa empática.

---

## 🛡️ Considerações de Segurança

* **Criptografia:** Dados coletados para relatórios são criptografados com AES-256 (atualmente simulado, a biblioteca `PyCryptodome` está sendo usada). A chave (`ENCRYPTION_KEY`) é crucial e deve ser gerenciada com segurança.
* **Chaves de API:** `GEMINI_API_KEY` e futuras credenciais do Google Cloud devem ser gerenciadas via variáveis de ambiente (ou segredos do Colab) e NUNCA incluídas no código-fonte.
* **Tratamento de Dados Sensíveis:** O código busca minimizar o tempo que os dados ficam em memória e anonimizar informações sempre que possível. Este é um ponto de atenção contínuo.
* **Anonimato:** A prioridade é o anonimato do usuário, especialmente na denúncia.
* **Error Handling:** O código inclui blocos `try...except` para lidar com falhas, mas precisa de refinamento contínuo.

---

## 📝 Divisão das Tarefas

Conforme planejado:

* **Chatbot (Gemini):** Projetar prompts para empatia, coleta de dados estruturada, identificação de intenção. Implementar a chamada da API do Gemini.
    * *Ferramentas:* Google AI Studio, Python (`google-generativeai`).
    * *Status Atual:* Funções de interação com Gemini implementadas (`get_gemini_...`), prompts definidos.
* **Criptografia de dados:** Implementar funções de criptografia e descriptografia AES-256. Definir formato dos dados. Gerenciar a chave.
    * *Ferramentas:* Python (`PyCryptodome`).
    * *Status Atual:* Funções de simulação de criptografia/descriptografia AES implementadas.
* **Integração com APIs (Google Drive, Calendar, Discord):** Configurar autenticação (OAuth2). Escrever funções para upload, criação de evento, alertas.
    * *Ferramentas:* Python, Google APIs.
    * *Status Atual:* **Simulado.** Esta é uma das próximas etapas de desenvolvimento.
* **Lógica do Agente Autônomo:** Orquestrar o fluxo: receber dados do chatbot, chamar funções de criptografia/API, gerar PDF, decidir qual ação tomar.
    * *Ferramentas:* Python, `reportlab`/`fpdf`.
    * *Status Atual:* Lógica de orquestração básica implementada no loop principal. Geração de PDF **simulada**.
* **Documentação (GitHub):** Escrever README claro, comentários no código, vídeo de demonstração.
    * *Ferramentas:* Markdown, Vídeo, Comentários no código.
    * *Status Atual:* Este README é o início. Comentários no código existem.

---

## 🤝 Contribuição

*(Esta seção pode ser expandida se o projeto se tornar aberto a contribuições externas futuramente)*

No momento, o projeto está sendo desenvolvido somente por mim. Caso no futuro queira participar deste projeto siga os passos:
1.  Crie uma Branch para sua Feature (`git checkout -b feature/MinhaNovaFeature`).
2.  Faça Commit suas mudanças (`git commit -m 'Adiciona MinhaNovaFeature'`).
3.  Faça Push para a Branch (`git push origin feature/MinhaNovaFeature`).
4.  Abra um Pull Request para a `main` (ou `develop`, se usada).

---

## 📜 Licença

Distribuído sob a Licença MIT.

---

## 📞 Contato

Nome do Projeto Link: [https://github.com/lucas-lins-lima/AnonGuard](https://github.com/lucas-lins-lima/AnonGuard) ---

## 📹 Vídeo de Demonstração (A ser adicionado que será posto pelo YouTube)

*(Link para o vídeo de demonstração quando estiver pronto)*

---

## 🛣️ Próximos Passos / Roadmap

Abaixo estão os marcos já alcançados e os próximos passos planejados para o AnonGuard:

**Funcionalidades e Módulos Implementados (Protótipo/Base):**

* **Chatbot (Interação com Gemini):**
    * [x] Design e implementação de prompts para:
        * [x] Suporte emocional empático.
        * [x] Identificação de intenção do usuário.
        * [x] Coleta de dados estruturada para denúncias.
        * [x] Coleta de dados estruturada para agendamentos.
    * [x] Implementação das chamadas à API do Gemini para todas as funcionalidades de conversação listadas acima.
* **Criptografia de Dados (Base):**
    * [x] Implementação de funções de criptografia (AES-256 com PyCryptodome) e descriptografia para os dados da denúncia.
    * [x] Definição do formato dos dados a serem criptografados (conteúdo do relatório em texto).
    * [x] Mecanismo para gerenciamento da chave de criptografia via variável de ambiente (para prototipagem).
* **Lógica do Agente Autônomo (Orquestração Inicial):**
    * [x] Orquestração do fluxo principal da conversa, alternando entre estados (suporte, coleta para denúncia, coleta para agendamento) com base na intenção identificada.
    * [x] Chamada das funções de coleta de dados do chatbot.
    * [x] Chamada da função de criptografia para os dados da denúncia.
    * [x] Simulação das seguintes ações do agente:
        * [x] Geração de conteúdo para o relatório PDF.
        * [x] Upload do relatório criptografado para o Google Drive.
        * [x] Criação de evento no Google Calendar.
* **Documentação e Código:**
    * [x] Código fonte inicial com comentários explicativos e docstrings.
    * [x] Elaboração da estrutura inicial e conteúdo do `README.md`.

**Próximas Implementações e Melhorias:**

* **Integração Real com APIs Google:**
    * [ ] Configurar autenticação OAuth2 segura para Google Drive e Google Calendar.
    * [ ] Substituir a simulação pela implementação real do upload de arquivos criptografados para o Google Drive.
    * [ ] Substituir a simulação pela implementação real da criação de eventos no Google Calendar.
* **Geração de Relatórios em PDF:**
    * [ ] Integrar uma biblioteca como `reportlab` ou `fpdf` para gerar os relatórios de denúncia em formato PDF antes da criptografia.
* **Funcionalidade de Orientação e Informação:**
    * [ ] Desenvolver o fluxo e a base de conhecimento para "Buscar Informações/Orientação", permitindo ao chatbot fornecer informações sobre direitos, ONGs e próximos passos de forma conversacional.
* **Aprimoramentos de Robustez e Segurança:**
    * [ ] Melhorar o tratamento de exceções em todo o sistema para maior resiliência.
    * [ ] Implementar um sistema de logging mais estruturado e detalhado (substituindo os `print` de debug).
    * [ ] Realizar uma revisão completa do fluxo de dados sensíveis e da implementação da criptografia, visando melhores práticas.
    * [ ] Planejar e executar testes de segurança.
* **Testes Automatizados:**
    * [ ] Escrever testes unitários para os principais módulos (chatbot, criptografia, agente).
    * [ ] Desenvolver testes de integração para os fluxos completos.
* **Interface do Usuário (Consideração Futura):**
    * [ ] Avaliar e, se aplicável, desenvolver uma interface de usuário mais amigável além do console (ex: interface web simples, integração com plataformas de mensagem).
* **Webhook Discord (Consideração futura):**
    * [ ] Se decidido como prioritário, implementar o envio de alertas anonimizados para uma equipe de moderação via Discord Webhook em situações de risco extremo detectadas.
* **Documentação Final e Demonstração:**
    * [ ] Finalizar e refinar toda a documentação do projeto.
    * [ ] Gravar e editar um vídeo de demonstração do AnonGuard.

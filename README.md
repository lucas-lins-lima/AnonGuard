1. Ideia Principal

Nome do Projeto: AnonGuard Proposta: Chatbot + Agente Autônomo que:



Oferece suporte emocional empático via Gemini (IA generativa), utilizando técnicas de prompt engineering para garantir respostas seguras e de apoio em situações sensíveis.

Orienta vítimas sobre direitos, próximos passos e canais de ajuda confiáveis (integrado com bases de dados de ONGs ou informações pré-carregadas), funcionando como um knowledge base acessível conversacionalmente.

Permite denúncias anônimas com relatórios estruturados (Google Drive/PDF), onde o agente autônomo coleta dados específicos durante a conversa e os formata para um documento seguro, acionado pelo usuário. O foco na anonimidade é crucial para encorajar vítimas a buscar ajuda sem medo de retaliação.



2. Tecnologias e Ferramentas

Google Gemini (API Key): A espinha dorsal conversacional. Usado para entender a linguagem natural, manter o contexto da conversa, oferecer suporte emocional e extrair informações relevantes para a denúncia/ação do agente. O prompt deve ser finamente ajustado para lidar com temas delicados e evitar respostas inadequadas.

Google AI Studio: Essencial para prototipar rapidamente diferentes prompts e fluxos de conversa para o chatbot, testando a capacidade do Gemini de responder de forma empática e coletar dados de forma não intrusiva antes de escrever o código principal.

Google Colab: Ambiente de desenvolvimento em Python. Perfeito para integrar as APIs, implementar a lógica do agente autônomo, gerenciar a criptografia, processar os dados coletados pelo chatbot e gerar os relatórios. Precisaremos de bibliotecas como google-api-python-client para as APIs do Google e uma biblioteca de criptografia como PyCryptodome para AES.

Extras:

Google Drive API: Usada para armazenar os relatórios gerados de forma segura. Os arquivos devem ser criptografados antes de serem enviados para o Drive, garantindo que mesmo que o Drive seja comprometido, os dados permaneçam ilegíveis sem a chave de criptografia.

Google Calendar API: O agente autônomo pode usar esta API para agendar automaticamente um lembrete ou um evento (como uma consulta inicial com uma ONG parceira, se a vítima consentir), baseando-se nas informações e no consentimento obtidos na conversa com o chatbot.

Discord Webhook (opcional): Pode ser configurado para enviar alertas anonimizados para uma equipe de moderação ou suporte em tempo real, caso o chatbot detecte uma situação de risco extremo baseada em keywords ou no fluxo da conversa (sem identificar o usuário).

Considerações Técnicas e de Segurança:



Criptografia: Implementar AES-256 para criptografar os dados coletados antes de salvar no Google Drive. A chave de criptografia deve ser gerenciada de forma segura (idealmente não armazenada junto com os dados ou no código-fonte, mas para um protótipo, podemos simplificar, deixando claro a ressalva).

API Keys: Nunca embutir API keys diretamente no código. Usar variáveis de ambiente ou um arquivo .env carregado de forma segura no Colab.

Tratamento de Dados Sensíveis: O código deve ser cuidadoso ao manipular as informações coletadas, minimizando o tempo que os dados ficam em memória e garantindo que apenas os dados necessários e anonimizados sejam processados ou armazenados.

Error Handling: Implementar blocos try...except para lidar com falhas nas chamadas de API (Gemini, Drive, Calendar) e garantir que o sistema não quebre inesperadamente, oferecendo feedback adequado ao usuário.



3. Divisão de Tarefas

(Como equipe: você, Elliot e Darlene)


- Chatbot (Gemini): Projetar prompts para empatia, coleta de dados estruturada, identificação de intenção (denúncia, suporte, agendamento). Implementar a chamada da API do Gemini no Colab - ferramentas são Google AI Studio, Python

- Criptografia de dados: Implementar funções de criptografia e descriptografia AES-256. Definir formato dos dados a serem criptografados (e.g., JSON). Gerenciar a chave (para o protótipo, definir como será tratada) - ferramentas são Python (Colab), "PyCryptodome"

- Integração com APIs: Configurar autenticação (OAuth2). Escrever funções para: 1) Upload de arquivo criptografado no Drive. 2) Criação de evento no Calendar. 3) Opcional: Enviar alerta via Discord Webhook - ferramentas são Python (Colab), Google APIs

- Lógica do Agente Autônomo: Orquestrar o fluxo: receber dados do chatbot, chamar funções de criptografia/API, gerar PDF (usando uma lib como reportlab ou fpdf), decidir qual ação tomar (salvar relatório, agendar) - Elliot/Darlene

- Documentação (GitHub): Escrever README claro (instalação, uso, arquitetura, notas de segurança). Adicionar comentários explicativos no código. Gravar e editar o vídeo de demonstração - ferramentas são README.md, Vídeo, Code Comments

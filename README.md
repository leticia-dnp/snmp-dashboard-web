📋 Sobre o projeto

Este repositório contém a implementação de um trabalho acadêmico cujo objetivo é demonstrar, na prática, a coleta de informações de gerenciamento de rede via SNMP (Simple Network Management Protocol), utilizando OIDs padronizados da MIB-2 (RFC 1213).
Como o ambiente de laboratório não permite acesso de administrador na máquina de testes, a entrega oficial do trabalho é feita por meio de vídeo de demonstração, mostrando:

✅ O agente SNMP (snmpd) em execução como serviço do sistema operacional;
✅ A aplicação web consumindo os dados via SNMP em tempo real;
✅ O código-fonte completo, disponível neste repositório;
✅ A contribuição individual de cada integrante da equipe.

⚙️ Funcionalidades:

Consulta automática de dados SNMP a cada intervalo configurável;
Exibição dos dados em cards e tabelas em uma página web responsiva;
Atualização assíncrona via JavaScript (sem necessidade de recarregar a página);
Tratamento de erros de conexão/timeout com o agente SNMP;
Configuração do host, porta e community via variáveis de ambiente.

💡 Como item extra (bônus), o dashboard também pode listar as interfaces de rede (ifTable — OID 1.3.6.1.2.1.2.2), exibindo nome, status e tráfego de entrada/saída.

🏗️ Arquitetura
┌─────────────┐      HTTP       ┌──────────────┐      SNMP GET/WALK      ┌──────────────┐
│  Navegador   │ ──────────────▶ │  Flask App    │ ───────────────────────▶ │  Agente SNMP  │
│ (Dashboard)  │ ◀────────────── │ (app.py)      │ ◀─────────────────────── │  (snmpd)      │
└─────────────┘   JSON (fetch)  └──────────────┘        Rede/Localhost     └──────────────┘

O snmpd roda como serviço na máquina alvo, expondo a MIB-2 na porta 161/UDP.
A aplicação Flask consulta o agente via snmpget/snmpwalk (Net-SNMP).
O frontend (HTML/CSS/JS) busca os dados via fetch() no endpoint /api/snmp-data e atualiza o dashboard automaticamente.

📁 Estrutura do projeto
snmp-dashboard-web/
├── app.py                 # Aplicação Flask (rotas web e API)
├── snmp_client.py          # Camada de coleta de dados via SNMP
├── requirements.txt        # Dependências Python
├── .env.example             # Modelo de variáveis de ambiente
├── templates/
│   └── index.html          # Página principal do dashboard
├── static/
│   ├── css/style.css       # Estilos do dashboard
│   └── js/dashboard.js     # Requisições assíncronas e atualização da UI
└── README.md

👥 Equipe e contribuições
Integrantes e	Contribuição
Letícia do Nascimento Pereira: Configuração do agente SNMP e testes de conectividade, Desenvolvimento do frontend (HTML/CSS/JS) e  Documentação e gravação do vídeo de apresentação
Vagner Silveira Rocha Jr. Desenvolvimento do backend (Flask + coleta SNMP), Configuração do agente SNMP e testes de conectividade e Documentação e gravação do vídeo de apresentação

🎥 Vídeo de demonstração

📺 Link do vídeo:

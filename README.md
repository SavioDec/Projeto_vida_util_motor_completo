#D.I.V.I - Detector Industrial de Vibração e Inteligência
       2
       3 Este é o repositório principal (Umbrella) que consolida o ecossistema do projeto **D.I.V.I**. O sistema utiliza IoT (ESP32) para monitorar a saúde de motores industriais, integrando telemetria em tempo real,
         persistência local resiliente (SQLite) e análise histórica em nuvem (Firebase).
       4
       5 ---
       6
       7 ## 🏗 Estrutura do Ecossistema
       8
       9 O projeto é dividido em dois grandes pilares, gerenciados aqui via **Git Submodules**:
      10                                                                                                                                                                                                                            
      11 1.  **[Backend (Gateway IoT)](backend/):** Desenvolvido em .NET 9. Atua como o cérebro local, processando dados da Serial, gerenciando o banco SQLite e sincronizando lotes com o Firebase.                          quota
      12 2.  **[Frontend (Dashboard)](frontend/):** Desenvolvido em Next.js 15. Interface administrativa para monitoramento em tempo real, controle de ativos e análise preditiva.                                         15% used
      13
      14 ---
      15
      16 ## 🚀 Como Clonar e Iniciar
      17
      18 Como este repositório utiliza submódulos, o comando de clone deve ser recursivo:
      19
      20 ### 1. Clonagem Completa
      21 ```bash
      22 git clone --recursive https://github.com/SavioDec/Projeto_vida_util_motor_completo.git
      23 cd Projeto_vida_util_motor_completo
      24 ```
      25
      26 ### 2. Iniciando o Back-End (Gateway)
      27 O Back-End deve ser o primeiro a ser iniciado para que a API esteja disponível para o Front.
      28 ```bash
      29 cd backend
      30 # Certifique-se de que o arquivo firebase-auth.json está nesta pasta
      31 dotnet run
      32 ```
      33 *O servidor subirá em `http://localhost:5001`.*
      34
      35 ### 3. Iniciando o Front-End (Dashboard)
      36 Em outro terminal:
      37 ```bash
      38 cd frontend
      39 npm install
      40 npm run dev
      41 ```
      42 *O dashboard estará disponível em `http://localhost:3000`.*
      43
      44 ---
      45
      46 ## 🛠 Fluxo de Dados
      47
      48 1.  **Sensores -> ESP32:** Captura vibração e estado de emergência.
      49 2.  **ESP32 -> Gateway (.NET):** Envia dados via Serial (USB).
      50 3.  **Gateway -> SQLite:** Grava instantaneamente para garantir que nenhum dado seja perdido se a internet cair.
      51 4.  **Gateway -> Firebase:** Sincroniza lotes de dados localmente a cada 5 minutos para economia de banda e cota.
      52 5.  **Gateway -> Dashboard:** Disponibiliza API local para visualização em tempo real (0s de latência de nuvem).
      53 6.  **Firebase -> Dashboard:** Fornece dados históricos para análise de tendências de longo prazo.
      54
      55 ---
      56
      57 ## 📝 Requisitos para Funcionamento
      58 - **Hardware:** ESP32 conectado via USB ao computador rodando o Gateway.
      59 - **Software:** .NET 9 SDK, Node.js v18+, Arquivo de credenciais `firebase-auth.json`.
      60
      61 ---
      62
      63 ## 🔗 Repositórios Individuais
      64 Caso deseje contribuir ou visualizar os históricos separadamente:
      65 - [Repositório de Telemetria (Back-End)](https://github.com/SavioDec/backend_detector_vida_util_motor)
      66 - [Repositório de Interface (Front-End)](https://github.com/SavioDec/frontend_detector_vida_util_motor)

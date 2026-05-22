## D.I.V.I - Detector Industrial de Vibração e Inteligência

 Este é o repositório principal (Umbrella) que consolida o ecossistema do projeto **D.I.V.I**. O sistema utiliza IoT (ESP32) para monitorar a saúde de motores industriais, integrando telemetria em tempo real,
         persistência local resiliente (SQLite) e análise histórica em nuvem (Firebase).

---

 ## 🏗 Estrutura do Ecossistema

 O projeto é dividido em dois grandes pilares, gerenciados aqui via **Git Submodules**:
                                                                                                                                                                                                                            
1.  **[Backend (Gateway IoT)](backend/):** Desenvolvido em .NET 9. Atua como o cérebro local, processando dados da Serial, gerenciando o banco SQLite e sincronizando lotes com o Firebase.                          quota
 2.  **[Frontend (Dashboard)](frontend/):** Desenvolvido em Next.js 15. Interface administrativa para monitoramento em tempo real, controle de ativos e análise preditiva.                                         15% used


 ## 🚀 Como Clonar e Iniciar

 Como este repositório utiliza submódulos, o comando de clone deve ser recursivo:

 ### 1. Clonagem Completa
 ```bash
 git clone --recursive https://github.com/SavioDec/Projeto_vida_util_motor_completo.git
 cd Projeto_vida_util_motor_completo
 ```
 ### 2. Iniciando o Back-End (Gateway)
 O Back-End deve ser o primeiro a ser iniciado para que a API esteja disponível para o Front.
 ```bash
 cd backend
 # Certifique-se de que o arquivo firebase-auth.json está nesta pasta
 dotnet run
 ```
 *O servidor subirá em `http://localhost:5001`.*

 ### 3. Iniciando o Front-End (Dashboard)
 Em outro terminal:
 ```bash
 cd frontend
 npm install
 npm run dev
 ```
 *O dashboard estará disponível em `http://localhost:3000`.*

 ---

 ## 🛠 Fluxo de Dados

 1.  **Sensores -> ESP32:** Captura vibração e estado de emergência.
 2.  **ESP32 -> Gateway (.NET):** Envia dados via Serial (USB).
 3.  **Gateway -> SQLite:** Grava instantaneamente para garantir que nenhum dado seja perdido se a internet cair.
 4.  **Gateway -> Firebase:** Sincroniza lotes de dados localmente a cada 5 minutos para economia de banda e cota.
 5.  **Gateway -> Dashboard:** Disponibiliza API local para visualização em tempo real (0s de latência de nuvem).
6.  **Firebase -> Dashboard:** Fornece dados históricos para análise de tendências de longo prazo.

 ---
 ## 📝 Requisitos para Funcionamento
 - **Hardware:** ESP32 conectado via USB ao computador rodando o Gateway.
 - **Software:** .NET 9 SDK, Node.js v18+, Arquivo de credenciais `firebase-auth.json`.

 ---

 ## 🔗 Repositórios Individuais
 Caso deseje contribuir ou visualizar os históricos separadamente:
 - [Repositório de Telemetria (Back-End)](https://github.com/SavioDec/backend_detector_vida_util_motor)
 - [Repositório de Interface (Front-End)](https://github.com/SavioDec/frontend_detector_vida_util_motor)

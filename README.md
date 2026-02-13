#🖥️ PowerKeeper.dart - Sistema de Gerenciamento e Análise#
Backend e Interface de Linha de Comando do PowerKeeper
Desenvolvido por Luiz Gustavo, Matteo e Nicolas
Ciência da Computação | Unifeob 2025.1 e 2025.2

#📘 Visão Geral#
O PowerKeeper.dart é o módulo de backend e gerenciamento do sistema PowerKeeper, responsável por processar, analisar e administrar os dados coletados pelos dispositivos IoT ESP32. Implementado em Dart, oferece uma interface de linha de comando robusta para operações administrativas e análise de dados energéticos.
Este módulo se conecta ao Firebase Realtime Database para recuperar leituras dos sensores, realizar cálculos estatísticos, gerar relatórios e gerenciar o cadastro de dispositivos e usuários do sistema.

⚙️ Funcionalidades Principais
📊 Análise de Dados

Processamento de leituras em tempo real do Firebase
Cálculos estatísticos: média, máximo, mínimo, desvio padrão
Análise de tendências de consumo ao longo do tempo
Detecção de anomalias em padrões de uso energético
Agregação de dados por período (diário, semanal, mensal)

📈 Geração de Relatórios

Relatórios de consumo por dispositivo e período
Comparativos históricos entre diferentes períodos
Exportação de dados em formatos CSV, JSON
Gráficos e visualizações de consumo (ASCII art para CLI)
Alertas de consumo acima de limiares configurados

🔐 Gerenciamento de Sistema

CRUD de dispositivos: cadastro, edição, exclusão
Gerenciamento de usuários e níveis de acesso
Configuração de parâmetros do sistema
Backup e restauração de dados
Logs de auditoria de operações administrativas

🔌 Integração com Firebase

Leitura de leituras da tabela /leituras
Acesso a snapshots via /ultima_leitura
Consulta de fechamentos em /consumos_diarios
Sincronização bidirecional de dados
Cache local para operações offline

📡 Interface CLI

Menu interativo para navegação
Comandos parametrizados para automação
Output formatado com cores e tabelas
Modo batch para scripts e agendamentos
Help system integrado


🗂️ Estrutura do Projeto
powerkeeper.dart/
│
├── bin/
│   └── powerkeeper.dart          # Ponto de entrada da aplicação CLI
│
├── lib/
│   ├── models/
│   │   ├── reading.dart          # Modelo de dados de leitura
│   │   ├── device.dart           # Modelo de dispositivo
│   │   ├── daily_consumption.dart # Modelo de consumo diário
│   │   └── user.dart             # Modelo de usuário
│   │
│   ├── services/
│   │   ├── firebase_service.dart # Comunicação com Firebase
│   │   ├── analytics_service.dart # Análises e estatísticas
│   │   ├── report_service.dart   # Geração de relatórios
│   │   └── auth_service.dart     # Autenticação e autorização
│   │
│   ├── utils/
│   │   ├── date_utils.dart       # Utilitários de data/hora
│   │   ├── formatters.dart       # Formatação de dados
│   │   └── validators.dart       # Validações
│   │
│   └── cli/
│       ├── commands/             # Implementação de comandos CLI
│       ├── menu.dart             # Sistema de menus
│       └── output.dart           # Formatação de saída
│
├── test/
│   └── unit/                     # Testes unitários
│
├── pubspec.yaml                  # Dependências do projeto
├── analysis_options.yaml         # Configurações de análise
└── README.md                     # Este arquivo

🚀 Instalação e Configuração
Pré-requisitos

Dart SDK >= 3.0.0
Firebase Account com projeto configurado
Credenciais Firebase (service account JSON)

1️⃣ Instalação do Dart SDK
Linux/macOS:
bash# Via Homebrew (macOS)
brew tap dart-lang/dart
brew install dart

# Via apt (Ubuntu/Debian)
sudo apt update
sudo apt install dart
Windows:
powershell# Via Chocolatey
choco install dart-sdk
Verificar instalação:
bashdart --version
2️⃣ Clonar o Repositório
bashgit clone https://github.com/dLuizg/powerkeeper.dart.git
cd powerkeeper.dart
3️⃣ Instalar Dependências
bashdart pub get
4️⃣ Configurar Firebase

Baixe o arquivo de credenciais do Firebase:

Acesse Firebase Console
Vá em Configurações do Projeto → Contas de Serviço
Clique em Gerar nova chave privada
Salve o arquivo como firebase_credentials.json


Configure as variáveis de ambiente:

bash# Linux/macOS
export FIREBASE_CREDENTIALS_PATH="./firebase_credentials.json"
export FIREBASE_DATABASE_URL="https://seu-projeto.firebaseio.com"

# Windows (PowerShell)
$env:FIREBASE_CREDENTIALS_PATH=".\firebase_credentials.json"
$env:FIREBASE_DATABASE_URL="https://seu-projeto.firebaseio.com"
Ou crie um arquivo .env:
envFIREBASE_CREDENTIALS_PATH=./firebase_credentials.json
FIREBASE_DATABASE_URL=https://seu-projeto.firebaseio.com

💻 Uso
Executar a Aplicação
bash# Modo interativo (menu)
dart run

# Comando direto
dart run bin/powerkeeper.dart --help
Exemplos de Comandos
Listar Dispositivos
bashdart run bin/powerkeeper.dart devices list
Visualizar Leituras de um Dispositivo
bashdart run bin/powerkeeper.dart readings --device-id 1 --from 2025-02-01 --to 2025-02-13
Gerar Relatório de Consumo
bashdart run bin/powerkeeper.dart report --device-id 1 --period monthly --month 02 --year 2025
Analisar Consumo Diário
bashdart run bin/powerkeeper.dart analyze daily --date 2025-02-13
Exportar Dados
bashdart run bin/powerkeeper.dart export --format csv --output consumo_fevereiro.csv --month 02
Cadastrar Novo Dispositivo
bashdart run bin/powerkeeper.dart devices add --name "Máquina de Solda 3" --location "Galpão B"
Verificar Anomalias
bashdart run bin/powerkeeper.dart anomalies --threshold 150 --device-id 1

📦 Dependências
Principais Bibliotecas
yamldependencies:
  # Firebase
  firebase_admin: ^0.3.0           # SDK administrativo Firebase
  firebase_dart: ^1.0.0            # Cliente Firebase para Dart
  
  # CLI
  args: ^2.4.0                     # Parser de argumentos
  cli_menu: ^2.0.0                 # Menus interativos
  interact: ^2.2.0                 # Prompts interativos
  
  # Utilitários
  intl: ^0.18.0                    # Formatação i18n
  path: ^1.8.0                     # Manipulação de caminhos
  dotenv: ^4.1.0                   # Variáveis de ambiente
  
  # Data & Analytics
  collection: ^1.17.0              # Coleções utilitárias
  charts: ^0.5.0                   # Geração de gráficos
  csv: ^5.1.0                      # Manipulação CSV
  
dev_dependencies:
  test: ^1.24.0                    # Framework de testes
  mockito: ^5.4.0                  # Mocking para testes
  lints: ^2.1.0                    # Regras de lint

🧪 Testes
Executar Todos os Testes
bashdart test
Executar Testes Específicos
bashdart test test/services/analytics_service_test.dart
Cobertura de Testes
bashdart pub global activate coverage
dart pub global run coverage:test_with_coverage
```

---

## 📊 Exemplos de Output

### Relatório de Consumo Mensal
```
╔════════════════════════════════════════════════════════════╗
║        RELATÓRIO DE CONSUMO - FEVEREIRO 2025              ║
║        Dispositivo: #1 - Máquina de Solda Principal       ║
╠════════════════════════════════════════════════════════════╣
║ Total do Período:           145.67 kWh                    ║
║ Média Diária:                11.21 kWh                    ║
║ Dia de Maior Consumo:        18.45 kWh (2025-02-05)      ║
║ Dia de Menor Consumo:         6.32 kWh (2025-02-10)      ║
║                                                            ║
║ Custo Estimado (R$ 0,85/kWh): R$ 123,82                  ║
╚════════════════════════════════════════════════════════════╝

Consumo por Dia:
01 ███████████░ 12.3 kWh
02 ████████████ 13.1 kWh
03 ██████████░░ 10.8 kWh
04 █████████░░░  9.4 kWh
05 ████████████████ 18.5 kWh
...
```

### Detecção de Anomalias
```
⚠️  ANOMALIAS DETECTADAS

Dispositivo #1 - 2025-02-13 14:35:00
├─ Pico de consumo: 245.8W (150% acima da média)
├─ Duração: 15 minutos
└─ Recomendação: Verificar funcionamento do equipamento

Dispositivo #1 - 2025-02-12 03:22:00
├─ Consumo fora do horário: 87.3W
├─ Horário atípico: 03:22 AM
└─ Recomendação: Verificar se equipamento foi deixado ligado

🔧 Configuração Avançada
Arquivo de Configuração (config.yaml)
yaml# PowerKeeper Configuration
app:
  name: "PowerKeeper CLI"
  version: "1.0.0"
  debug: false

firebase:
  credentials_path: "./firebase_credentials.json"
  database_url: "https://powerkeeper-synatec-default-rtdb.firebaseio.com/"
  timeout: 30

analytics:
  anomaly_threshold: 150  # % acima da média
  cache_duration: 3600    # segundos
  
reports:
  default_format: "table"
  date_format: "dd/MM/yyyy"
  decimal_places: 2
  
export:
  default_path: "./exports/"
  compress: true
  include_metadata: true
```

---

## 🔐 Segurança

### Boas Práticas

1. **Nunca commitar credenciais**
   - Use `.gitignore` para excluir `firebase_credentials.json`
   - Use variáveis de ambiente para dados sensíveis

2. **Controle de acesso**
   - Implemente autenticação para comandos críticos
   - Use roles para diferentes níveis de permissão

3. **Logs de auditoria**
   - Registre todas as operações administrativas
   - Mantenha histórico de modificações

4. **Validação de entrada**
   - Sanitize todos os inputs do usuário
   - Valide parâmetros de comandos

---

## 📈 Roadmap

- [ ] **Dashboard Web**: Interface gráfica complementar
- [ ] **API REST**: Exposição de funcionalidades via API
- [ ] **Machine Learning**: Previsão de consumo futuro
- [ ] **Integração Power BI**: Export direto para dashboards
- [ ] **Notificações**: Alertas via email/SMS
- [ ] **Multi-tenant**: Suporte a múltiplas organizações
- [ ] **Modo real-time**: Streaming de dados ao vivo
- [ ] **Plugins**: Sistema de extensões personalizadas

---

## 🐛 Troubleshooting

### Erro de Conexão com Firebase
```
Verificar:
✓ Credenciais corretas em firebase_credentials.json
✓ URL do database correto
✓ Permissões de leitura/escrita no Firebase
✓ Conexão com internet ativa
Comando não encontrado
bash# Verificar que o Dart está no PATH
echo $PATH | grep dart

# Reinstalar dependências
dart pub get
Problemas de Performance
bash# Limpar cache
dart pub cache clean

# Recompilar
dart compile exe bin/powerkeeper.dart -o powerkeeper

🤝 Contribuindo
Este é um projeto acadêmico, mas sugestões são bem-vindas:

Fork o repositório
Crie uma branch para sua feature (git checkout -b feature/MinhaFeature)
Commit suas mudanças (git commit -m 'Adiciona MinhaFeature')
Push para a branch (git push origin feature/MinhaFeature)
Abra um Pull Request


📝 Changelog
v1.0.0 (2025-02-13)

✨ Versão inicial do sistema
📊 Comandos básicos de análise
🔥 Integração com Firebase
📈 Geração de relatórios
🔍 Detecção de anomalias


📄 Licença
Este projeto faz parte do trabalho acadêmico do curso de Ciência da Computação da Unifeob (2025.1 e 2025.2) e foi desenvolvido para fins educacionais.

👨‍💻 Desenvolvedores

Luiz Gustavo
Matteo
Nicolas

Grupo Synatec | Ciência da Computação | Unifeob

🔗 Repositórios Relacionados

PowerKeeper (Repositório Principal)
PowerKeeper IoT (ESP32)
PowerKeeper Database


📚 Documentação Adicional

Guia de Comandos Completo
Arquitetura do Sistema
Guia de Desenvolvimento
FAQ


💡 Dica: Execute dart run bin/powerkeeper.dart --help para ver todos os comandos disponíveis e suas opções.
🔗 Integração: Este módulo trabalha em conjunto com o PowerKeeper IoT para formar o sistema completo de monitoramento energético.


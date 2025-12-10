# RAS - Robô Autônomo de Serviços

Sistema de controle e navegação autônoma para robô omnidirecional de 3 rodas, utilizando câmeras Intel RealSense (D435 e L515), detecção YOLO e interface web em tempo real.

![RAS-Imagem](https://github.com/user-attachments/assets/fb7c15bb-2333-40f6-87b7-962a2bd71497)


## 📋 Pré-requisitos

### Hardware
- Robô omnidirecional com 3 motores DC
- Arduino (Uno, Mega ou compatível)
- Intel RealSense D435 (câmera RGB-D)
- Intel RealSense L515 (LiDAR) - opcional
- Notebook/PC com USB 3.0
- Tablet para exibição de status (opcional)

### Software
- Node.js 18+ e npm
- Python 3.8+
- Arduino IDE
- Driver Intel RealSense SDK 2.0

## 🚀 Instalação

### 1. Clone o repositório

```bash
git clone https://github.com/Robo-Ras/ras.git
cd Robo-Ras
```

### 2. Instale as dependências do Frontend

```bash
npm install
```

### 3. Instale as dependências do Python

```bash
pip install -r backend/requirements.txt
```

### 4. Configure o Arduino

1. Abra o Arduino IDE
2. Carregue o arquivo `arduino_robot_control.ino`
3. Selecione a porta correta (ex: `/dev/ttyUSB0` no Linux)
4. Faça upload para o Arduino


### 5. Instalar Intel RealSense SDK

```bash
# Ubuntu/Debian
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE
sudo add-apt-repository "deb https://librealsense.intel.com/Debian/apt-repo $(lsb_release -cs) main"
sudo apt update
sudo apt install librealsense2-dkms librealsense2-utils
```

## ▶️ Executando o Sistema

### 1. Inicie o servidor web (Frontend)

```bash
npm run dev
```

O servidor iniciará em `http://localhost:5173`

### 2. Inicie o backend Python

Em outro terminal:

```bash
cd backend
python3 robot_autonomous_control.py
```

### 3. Acesse a interface

Abra o navegador e acesse: `http://localhost:5173`

## 🎮 Como Usar

### Conexão com Arduino
1. Conecte o Arduino via USB
2. Na interface web, selecione a porta serial
3. Clique em "Conectar"

### Controle Manual
- **Teclado**: WASD ou setas direcionais
- **Rotação**: Q (anti-horário) / E (horário)
- **Parar**: Espaço
- **Velocidade**: Ajuste pelos sliders

### Navegação Autônoma
1. Configure a velocidade desejada
2. Ative o switch "Navegação Autônoma"
3. O robô navegará evitando obstáculos automaticamente

### Controle por Voz
Comandos reconhecidos em português:
- "frente", "avançar", "pra frente"
- "trás", "voltar", "ré"
- "direita", "esquerda"
- "parar", "pare", "stop"
- "modo autônomo", "modo manual"

## Arquivos por Categoria

### 🐍 Backend Python (Essenciais)
| Arquivo | Função |
|---------|--------|
| `robot_autonomous_control.py` | Servidor WebSocket (porta 8765) + Flask (porta 5000), processamento de câmeras, lógica de navegação |
| `robot_tracking_system.py` | Sistema de tracking com YOLO e Kalman Filter para L515 + D435 |
| `requirements.txt` | Lista de dependências Python |

### 🔌 Arduino (Essencial)
| Arquivo | Função |
|---------|--------|
| `arduino_robot_control.ino` | Recebe comandos via Serial e controla os 3 motores |

### 🌐 Frontend React (Essenciais)
| Pasta/Arquivo | Função |
|---------------|--------|
| `src/pages/Index.tsx` | Dashboard principal de controle |
| `src/pages/TabletStatus.tsx` | Interface do tablet (carinha de emoções) |
| `src/components/DirectionalControl.tsx` | Controle direcional WASD |
| `src/components/MotorSpeedControl.tsx` | Controle de velocidade por motor |
| `src/components/SerialConnectionControl.tsx` | Conexão com Arduino |
| `src/components/CameraStatus.tsx` | Status das câmeras RealSense |
| `src/components/AutonomousControl.tsx` | Controle do modo autônomo |
| `src/components/VoiceControl.tsx` | Controle por voz |
| `src/components/MultiCameraView.tsx` | Visualização multi-câmera |
| `src/components/SensorVisualization.tsx` | Visualização de sensores |

---


## 🔧 Configuração

### Portas e Conexões
| Serviço | Porta |
|---------|-------|
| Frontend (Vite) | 5173 |
| WebSocket (Python) | 8765 |
| API Flask | 5000 |

### Parâmetros de Navegação
Editáveis em `robot_autonomous_control.py`:
- `SAFE_DISTANCE`: Distância mínima de obstáculos (padrão: 0.5m)
- `SCAN_INTERVAL`: Intervalo de varredura (padrão: 2s)
- `SCAN_DURATION`: Duração da rotação de scan (padrão: 0.3s)

## 🧪 Testes

### Teste 1: Conexão Arduino
```bash
# Verifique se a porta está disponível
ls /dev/ttyUSB*
```

### Teste 2: Câmeras RealSense
```bash
python -c "import pyrealsense2 as rs; print(rs.context().devices)"
```

### Teste 3: WebSocket
Inicie o backend e verifique no navegador se o status muda para "Conectado"

## ❗ Solução de Problemas

| Problema | Solução |
|----------|---------|
| Porta serial não aparece | Verifique conexão USB e permissões (`sudo chmod 666 /dev/ttyUSB0`) |
| Câmera não detectada | Reconecte USB 3.0, verifique `realsense-viewer` |
| WebSocket desconectado | Verifique se `robot_autonomous_control.py` está rodando |
| Robô não responde | Verifique alimentação e conexão do Arduino |

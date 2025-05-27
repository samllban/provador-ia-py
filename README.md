# 🧠 Back-end do Provador Virtual com IA e Modelos 3D

Este diretório contém a parte Python do sistema de provador virtual com inteligência artificial, modelagem 3D e simulação de roupas em tempo real.

## 🧰 Tecnologias Utilizadas

- Python 3.10+
- Flask (API REST)
- TensorFlow / MediaPipe / OpenCV
- Hugging Face Transformers / Diffusers
- Trimesh / Open3D / pygltflib
- Firebase (armazenamento de arquivos)
- JAX e JAXlib (otimizações de IA)

## 🔧 Como Executar

```bash
# Recomendado: ativar ambiente virtual
python -m venv venv
source venv/bin/activate  # ou venv\Scripts\activate no Windows

# Instalar as dependências
pip install -r requirements.txt

# Rodar o servidor Flask
python app.py


data/
│
├── raw/                # Dados brutos (imagens, fotos tiradas, 3D scaneado, não processados ainda)
├── processed/          # Dados já limpos, tratados (pronto para treinar modelos, ou para usar)
├── datasets/           # Datasets públicos ou privados (ex: COCO, DeepFashion, ou datasets próprios de escaneamento)
├── qr_codes/           # Imagens ou dados de QR Codes lidos (escaneamento ao vivo)
├── body_profiles/      # Perfis corporais detectados (ex: JSONs ou CSVs com medidas, tipo de corpo, proporções)
├── cloth_profiles/     # Dados das roupas (ex: tamanho, tipo de tecido, modelo 3D adaptado)
├── segmentation_masks/ # Máscaras de segmentação (ex: o corpo da pessoa separado do fundo, partes separadas)
├── 3d_models/          # Modelos 3D capturados ou ajustados (.glb, .obj, .fbx, etc.)
└── temp/               # Dados temporários que podem ser apagados (ex: cache de upload, manipulação rápida)

body_profiles/ → *.json (medidas, ângulos)

segmentation_masks/ → *.png (imagens preto/branco, máscara binária)

cloth_profiles/ → *.json (infos de roupa)

3d_models/ → .glb, .gltf, .obj, .fbx

datasets/ → pode ser .zip, .csv, .json, imagens etc.
#pesquisar como tratar esses dados pra saber onde cada um vai ficar em cada pasta



backend-python/
├── api/                  # Rotas HTTP da aplicação
│   ├── routes/
│   ├── schemas/
│   ├── services/
│   ├── utils/
│   └── __init__.py
│
├── data/                 # Dados brutos enviados pelos usuários
│   ├── qr_codes/
│   ├── raw_images/
│   ├── processed_images/
│   ├── body_measurements/
│   └── temp/             # Arquivos temporários que depois podem ser deletados
│
├── models/               # Modelos de IA treinados
│   ├── pose_estimation/
│   ├── body_segmentation/
│   ├── cloth_fitting/
│   ├── utils/            # Scripts para carregar modelos
│   └── README.md
│
├── src/                  # Código principal (controladores principais)
│   ├── detectors/        # Algoritmos de detecção (pose, QR, corpo)
│   ├── utils/            # Funções utilitárias diversas (não específicas de IA)
│   ├── pipelines/        # (opcional) Fluxos de processamento que combinam etapas
│   └── __init__.py
│
├── static/               # Arquivos estáticos, ex: exemplo de QR code, imagens públicas
│   ├── example_qr/
│   ├── example_body/
│   └── example_clothes/
│
├── main.py               # Arquivo principal para rodar o FastAPI ou Flask app
├── requirements.txt      # Lista de pacotes Python necessários
├── README.md             # Instruções para rodar e entender o projeto
├── .env                  # Variáveis de ambiente (ex: chaves do Firebase)
└── .gitignore            # Arquivos/pastas que o Git deve ignorar



api/
├── routes/
│   ├── __init__.py
│   ├── scan_qr.py           # Rota de escaneamento de QR Code
│   ├── pose_detection.py    # Rota de pose detection (MediaPipe, TensorFlow)
│   ├── body_segmentation.py # Rota de segmentação de corpo
│   ├── cloth_fit.py         # Rota de ajuste de roupa no corpo
│   ├── upload_images.py     # Rota para upload de imagens de corpo
│   └── user_profile.py      # Rota para cadastro/edição de perfil corporal
├── schemas/
│   ├── __init__.py
│   ├── body_measurements.py # Esquema de medidas corporais (altura, busto, etc)
│   ├── qr_code_data.py       # Esquema para dados do QR code
│   ├── image_upload.py       # Validação dos uploads de imagem
│   └── cloth_fit_request.py  # Dados enviados pra ajuste de roupa
├── services/
│   ├── __init__.py
│   ├── pose_service.py      # Funções para lidar com pose
│   ├── segmentation_service.py # Funções de segmentação
│   ├── cloth_fitting_service.py # Lógica de ajuste de roupa
│   └── qr_code_service.py   # Lógica de leitura e processamento de QR
├── utils/
│   ├── __init__.py
│   ├── file_handling.py     # Funções para lidar com arquivos/imagens
│   ├── firebase_service.py  # Funções para salvar no Firebase (Database/Storage)
│   ├── model_loader.py      # Carregar modelos TensorFlow/MediaPipe
│   └── response_format.py   # Padronizar as respostas das APIs
└── __init__.py




src/
├── detectors/        # Algoritmos para detectar pose, QR code, segmentação de corpo
│   ├── pose_detector.py
│   ├── qr_detector.py
│   ├── body_segmenter.py
│   └── cloth_fitter.py
│
├── utils/            # Funções auxiliares (ajuda geral)
│   ├── image_utils.py       # Ex: redimensionar imagem, converter formatos
│   ├── math_utils.py        # Ex: calcular ângulos do corpo
│   ├── firebase_utils.py    # Upload no Firebase
│   └── file_utils.py        # Lidar com arquivos temporários, salvar, deletar
│
├── pipelines/        # Combina vários detectores em fluxos automáticos (NEW!)
│   ├── scan_pipeline.py     # Ex: escaneia QR code + detecta corpo + mede
│   └── fitting_pipeline.py  # Ex: ajusta a roupa virtual no modelo 3D
│
├── services/         # Serviços de processamento de IA (NEW!)
│   ├── measurement_service.py   # Calcula medidas do corpo
│   ├── fitting_service.py       # Ajusta a roupa no avatar
│   └── qr_code_service.py       # Decodifica QR codes e coleta dados
│
└── __init__.py       # Torna a pasta src um módulo Python


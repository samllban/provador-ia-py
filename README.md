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

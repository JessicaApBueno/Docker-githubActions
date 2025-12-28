# 🐳 Docker + GitHub Actions: Automatizando o Push para o Docker Hub

Este projeto demonstra como criar um contêiner Docker extremamente otimizado para uma aplicação em **Go** e automatizar a publicação da imagem no **Docker Hub** sempre que uma nova `tag` de versão é gerada.

## 🚀 Tecnologias Utilizadas
* **Go (Golang)**: Linguagem de programação para o backend.
* **Docker**: Conteinerização utilizando *Multi-stage Build*.
* **GitHub Actions**: Automação da pipeline de CI/CD.
* **Docker Hub**: Registro de imagens de contêiner.

## 📦 Estrutura de Arquivos
* `main.go`: Servidor HTTP simples que exibe uma arte em ASCII de uma baleia.
* `Dockerfile`: Configuração de construção em duas etapas (*builder* e *scratch*) para reduzir o tamanho da imagem.
* `go.mod`: Gerenciamento de módulos e dependências do Go.
* `.github/workflows/docker-push.yml`: Configuração da pipeline de automação.

## 🏗️ Otimização com Multi-stage Build
O `Dockerfile` deste projeto utiliza a estratégia de construção em múltiplas etapas:
1. **Estágio Builder**: Utiliza a imagem oficial `golang:latest` para compilar o binário.
2. **Estágio Final**: Utiliza a imagem `scratch` (vazia), resultando em uma imagem final de aproximadamente **10MB a 15MB**, contendo apenas o binário executável.

## ⚙️ Configuração da Pipeline (GitHub Actions)
A pipeline está configurada para ser disparada apenas quando uma **Tag** (ex: `v1.0.0`) é enviada ao repositório.

### Pré-requisitos
No seu repositório GitHub, em **Settings > Secrets and variables > Actions**, configure as seguintes chaves:
* `DOCKER_HUB_USERNAME`: Seu usuário do Docker Hub (ex: `jessicaapbueno`).
* `DOCKER_HUB_ACCESS_TOKEN`: Token de acesso gerado no painel do Docker Hub.

### Como disparar o deploy
Para gerar uma nova imagem no Docker Hub, siga os comandos no terminal:
```bash
git add .
git commit -m "feat: nova versão da baleia"
git push origin main
git tag v1.0.0
git push origin v1.0.0
```
🖥️ Como rodar localmente

Após o build da imagem, você pode rodar o contêiner localmente com:
Bash
```
docker run -d -p 8080:8080 --name baleia-app jessicaapbueno/baleia-app:latest
```
<img width="1353" height="644" alt="image" src="https://github.com/user-attachments/assets/326aa88a-678e-4e86-8925-0fdeda39d28d" />
<img width="1366" height="373" alt="image" src="https://github.com/user-attachments/assets/db84294c-8f0b-4487-b299-38a72dab19d3" />


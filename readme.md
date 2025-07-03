# Imersão DevOps - Alura Google Cloud (Desafio)

Este projeto é uma API feita com **FastAPI** para gerenciar alunos, cursos e matrículas em uma escola. O projeto não é a parte de programação e sim foco em dev ops

---

## Pré-requisitos

Antes de começar, você precisa ter instalado no seu computador:

- [Python 3.10 ou superior instalado](https://www.python.org/downloads/)
- [Git](https://git-scm.com/downloads)
- [Docker (para rodar a aplicação em containers localmente)](https://www.docker.com/get-started/)
- [Google Cloud SDK (ferramenta `gcloud` para enviar o projeto para a nuvem)](https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe)

---
## Passos para subir o projeto

1. **Faça o download do repositório:**
   [Clique aqui para realizar o download](https://github.com/DurezahGeek/api-docker-ci-gcp/archive/refs/heads/main.zip)

2. **Crie um ambiente virtual:**
   ```sh
   python3 -m venv ./venv
   ```

3. **Ative o ambiente virtual:**
   - No Linux/Mac:
     ```sh
     source venv/bin/activate
     ```
   - No Windows, abra um terminal no modo administrador e execute o comando:
   ```sh
   Set-ExecutionPolicy RemoteSigned
   ```

     ```sh
     venv\Scripts\activate
     ```

4. **Instale as dependências:**
   ```sh
   pip install -r requirements.txt
   ```

5. **Execute a aplicação:**
   ```sh
   uvicorn app:app --reload
   ```

6. **Acesse a documentação interativa:**

   Abra o navegador e acesse:  
   [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

   Aqui você pode testar todos os endpoints da API de forma interativa.

---

## O que é Docker?

Docker é uma ferramenta que cria **containers**, que são ambientes isolados para rodar sua aplicação de forma padronizada, sem se preocupar com o sistema ou configurações do computador onde ela está rodando.

O **Docker Desktop** é um programa que você instala no seu PC para criar, rodar e gerenciar esses containers com interface gráfica e terminal.

---

## Arquivos importantes do Docker no projeto

- **Dockerfile**: Um arquivo com instruções para montar uma "imagem" que representa o ambiente da sua aplicação — sistema, bibliotecas e código prontos para rodar.

- **docker-compose.yml**: Arquivo que ajuda a subir vários containers juntos, configurar portas, volumes e variáveis com um único comando.

- **.dockerignore**: Lista arquivos e pastas que não devem entrar na imagem, para evitar aumentar o tamanho da aplicação.

---

## Passo a passo para rodar o projeto localmente com Docker

1. Tenha o Docker Desktop instalado e aberto no seu computador.

2. Baixe o código do projeto e abra a pasta no terminal.

3. Verifique que seu projeto tem:  
   - `Dockerfile` (com instruções para montar a imagem)  
   - `docker-compose.yml` (para facilitar rodar o container)

4. No terminal, dentro da pasta do projeto, execute:  
   ```bash
   docker-compose up --build

Isso vai construir a imagem e rodar o container da aplicação.

Acesse no navegador:  
[http://localhost:8000/docs](http://localhost:8000/docs)  
para ver a documentação e testar a API.

---

## Subindo o projeto para o GitHub e usando GitHub Actions

1. Faça o commit do seu código local e envie (push) para seu repositório no GitHub.

2. No repositório do GitHub, vá até a aba **Actions**.

3. Configure um workflow (arquivo YAML) que:  
   - Constrói a imagem Docker automaticamente a cada push;  
   - Executa testes automatizados;  
   - Pode enviar a imagem para um registro Docker (Docker Hub, Google Container Registry);  
   - Pode automatizar o deploy da aplicação na nuvem.

4. Ao ativar o GitHub Actions, todo esse processo roda automaticamente nos servidores do GitHub, garantindo integração contínua (CI).

---

## Passo a passo para fazer deploy na nuvem com Google Cloud Run

1. No terminal, faça login na sua conta Google:  
   ```bash
   gcloud auth login
```

2. Defina qual projeto Google Cloud usar:
   ```bash
   gcloud config set project [ID_DO_PROJETO]
```

3. Certifique-se que o Dockerfile está configurado para rodar na porta 8000.

4. Envie a aplicação para o Google Cloud Run com:
   ```bash
  gcloud run deploy --port=8000
```

5. Siga as instruções para escolher região e configurações.

6. Ao final, o Google vai te mostrar uma URL pública onde sua API estará disponível para qualquer um acessar.

## Estrutura do Projeto

- `app.py`: Arquivo principal da aplicação FastAPI.
- `models.py`: Modelos do banco de dados (SQLAlchemy).
- `schemas.py`: Schemas de validação (Pydantic).
- `database.py`: Configuração do banco de dados SQLite.
- `routers/`: Diretório com os arquivos de rotas (alunos, cursos, matrículas).
- `requirements.txt`: Lista de dependências do projeto.

---

- O banco de dados SQLite será criado automaticamente como `escola.db` na primeira execução.
- Para reiniciar o banco, basta apagar o arquivo `escola.db` (isso apagará todos os dados).

---

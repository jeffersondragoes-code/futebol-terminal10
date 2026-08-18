# Futebol Terminal10

MVP de um agregador de notícias de futebol em tempo quase real, inspirado na interface mostrada pelo usuário.

## O que já está pronto

- Feed cronológico.
- Coleta automática a cada intervalo configurável.
- WebSocket para atualizar a tela quando entram notícias.
- Filtros por transferência, escalação, lesão, jogo e urgência.
- Identificação básica do clube.
- Deduplicação por URL.
- SQLite.
- NewsAPI.
- RSS configurável.
- Classificação local por palavras-chave.
- Classificação opcional com OpenAI.
- Docker.

## Rodar localmente

Python 3.12+:

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# Linux/macOS
source .venv/bin/activate

pip install -r requirements.txt
cp .env.example .env
uvicorn app.main:app --reload
```

Abra http://localhost:8000

## NewsAPI

Crie uma chave no NewsAPI e coloque no `.env`:

NEWSAPI_KEY=sua_chave

O projeto usa o endpoint `/v2/everything` e depois aplica o filtro de futebol.

## RSS

Adicione feeds autorizados:

RSS_FEEDS=https://exemplo.com/feed.xml,https://outro.com/rss

## IA

Opcional:

OPENAI_API_KEY=sua_chave
OPENAI_MODEL=gpt-5.6-luna

Sem chave da OpenAI, a classificação local continua funcionando.

## Docker

```bash
cp .env.example .env
# edite .env
docker compose up -d --build
```

Abra http://localhost:8000

## Arquitetura

Fonte -> coletor -> filtro -> deduplicação -> IA -> SQLite -> API -> WebSocket -> navegador

## Produção

Para uma versão comercial, recomendo PostgreSQL + Redis, autenticação de administrador, fila de processamento, logs, métricas, notificações e APIs esportivas/licenciadas.

Mostre título/resumo curto e link para a matéria original em vez de republicar o texto integral.

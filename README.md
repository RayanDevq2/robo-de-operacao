# Vagas de edição de vídeo

Site estático que mostra vagas de editor de vídeo / motion (Brasil e internacional), atualizado todo dia às 06:00 (Brasília).

## Como publicar (grátis)

1. Crie um repositório no GitHub e envie esta pasta inteira (inclusive `.github/`).
2. Em **Settings → Pages**, escolha a branch `main` e a pasta `/ (root)`.
3. Em **Actions**, abra "Atualizar vagas" e clique em **Run workflow** para a primeira coleta.
4. (Recomendado para mais vagas no Brasil) Crie uma conta grátis em developer.adzuna.com e adicione os secrets `ADZUNA_APP_ID` e `ADZUNA_APP_KEY` em **Settings → Secrets and variables → Actions**.

## Testar localmente

```
pip install requests
python scripts/fetch_jobs.py
python -m http.server 8000
```

Abra http://localhost:8000.

## Fontes

Gupy (Brasil), Remotive, RemoteOK, Jobicy, Arbeitnow (sem chave) e Adzuna (com chave, cobre Brasil, EUA, Reino Unido, Canadá e Austrália). Para adicionar outra fonte, crie uma função em `scripts/fetch_jobs.py` que devolva vagas com `job(...)` e inclua na lista em `main()`.

## Vaga do dia escolhida por IA

Depois de cada coleta, o script envia as 40 vagas mais recentes para o Claude, que escolhe a melhor para um editor que mora no Brasil e explica o motivo em duas frases. A vaga aparece em destaque no topo do site.

1. Crie uma chave em console.anthropic.com (a API é cobrada à parte da assinatura do Claude.ai; uma chamada por dia custa muito pouco).
2. No repositório, em **Settings → Secrets and variables → Actions**, crie o secret `ANTHROPIC_API_KEY`.

Sem a chave, o site escolhe a vaga do dia por uma regra simples e avisa isso no destaque. Para trocar o modelo, defina a variável `ANTHROPIC_MODEL` no workflow.

Cada vaga agora também recebe um nicho (anúncios, redes sociais, motion, podcast, agência e outros), com filtro no site.

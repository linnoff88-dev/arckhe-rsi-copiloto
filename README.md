# RSI Copiloto

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

[![RSI Copiloto](guia/assets/banner.jpg)](https://inematds.github.io/rsi-copiloto/guia/)

Assistente local com IA, memÃ³ria, tarefas e ciclos de melhoria supervisionada para pessoas fÃ­sicas, profissionais independentes e pequenas empresas. **Projeto separado da [pesquisa RSI](https://inematds.github.io/rsi/guia/)**.

**[Experimentar demonstraÃ§Ã£o](https://inematds.github.io/rsi-copiloto/app/)** Â· **[Guia de uso](https://inematds.github.io/rsi-copiloto/guia/)**

A demonstraÃ§Ã£o usa exemplos programados e armazenamento do navegador. A versÃ£o local chama IA real via OpenRouter e persiste dados em SQLite. A demonstraÃ§Ã£o agora oferece interface PT/EN/ES; o guia e o README tambÃ©m estÃ£o traduzidos.

## Rodar

Python 3.11+ e Git. Sem dependÃªncias Python adicionais.

```bash
git clone https://github.com/inematds/rsi-copiloto.git
cd rsi-copiloto
python3 -m rsi.server
```

Abra **http://127.0.0.1:8765/app/**. O servidor atende somente em loopback; uso individual.

A credencial `OPENROUTER_API_KEY` Ã© lida do ambiente ou do arquivo apontado por `RSI_ENV_FILE`. Na mÃ¡quina do autor, tambÃ©m procura `~/projetos/openpcbotv2/.env` e `~/projetos/wifi/.env`. NÃ£o copie chaves para este repositÃ³rio.

```bash
RSI_ENV_FILE="$HOME/.config/minhas-credenciais.env" python3 -m rsi.server
```

O arquivo indicado precisa conter `OPENROUTER_API_KEY`. ConfiguraÃ§Ã£o opcional: `RSI_MODEL` (padrÃ£o `openai/gpt-5.4-nano`), `RSI_DAILY_CALLS` (50 tentativas/dia UTC), `RSI_DB`, `--port`, `--db`, `--no-scheduler`. AtÃ© 2.400 tokens de saÃ­da por chamada. Limite de chamadas nÃ£o equivale a teto financeiro.

## O que funciona

- TrÃªs espaÃ§os: pessoal, autÃ´nomo e pequena empresa; nove rotinas prontas.
- Entregas com lacunas, fontes de memÃ³ria, prÃ³ximos passos, tokens e custo informado.
- Tarefas, conhecimento por perfil e contexto recuperado por palavras.
- Feedback, proposta de instruÃ§Ã£o, comparaÃ§Ã£o atual/candidata em trÃªs casos, revisÃ£o humana, promoÃ§Ã£o e reversÃ£o.
- Rotinas diÃ¡rias opcionais com servidor aberto; falha pausa a rotina.
- HistÃ³rico, backup JSON/restauraÃ§Ã£o, tarefas CSV e calendÃ¡rio `.ics`.

O ciclo melhora instruÃ§Ãµes e processos, **nÃ£o os pesos do modelo**. Os checks sÃ£o estruturais, nÃ£o provam verdade ou ganho de negÃ³cio. A instruÃ§Ã£o ativa vale para os trÃªs espaÃ§os. A IA nÃ£o envia mensagens, movimenta dinheiro nem executa comandos. IntegraÃ§Ãµes externas e mÃºltiplos usuÃ¡rios sÃ£o etapas futuras.

## Dados

SQLite em `~/.local/share/rsi-copiloto/state.sqlite3`, fora do diretÃ³rio publicado. A API recebe demanda, perfil, instruÃ§Ã£o e atÃ© cinco memÃ³rias relevantes. Backup contÃ©m dados dos trÃªs espaÃ§os: mantenha-o privado. Importar pausa recorrÃªncias e exige nova avaliaÃ§Ã£o antes de promover instruÃ§Ãµes; o limite diÃ¡rio de uso local Ã© preservado.

## Verificar

```bash
python3 -m unittest discover -s tests -v
# Opcional: teste real pago, atÃ© oito chamadas, somente dados fictÃ­cios.
python3 -m scripts.smoke_live
```

[Plano](docs/PLANO-IMPLEMENTACAO.md) Â· [OperaÃ§Ã£o](docs/OPERACAO.md) Â· [ValidaÃ§Ã£o](docs/VALIDACAO.md) Â· [Changelog](CHANGELOG.md)

Projeto aberto e gratuito de pesquisa e educaÃ§Ã£o do [INEMA.CLUB](https://inema.club).

## MissÃ£o e LOOP-R: dois ciclos conectados.

VocÃª define a missÃ£o. A IA propÃµe de uma a cinco etapas. Confira o plano e clique em â€œAprovar plano e executar primeira etapaâ€. A entrega aparece na mesma missÃ£o, aguardando sua avaliaÃ§Ã£o.

Clique em â€œAprovar e executar prÃ³xima etapaâ€ para o copiloto continuar usando a entrega e sua avaliaÃ§Ã£o. â€œCorrigir esta etapaâ€ refaz o trabalho atual. VocÃª tambÃ©m pode pausar, recarregar a pÃ¡gina e retomar. Salvar na memÃ³ria Ã© opcional: o histÃ³rico da missÃ£o jÃ¡ Ã© preservado.

**Executar â†’ Medir â†’ Criticar â†’ Propor â†’ Testar â†’ Validar â†’ Promover â†’ Repetir**

Ao concluir, veja sua nota mÃ©dia e a quantidade de correÃ§Ãµes. Clique em â€œIniciar LOOP-R desta missÃ£oâ€. A IA recebe essas evidÃªncias, critica as falhas e propÃµe uma instruÃ§Ã£o candidata. No laboratÃ³rio, compare atual e candidata, leia as respostas, registre seu parecer e sÃ³ entÃ£o promova.

Novas missÃµes usam a instruÃ§Ã£o promovida. MissÃµes jÃ¡ iniciadas mantÃªm sua versÃ£o. Ã‰ evoluÃ§Ã£o supervisionada de instruÃ§Ãµes e procedimentos, sem treino dos pesos do modelo. Os trÃªs testes gerais verificam estrutura; nÃ£o comprovam ganho de qualidade ou resultado financeiro.

Na demonstraÃ§Ã£o pÃºblica, as entregas sÃ£o exemplos programados. O fluxo completo funciona; para executar o conteÃºdo da sua missÃ£o com IA, use a versÃ£o local.

---

Projeto adaptado da comunidade INEMA TDS - Marca Arckhe
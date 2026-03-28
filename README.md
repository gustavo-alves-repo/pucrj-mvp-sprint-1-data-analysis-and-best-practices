# MVP — Sprint 01 - Análise Exploratória e Boas Práticas - Fatores pré-jogo associados à vitória das **BRANCAS** em partidas do Chess.com

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/gustavo-alves-repo/pucrj-mvp-sprint-1-data-analysis-and-best-practices/blob/main/mvp_sprint_1_data_analysis_and_best_practices.ipynb)

**Autor:** Gustavo Alves  
**Matrícula:** 4052025001911  
**Notebook principal:** [mvp_sprint_1_data_analysis_and_best_practices.ipynb](https://colab.research.google.com/github/gustavo-alves-repo/pucrj-mvp-sprint-1-data-analysis-and-best-practices/blob/main/mvp_sprint_1_data_analysis_and_best_practices.ipynb)

## Objetivo

Analisar **fatores pré-jogo** associados à vitória das **BRANCAS** em partidas de xadrez, estruturando os dados de forma consistente e preparada para análises futuras.

## Dados

- **Fonte:** [Chess Game Dataset (Kaggle)](https://www.kaggle.com/datasets/adityajha1504/chesscom-user-games-60000-games)  
- Trabalho com ~60k jogos públicos do Chess.com (EN-US), textos do notebook em PT-BR.  
- Para execução reprodutível, o CSV é lido diretamente de um link do GitHub.

## Escopo & formulação

- **Tarefa conceitual:** Classificação **binária** (win vs not_win).
- **Positiva (1):** win (vitória das BRANCAS).  
- **Negativa (0):** not_win (empate ou derrota das BRANCAS).
- **Variáveis analisadas:** `rating_diff`, `rated` (0/1), `time_class` (`bullet`, `blitz`, `rapid`, `daily`).
- **Filtros:** apenas `rules == 'chess'` (xadrez clássico).

## Etapas do notebook

1. **Definição do problema** — escopo, objetivo, tipo de tarefa, premissas e hipóteses.
2. **Carga e qualidade dos dados** — leitura com tipagem explícita, verificação de nulos, shape e memória.
3. **Análise exploratória (EDA):**
   - Distribuição de resultados (`white_result` / `black_result`).
   - Distribuição por classe de tempo (`time_class`).
   - Histogramas de `white_rating`, `black_rating` e `rating_diff`.
   - Win rate das BRANCAS por faixa de `rating_diff`.
   - Distribuição do alvo binário (`target_bin`) — análise de balanceamento.
   - Win rate das BRANCAS por `time_class` — análise combinada.
   - Heatmap de correlação entre variáveis numéricas pré-jogo.
4. **Pré-processamento:**
   - Filtragem (`rules == 'chess'`).
   - Mapeamento de `white_result` → `white_outcome` (win / not_win).
   - Criação de `rating_diff` e `target_bin`.
   - One-hot encoding de `time_class` via `pd.get_dummies`.

## Principais achados

- **`rating_diff` é o fator mais relevante:** win rate sobe de ~15–20% (faixa ≤ −200) para ~80–85% (faixa ≥ +200).
- **Balanceamento natural:** ~50% win vs ~50% not_win — não exige reamostragem.
- **`time_class` influencia o resultado:** o win rate das brancas varia entre os ritmos de jogo.
- **`rated` tem correlação próxima de zero** com o resultado.

## Como reproduzir

### Opção A — Google Colab

1. Abra o notebook `mvp_sprint_1_data_analysis_and_best_practices.ipynb` no Colab.  
2. Execute **Runtime → Run all**.  
3. O dataset é lido via URL do meu GitHub público; não precisa configurar nada.

### Opção B — Local (ex.: VS Code)

```bash
python -m venv .venv
source .venv/Scripts/activate  # Mac: .venv/bin/activate
pip install -r requirements.txt
jupyter notebook  # ou jupyter lab
```
# Árvore de Decisão (Decision Tree)

> Parte do repositório de estudos de IA • Atualizado em 20/08/2025

## O que é
Uma **árvore de decisão** é um modelo de *aprendizado supervisionado* que faz previsões ao **dividir recursivamente** o espaço de atributos em regiões cada vez mais homogêneas.  
Cada **nó interno** contém uma regra de decisão (ex.: `petal_length <= 2.45`), e cada **folha** traz uma **classe** (classificação) ou um **valor** (regressão).

## Como decide os cortes?
O algoritmo escolhe, a cada passo, o atributo e o limiar que **maximizam a pureza** das folhas:
- **Classificação:** critérios mais comuns são **Gini** (`criterion="gini"`) e **Entropia** (`criterion="entropy"`).
- **Regressão:** usa-se **mse**/**friedman_mse** (variância) como medida de impureza.

O ganho de informação mede **o quanto a incerteza diminui** após um corte.

## Principais hiperparâmetros (sklearn)
- `max_depth`: **profundidade máxima** da árvore. Quanto maior, mais risco de **overfitting**.
- `min_samples_split`: mínimo de amostras para **dividir** um nó.
- `min_samples_leaf`: mínimo de amostras em **cada folha**.
- `max_leaf_nodes`: número máximo de **folhas**.
- `criterion`: métrica de impureza (**gini**, **entropy**).
- `splitter`: **best** (padrão) ou **random**.
- `class_weight`: útil para **desbalanceamento** de classes.
- `ccp_alpha`: **poda por complexidade mínima** (*cost-complexity pruning*). Valores maiores ⇒ árvores mais simples.

## Vantagens
- Fácil de **interpretar** e **visualizar**.
- Pouco ou nenhum **pré-processamento**; **não** exige padronização de escalas.
- Captura **interações não-lineares** entre atributos.
- Produz **importância de atributos**.

## Desvantagens
- Tende a **overfitting** se não for podada.
- Pode ser **instável** (pequenas variações nos dados mudam a árvore).
- Geralmente tem **menor acurácia** que comitês como **Random Forest**/ **Gradient Boosting**.

## Boas práticas
- **Controle a complexidade** com `max_depth`, `min_samples_leaf`, `ccp_alpha`.
- Use **validação cruzada** e/ou um **conjunto de validação**.
- Para **categóricas**, faça **one-hot encoding** (o `sklearn` não divide por rótulos nativamente).
- Em **classes desbalanceadas**, avalie **AUC, F1, recall** e/ou ajuste `class_weight`.
- **Explique** a solução com: visualização da árvore (`plot_tree`) e **importância de atributos**.

## Métricas comuns
- **Classificação:** acurácia, precision/recall/F1, matriz de confusão, AUC-ROC.
- **Regressão:** RMSE, MAE, R².

## Exemplo prático (Colab)
Use o notebook abaixo (inclui comentários linha a linha, visualização e tuning rápido de `max_depth`):
- **Notebook:** `DecisionTree_Exemplo.ipynb` (suba para o Google Colab ou mantenha em `notebooks/` do seu repositório).

## Referências rápidas
- `sklearn.tree.DecisionTreeClassifier`
- `sklearn.tree.plot_tree`
- `sklearn.model_selection.train_test_split`, `GridSearchCV`
- `sklearn.metrics.classification_report`, `confusion_matrix`

---

### Checklist para provas/entrevistas
- Diferença entre **Gini** e **Entropia**.
- **Poda**: *pré-poda* (limitar profundidade/folhas) vs *pós-poda* (`ccp_alpha`).
- Como lidar com **overfitting** e **desbalanceamento** de classes.
- Interpretabilidade: **regras** + **importância de atributos**.
- Quando preferir **árvores** vs **florestas**/**boosting**.

> Dica: após dominar a árvore simples, avance para **Random Forest** e **Gradient Boosting** para melhor performance.
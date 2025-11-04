# Case iFood – CRM Estruturante (BI/Analytics)

Este repositório contém a solução completa do case técnico: construção de base de engajamento multicanal, análise por clusters de merchants, KPIs gerenciais e um modelo de propensão à conversão (IA/ML).

## Como executar

### Opção A) Databricks (recomendado)
1. Crie um workspace na Databricks Community Edition.
2. Importe os notebooks da pasta `notebooks/` (File → Import → Upload).
3. (Se necessário) Faça upload das bases em **Catalog/Volumes** ou **DBFS**.
4. Execute os notebooks na ordem:
   - `01_missao1_base_engajamento`
   - `02_missao2_crm_analise_cluster`
   - `03_missao3_kpis_storytelling`
   - `04_missao4_propensao_conversao`
5. Os artefatos (tabelas Delta temporárias/views) são criados automaticamente pelos notebooks.

### Opção B) Local (PySpark)
> **Demonstração** (para rodar alguns passos localmente com dados de exemplo).
1. `python -m venv .venv && source .venv/bin/activate` (Windows: `.\.venv\Scripts\activate`)
2. `pip install -r requirements.txt`
3. Execute os scripts de exemplo (diferencial):
   - `python src/etl/etl_base_engajamento.py`
   - `python src/ml/treinar_propensao.py`

### Requisitos
- Python 3.10+
- PySpark 3.5+, pandas, matplotlib
- (Databricks CE ou runtime compatível)

## Estrutura dos Notebooks

1. **Missão 1 – Base de Engajamento**  
   Cria `base_engajamento_canais` unificando WhatsApp/Email, padroniza funil e calcula custos.

2. **Missão 2 – Enriquecimento e Clusters**  
   Cria `crm_analise_cluster` juntando engajamento + `cluster_merchant_history` + `merchant_info`.

3. **Missão 3 – KPIs e Storytelling**  
   Cria a view `kpis_crm_b2b` (taxas, custos, eficiência por canal/cluster).  
   Apresentação em `reports/apresentacao_case_ifood.pdf`.

4. **Missão 4 – IA/ML (Propensão)**  
   Monta a base rotulada com `flag_converteu`, treina **Logistic Regression** e gera probabilidades.

## Entregáveis (checklist)

- [x] **Notebooks** (obrigatório) em `notebooks/`
- [x] **Relatório/Apresentação PDF** (obrigatório) em `reports/`
  - Conclusões e sugestões claras
  - Storytelling dos principais insights
- [ ] **Arquitetura** (diferencial) em `diagrams/`
- [ ] **Pipeline PySpark** (diferencial) em `src/`  
  (exemplo mínimo de ETL e treino ML com dados dummy)

## Principais Insights (resumo)
- **E-mail**: altíssimo alcance e custo muito baixo por envio; taxas de entrega ~97–98%.  
- **WhatsApp**: custo elevado por envio, porém engajamento superior (entrega/visualização >95%).  
- **Estratégia**: usar **E-mail** para escala e **WhatsApp** para ativação/relacionamento e reativação de clusters críticos (pré-churn/churn).  
- **IA/ML**: modelo de propensão identifica parceiros com maior chance de conversão — base para priorização de disparos e redução de custo.

## Como exportar a apresentação
1. No Databricks, gere os gráficos/tabelas no notebook 03 e 04.
2. Monte os slides (Google Slides/PowerPoint/Canva) com:
   - Problema → Abordagem → Resultados → Recomendações
3. Exporte para **PDF** e salve em `reports/apresentacao_case_ifood.pdf`.

## Licença
MIT (ou a que preferir).

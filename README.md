# IC 2026 — Modelagem e Quantificação do Agente Causal

**Iniciação Científica em Computação Quântica e Sistemas Quânticos Abertos**  
**Pesquisador:** Daniel Santos Baptista · **Início:** fevereiro de 2026  
**Escopo:** modelagem física, simulação de um qubit, identificabilidade causal, reversibilidade e quantificação informacional.

[![Testes científicos](https://github.com/DanielBaptista01/IC-Computacao_Cientifica/actions/workflows/tests.yml/badge.svg?branch=main)](https://github.com/DanielBaptista01/IC-Computacao_Cientifica/actions/workflows/tests.yml)
[![Versão científica](https://img.shields.io/badge/release-ic--2026--final--v2-blue)](https://github.com/DanielBaptista01/IC-Computacao_Cientifica/releases/tag/ic-2026-final-v2)
![Estado](https://img.shields.io/badge/ML%2FQML-n%C3%A3o%20treinado-lightgrey)

> **Questão de pesquisa:** até que ponto fontes ou mecanismos físicos específicos que perturbam um qubit podem ser individualizados matematicamente a partir de suas dinâmicas, parâmetros e observações — e quando diferentes fontes se tornam indistinguíveis no sistema reduzido?

**Comece aqui:** [visão científica](#1-visão-geral-científica) · [resultados](#3-resultados-e-evidências) · [reprodução](#5-instalação-e-reprodução) · [limitações](#7-limitações-e-status-epistemológico) · [release oficial](https://github.com/DanielBaptista01/IC-Computacao_Cientifica/releases/tag/ic-2026-final-v2)

## Resumo executivo

Esta pesquisa investiga uma **caracterização operacional de fontes de perturbação quântica**, denominadas *Agentes Causais* na formulação autoral da IC. O ambiente **não é eliminado** da teoria: sua descrição em sistemas quânticos abertos é preservada, enquanto a pesquisa procura decompor mecanismos físicos identificáveis e associá-los a modelos de interação, transformações reduzidas, parâmetros e assinaturas observáveis.

A implementação contém uma biblioteca científica modular, testes automatizados, experimentos controlados de reversibilidade, uma **Transformação Causal Latente** entre operações programadas e dois conjuntos de dados versionados: um **baseline mecanístico v1 com 35.154 registros** e uma **expansão físico-causal v2 com 45.920 registros**, ambos obtidos por simulação. A pesquisa testa identificabilidade **condicional**: há condições distinguíveis e condições de colisão de assinaturas. Nenhuma unicidade universal é pressuposta.

A **versão científica congelada de referência** é [`ic-2026-final-v2`](https://github.com/DanielBaptista01/IC-Computacao_Cientifica/releases/tag/ic-2026-final-v2), no commit [`ca4ee8b`](https://github.com/DanielBaptista01/IC-Computacao_Cientifica/commit/ca4ee8b00aea8d450c7219bd9782b732bf966856). Atualizações editoriais posteriores na `main` **não alteram a release congelada**.

## 1. Visão geral científica

### 1.1 Problema e hipótese autoral

Na descrição de sistemas quânticos abertos, a evolução conjunta sistema–ambiente pode ser unitária, embora a dinâmica do sistema reduzido não seja. Um canal quântico efetivo descreve o que ocorreu ao qubit, mas **não identifica necessariamente a fonte física** que o produziu.

A proposta autoral denomina **Agente Causal** a fonte ou mecanismo específico responsável por uma interação. Seu objetivo não é renomear canais como fontes, mas estabelecer uma trilha rastreável:

$$
\underbrace{A_k}_{\text{fonte/mecanismo}}
\longrightarrow H_{\mathrm{int}}^{(k)}
\longrightarrow \mathcal E_k(t)
\longrightarrow \rho_k(t)
\longrightarrow \Sigma_k
\longrightarrow R_k.
$$

- **`A_k`:** hipótese de origem/mecanismo físico da perturbação;
- **`H_{\mathrm{int}}^{(k)}`:** Hamiltoniano ou outro modelo de interação, quando aplicável;
- **`\mathcal E_k`:** transformação quântica efetiva sobre o sistema;
- **`\rho_k`:** estado resultante;
- **`\Sigma_k`:** assinatura baseada em observáveis, dinâmica e métricas;
- **`R_k`:** diagnóstico da reversibilidade/recuperabilidade **na condição estudada**, não atributo absoluto da fonte.

**Distinção central:** agente ≠ mecanismo de interação ≠ canal efetivo ≠ ruído observado ≠ entropia.

### 1.2 Transformação Causal Latente

A implementação também investiga evoluções físicas não programadas entre profundidades de um circuito:

$$
G_d \;\longrightarrow\; \mathcal C_{k,d} \;\longrightarrow\; G_{d+1}.
$$

A `\mathcal C_{k,d}` não é presumida como porta unitária: pode ser identidade, transformação unitária, canal CPTP/Kraus ou outro modelo justificado. A expressão é uma **abstração de modelagem**, não evidência de que toda interação real seja diretamente observável ou separável em intervalos independentes.

### 1.3 Perguntas avaliadas

1. Fontes fisicamente distintas podem produzir o **mesmo canal reduzido**?
2. Que combinações de estados de prova, tempos e parâmetros tornam duas interações distinguíveis?
3. Uma alteração de fidelidade implica decoerência? **Não necessariamente.**
4. Quando existe inversão unitária, inversa apenas linear ou impossibilidade de inversa CPTP universal?
5. Que informação operacional poderá, futuramente, sustentar estratégias adaptativas de mitigação ou recuperação?

O código implementa e testa **modelos e protocolos específicos**. Não demonstra que toda fonte física real seja unicamente identificável.

## 2. Linha de desenvolvimento e conjuntos de dados

| Marco | Escopo | Registro de referência |
| --- | --- | --- |
| Fundamentos e controles | Estados de um qubit, dinâmica unitária, Kraus, traço parcial, métricas, reversibilidade e experimento inter-depth | [Mapeamento matemático](docs/MATHEMATICAL_MAPPING.md) · [Experimento inicial](results/first_experiment.csv) |
| Dataset 001 | Coleta preliminar em escala e verificações de qualidade | [Resultados preliminares](docs/FIRST_SCALED_DATASET_RESULTS.md) |
| **Baseline mecanístico v1** | **4 famílias**, 14 estados de prova, 81 tempos, **35.154 amostras** | [Resumo v1](results/final/FINAL_SUMMARY.json) · [Evidências](results/final/evidence/) |
| **Expansão físico-causal v2** | **8 famílias**, 80 pontos paramétricos, 14 estados de prova, 41 tempos, **45.920 amostras** | [Auditoria de mecanismos](docs/PHYSICAL_CAUSAL_AGENTS_AUDIT.md) · [Release v2](https://github.com/DanielBaptista01/IC-Computacao_Cientifica/releases/tag/ic-2026-final-v2) |
| **Freeze científico** | Tag imutável como referência metodológica da versão consolidada | [`ic-2026-final-v2`](https://github.com/DanielBaptista01/IC-Computacao_Cientifica/releases/tag/ic-2026-final-v2) |

O v1 e o v2 são **experimentos distintos**, não números a serem somados como se fossem um único dataset. O Dataset 001 é histórico/preliminar. A `main` incorpora o desenvolvimento científico dos PRs anteriores; a release preserva o estado oficial usado para rastreabilidade.

### 2.1 Famílias do baseline v1

1. `coherent-longitudinal-detuning` — perturbação longitudinal unitária;
2. `finite-two-level-exchange-relaxation` — troca de excitação com grau de liberdade finito;
3. `finite-mode-spin-boson-dephasing` — banho bosônico térmico finito;
4. `markovian-photon-reservoir-decay` — reservatório fotônico Markoviano de temperatura nula.

### 2.2 Famílias da expansão físico-causal v2

| Família implementada | Mecanismo modelado |
| --- | --- |
| `external-magnetic-field-wave` | Campo magnético externo, dinâmica Zeeman e ensemble quasistático |
| `external-electromagnetic-rabi-drive` | Excitação eletromagnética coerente com taxa efetiva de Rabi |
| `finite-mode-spin-boson-dephasing` | Banho bosônico térmico finito |
| `thermal-photon-reservoir` | Emissão/absorção em reservatório fotônico a `T=0` e `T>0` |
| `mechanical-phonon-mode` | Troca de excitação com modo mecânico/acústico quantizado |
| `single-mode-mechanical-phonon-dephasing` | Acoplamento vibracional longitudinal e recorrência |
| `ionizing-radiation-quasiparticle-burst` | Dinâmica pós-impacto de quasipartículas; **ponte de deposição fenomenológica** |
| `bistable-charge-fluctuator-rtn` | Defeito/flutuador de carga biestável, *random-telegraph noise* |

Essas famílias são modelos físicos declarados em domínios de validade específicos, **não medições de fontes reais**. O antigo modelo de decaimento fotônico a `T=0` do v1 não é contado novamente como identidade causal independente na v2.

## 3. Resultados e evidências

### 3.1 Identificabilidade condicional

A análise do v1 compara os seis pares de famílias em estados, tempos e combinações paramétricas. Segundo o protocolo e a tolerância definidos, foram registradas **748 condições de colisão de assinaturas** — o que **não** significa 748 fontes iguais, nem prova não-identificabilidade em todos os protocolos.

Em um controle específico, o modelo de troca finita e o reservatório fotônico Markoviano foram parametrizados para produzir o mesmo canal reduzido de *amplitude damping*, com diferença numérica máxima entre saídas de aproximadamente `2,22 × 10⁻¹⁶`. Na v2, um exemplo análogo compara dephasing por mecanismos diferentes em um instante selecionado.

$$
\mathcal E_{A_i}=\mathcal E_{A_j}
\;\not\Rightarrow\;
A_i=A_j.
$$

Isso evidencia uma **limitação de identificabilidade** no nível observado e motiva o uso de informação temporal e múltiplos estados de prova. A v2 avalia os **28 pares** possíveis entre suas oito famílias e uma assinatura operacional de processo obtida com quatro estados linearmente independentes. A distância operacional RMS usada **não é distância diamond**.

**Evidências:** [análise de identificabilidade v1](results/final/evidence/FINAL_IDENTIFIABILITY_ANALYSIS.md) · [auditoria v2](docs/PHYSICAL_CAUSAL_AGENTS_AUDIT.md)

![Matriz de frações de colisão sob o protocolo do v1](results/final/figures/identifiability_collision_fraction_matrix.png)

*Frações de condições com assinaturas próximas segundo o critério numérico do v1. A figura depende do conjunto de estados, tempos, parâmetros e tolerâncias selecionados.*

### 3.2 Agente, ruído e entropia

Uma perturbação pode alterar o estado sem alterar sua entropia. No controle unitário do v1, o maior `|\Delta S|` registrado foi da ordem de `8,01 × 10⁻¹⁶`, embora a distância de traço relativa à entrada alcançasse `1` em condições simuladas.

$$
\Delta S=0
\;\not\Rightarrow\;
\text{ausência de perturbação}.
$$

A caracterização utiliza entropia de von Neumann, pureza, coerência `\ell_1` na base computacional, fidelidade, distância de traço e descritores de estado/processo, conforme o experimento. **Métricas isoladas não identificam a fonte causal.**

**Evidências:** [resultados científicos v1](results/final/evidence/FINAL_SCIENTIFIC_RESULTS.md) · [tabela Agente–Ruído–Entropia](results/final/tables/agent_noise_entropy_summary.csv)

### 3.3 Reversibilidade e dinâmica aberta

$$
\mathcal E(\rho)=U\rho U^\dagger
\quad\Longrightarrow\quad
\mathcal E^{-1}(\rho')=U^\dagger\rho' U
$$

para uma transformação unitária conhecida. No caso geral, distinguem-se **invertibilidade linear**, **existência de inversa CPTP** e **recuperação condicionada/estruturada**. A evolução global unitária sistema+ambiente não garante uma porta inversa operando apenas sobre o qubit reduzido.

A classificação depende de `(\boldsymbol\theta,t)` e das condições de acesso ao sistema, não é um rótulo invariável do agente.

**Evidências:** [reversibilidade v1](results/final/evidence/FINAL_REVERSIBILITY_ANALYSIS.md) · [formalismo/código](docs/MATHEMATICAL_MAPPING.md)

![Distribuição de classificações de reversibilidade no corpus v1](results/final/figures/reversibility_distribution.png)

*Distribuição no protocolo e nas condições amostradas do baseline v1; não representa todas as interações possíveis de cada família física.*

## 4. Organização do repositório

```text
src/ic_quantum/
├── core/          estados, operadores e validação
├── agents/        representações e modelos de Agentes Causais
├── channels/      operações unitárias e canais de Kraus
├── dynamics/      evolução, traço parcial e transformação latente
├── metrics/       entropia, pureza, fidelidade e coerência
├── analysis/      identificabilidade e reversibilidade
├── experiments/   execução dos protocolos e pipelines
└── data/          schemas, registros e exportação

experiments/configs/   configurações dos experimentos
tests/                 testes científicos automatizados
docs/                  fundamentação, protocolos e auditorias
results/final/         dataset v1, figuras, tabelas e evidências
.github/workflows/     validação e publicação de releases
```

O formalismo é implementado explicitamente com álgebra matricial NumPy/SciPy; não depende exclusivamente de uma API de circuitos. O código inclui verificações de Hermiticidade, estados densidade, unitariedade, completude de Kraus, propriedades CPTP, limites analíticos e equivalência sistema global/reduzido.

Consulte [`docs/MATHEMATICAL_MAPPING.md`](docs/MATHEMATICAL_MAPPING.md) para a correspondência formalismo → implementação.

## 5. Instalação e reprodução

**Requisitos:** Python ≥ 3.11, Git e as dependências declaradas no `pyproject.toml`.

```bash
git clone https://github.com/DanielBaptista01/IC-Computacao_Cientifica.git
cd IC-Computacao_Cientifica
python -m venv .venv
```

Ative o ambiente virtual:

- Linux/macOS: `source .venv/bin/activate`
- Windows PowerShell: `.venv\Scripts\Activate.ps1`

Para reproduzir o conjunto fixado de dependências, conforme `requirements-lock.txt`:

```bash
python -m pip install -r requirements-lock.txt
python -m pip install -e . --no-deps
pytest
```

**Reproduzir os experimentos e conjuntos de dados:**

```bash
# Transformação Causal Latente em circuito mínimo
ic-interdepth-experiment --output-dir results/interdepth

# Baseline mecanístico v1
ic-finalize --config experiments/configs/ic_causal_agents_final_v1.json --output-dir results/final

# Expansão físico-causal v2
ic-physical-v2 --config experiments/configs/ic_causal_agents_physical_v2.json --output-dir results/physical_v2
```

A geração incorpora validações matemáticas e registra metadados, configurações, proveniência e hashes dos arquivos produzidos. **A execução em hardware real não faz parte deste corpus.**

### Arquivos e versões para citação

- **Código e resultados congelados:** [release `ic-2026-final-v2`](https://github.com/DanielBaptista01/IC-Computacao_Cientifica/releases/tag/ic-2026-final-v2).
- **Metadados e integridade v1:** [manifest](results/final/FINAL_DATASET_MANIFEST.json) · [resumo](results/final/FINAL_SUMMARY.json).
- **Pacotes oficiais v1 e v2:** anexados à release consolidada.
- **Evidências para o relatório científico:** [`results/final/evidence/`](results/final/evidence/).
- **Critério de congelamento científico:** [`docs/PHYSICAL_V2_READINESS.md`](docs/PHYSICAL_V2_READINESS.md).

O diretório `results/physical_v2/` é produzido pelo comando `ic-physical-v2` e disponibilizado no pacote da **release**, não necessariamente como pasta versionada na `main`. Não se deve inferir ausência de resultados v2 pela ausência dessa pasta na árvore de arquivos.

### Integridade dos dados e futuro aprendizado

Os conjuntos exportados separam `scientific_records`, `observable_features` e `causal_labels`. O registro completo contém o estado exato e os parâmetros da simulação (*ground truth*); o conjunto de características observáveis exclui identificadores e parâmetros que revelariam diretamente a classe causal. Essa separação **prepara** estudos futuros, mas não valida, por si só, identificabilidade, generalização ou desempenho de aprendizado.

## 6. Estado de validação e publicação

A [execução da `main` de 8 de outubro de 2026](https://github.com/DanielBaptista01/IC-Computacao_Cientifica/actions/runs/37844331504), vinculada ao commit da release, concluiu com sucesso testes, geração e publicação dos dois pacotes científicos.

A documentação de prontidão registra **104 testes** no estado pré-freeze; para verificar o estado corrente, use `pytest` e o workflow [`scientific-tests`](https://github.com/DanielBaptista01/IC-Computacao_Cientifica/actions/workflows/tests.yml). A execução bem-sucedida do CI sustenta **reprodutibilidade computacional naquele ambiente**, não validação independente em hardware ou generalização física irrestrita.

**A tag congelada permanece fixa:** commits de manutenção ou apresentação na `main` não redefinem retroativamente o estado científico da release.

## 7. Limitações e status epistemológico

| Categoria | O que o projeto sustenta |
| --- | --- |
| **Literatura estabelecida** | Formalismo sistema–ambiente, operações quânticas, traço parcial, canais CPTP/Kraus, métricas informacionais |
| **Proposta autoral** | Enquadramento de fontes específicas como *Agentes Causais* e Transformações Causais Latentes entre profundidades |
| **Validado por simulação** | Implementações dos modelos no domínio declarado, experimentos controlados, métricas, colisões de assinatura e classificação operacional de reversibilidade |
| **Não demonstrado** | Identidade física única a partir do canal reduzido, superioridade universal de estratégias adaptativas, inferência causal de todo ruído real |
| **Trabalho futuro** | Comparação com medições de hardware, novos modelos físicos e avaliação de aprendizado clássico, híbrido ou QML |

Limitações explícitas do corpus: estudo predominantemente de **um qubit**, grades paramétricas teóricas, ausência de hardware/shots/erros de leitura, aproximações físicas e fenomenológicas documentadas, coerência `\ell_1` dependente da base e identificabilidade dependente do protocolo. Alguns fenômenos macroscópicos, acoplamentos espaciais multiqubit e calibrações dependentes de plataforma permanecem fora de escopo.

**Nenhum modelo de Machine Learning ou Quantum Machine Learning foi treinado nesta IC.** A Utunnel pertence à trajetória exploratória anterior e **não** é resultado final comprovado desta linha. Para os limites de cada mecanismo, consulte [auditoria físico-causal](docs/PHYSICAL_CAUSAL_AGENTS_AUDIT.md) e [limitações científicas v1](results/final/evidence/FINAL_LIMITATIONS.md).

## 8. Bibliografia, autoria e histórico

**Autoria e formulação de pesquisa:** Daniel Santos Baptista — Iniciação Científica iniciada em fevereiro de 2026.

**Documentos autorais prioritários:** *Relatório Parcial de Atividades — IC 2026* e *Modelagem e Quantificação do Agente Causal*. Esses materiais registram a evolução conceitual; não foram automaticamente tratados como evidência de validação de hipóteses.

**Fundamentos de referência:**
- Nielsen, M. A.; Chuang, I. L. *Quantum Computation and Quantum Information*. Cambridge University Press, 2010.
- Breuer, H.-P.; Petruccione, F. *The Theory of Open Quantum Systems*. Oxford University Press, 2002.
- Baumgratz, T.; Cramer, M.; Plenio, M. B. “Quantifying Coherence”. *Physical Review Letters* **113**, 140401 (2014).

**Documentação científica do projeto:** [formalismo](docs/MATHEMATICAL_MAPPING.md) · [protocolo de coleta](docs/CAUSAL_AGENT_COLLECTION_PROTOCOL.md) · [auditoria final](docs/FINAL_CODE_SCIENTIFIC_AUDIT.md) · [auditoria físico-causal](docs/PHYSICAL_CAUSAL_AGENTS_AUDIT.md).

**Histórico reprodutível:** [Pull Requests](https://github.com/DanielBaptista01/IC-Computacao_Cientifica/pulls?q=is%3Apr) · [GitHub Actions](https://github.com/DanielBaptista01/IC-Computacao_Cientifica/actions) · [Releases](https://github.com/DanielBaptista01/IC-Computacao_Cientifica/releases).

---

**Princípio metodológico da IC:** problema → hipótese → modelo → implementação → testes → experimento → dados → análise crítica. A contribuição autoral é uma **hipótese de organização e caracterização causal** investigada numericamente, e não uma alegação de solução universal para a decoerência.
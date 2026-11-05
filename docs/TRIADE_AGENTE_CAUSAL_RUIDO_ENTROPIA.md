# A tríade Agente Causal – Ruído – Entropia

**Objetivo científico transversal da IC 2026.** Esta nota explicita a relação conceitual, o formalismo e as limitações de inferência associados à tríade, em continuidade à formulação autoral de *Modelagem e Quantificação do Agente Causal* e ao Relatório Parcial da IC. As expressões de sistemas abertos e informação quântica são resultados consolidados; a organização por *Agente Causal* é a proposta autoral investigada no corpus computacional.

## 1. Três conceitos que não são sinônimos

| Componente | Significado nesta pesquisa | O que **não** representa |
| --- | --- | --- |
| **Agente Causal** $A_k$ | Fonte física ou mecanismo específico que pode interagir com o qubit (ex.: campo magnético, banho bosônico, reservatório fotônico) | Não é automaticamente o nome de um canal quântico |
| **Ruído** | Manifestação operacional do desvio provocado pela interação relativamente à evolução de referência pretendida | Não é, por definição, a própria fonte; não precisa ser um escalar |
| **Entropia** $S(\rho)$ | Grandeza informacional calculada sobre o estado; ajuda a medir mistura e mudanças no espectro | Não é o ruído, nem identifica sozinha o agente; não é necessariamente crescente |

A **interação** conecta os componentes: uma fonte/mecanismo produz uma dinâmica física; a dinâmica modifica ou não o estado em relação ao processo desejado; dessa diferença obtemos descritores de perturbação e métricas informacionais.

A cadeia conceitual autoral é:

$$
\underbrace{A_k}_{\text{fonte/mecanismo}}
\longrightarrow
\underbrace{H_{\mathrm{int}}^{(k)}}_{\text{interação física, quando aplicável}}
\longrightarrow
\underbrace{\mathcal{E}_{k,t}}_{\text{dinâmica reduzida}}
\longrightarrow
\underbrace{\rho'_k}_{\text{estado resultante}}
\longrightarrow
\underbrace{\Sigma_{k,t}}_{\text{assinatura operacional}}.
$$

$$
\Sigma_{k,t}=(N_k,\Delta S_k,\Delta P_k,\Delta C_k,F_k,\ldots).
$$

A tríade **não** deve ser interpretada como uma lei de causa única: múltiplos mecanismos podem atuar conjuntamente e seus efeitos podem não ser aditivos ou separáveis apenas pelo qubit observado.

## 2. Fundamento em sistemas quânticos abertos

Para uma condição inicial sem correlações sistema–ambiente e um ambiente fixado, pode-se escrever:

$$
\rho'_{S,k}(t)=
\mathrm{Tr}_E\![
U_{SE}^{(k)}(t)\,
(\rho_S(0)\otimes\rho_E(0))
U_{SE}^{(k)\dagger}(t)
]
=\mathcal{E}_{k,t}\!(\rho_S(0)).
$$

Nessas hipóteses, a aplicação $\mathcal{E}_{k,t}$ é um canal CPTP e pode admitir representação de Kraus. Essa representação descreve o **efeito reduzido**, mas não determina unicamente a identidade microscópica da fonte. Na presença de correlações iniciais, memória ou dependências de intervenções anteriores, a atribuição de um canal CPTP independente por intervalo exige hipóteses adicionais.

Para definir *ruído observado*, precisamos especificar a **evolução ideal de referência** $\mathcal{G}_t$:

$$
\rho_{\mathrm{ideal}}(t)=\mathcal{G}_t\!(\rho_S(0)),
\qquad
\delta\rho_k(t)=\rho'_{S,k}(t)-\rho_{\mathrm{ideal}}(t).
$$

$\delta\rho_k$ é uma **diferença de operadores**, não um operador densidade. Como indicador quantitativo de desvio, pode-se utilizar a distância de traço:

$$
N_k(t;\rho_S(0))\equiv
D_{\mathrm{tr}}\!(\rho'_{S,k}(t),\rho_{\mathrm{ideal}}(t))
=\frac12\lVert
\rho'_{S,k}(t)-\rho_{\mathrm{ideal}}(t)
\rVert_1.
$$

A definição de $N_k$ é um **descritor operacional escolhido** para a análise; não pretende reduzir todos os mecanismos de ruído a um único número. Ela depende também do estado de prova, do tempo e do protocolo. Em comparações com dados do corpus, verificar se a referência é o **estado de entrada** ou o **resultado ideal** da operação programada.

## 3. Como a entropia participa — e quais são seus limites

Para o operador densidade do qubit:

$$
S(\rho)=-\mathrm{Tr}\!(\rho\log_2\rho),\qquad
\Delta S_k=S(\rho'_{S,k})-S(\rho_S(0)).
$$

Na comparação contra uma operação de referência geral, também é possível definir

$$
\Delta S_k^{(\mathrm{ideal})}
=S(\rho'_{S,k})-S(\rho_{\mathrm{ideal}}).
$$

As duas expressões coincidem quando a evolução ideal é unitária, pois esta preserva o espectro e a entropia do estado inicial. Em geral, devem ser distinguidas.

**Caso A — perturbação coerente/unitária.** Se $\rho'=U\rho U^\dagger$, então

$$
S(\rho')=S(\rho),\qquad P(\rho')=P(\rho).
$$

Isso **não** impede que a distância de traço ao alvo ou a fidelidade ao estado ideal indiquem uma perturbação. Portanto, $\Delta S=0$ **não** prova ausência de ruído.

**Caso B — canal não unitário.** A entropia pode aumentar, diminuir ou, em condições específicas, permanecer constante; isso depende do canal e do estado de entrada. Como exemplo analítico didático, um canal de *amplitude damping* com parâmetro $p=1/2$ aplicado a $\rho=I/2$ produz $\rho'=\mathrm{diag}(3/4,1/4)$: a entropia cai de $1$ bit para $H_2(3/4)\approx0{,}811$ bit. Logo, "ruído aumenta a entropia" **não** é uma lei geral.

**Medidas complementares:** pureza $P(\rho)=\mathrm{Tr}(\rho^2)$; coerência $C_{\ell_1}(\rho)=\sum_{i\neq j}|\rho_{ij}|$ em base definida; fidelidade a um estado-alvo; distância de traço; espectro e, quando possível, correlações sistema–ambiente. Medir a entropia do subsistema não equivale automaticamente a medir entropia termodinâmica total produzida.

## 4. Evidência disponível na implementação

A tabela [`results/final/tables/agent_noise_entropy_summary.csv`](../results/final/tables/agent_noise_entropy_summary.csv) registra, para o baseline mecanístico v1:

| Modelo | Amostras | Maior distância de traço à entrada | Maior valor de $\lvert\Delta S\rvert$ |
| --- | ---: | ---: | ---: |
| Perturbação longitudinal coerente | 5.670 | $1$ | $8{,}00856626\times10^{-16}$ |
| Banho spin–boson finito (*dephasing*) | 18.144 | $0{,}5$ | $1$ |
| Troca de excitação com nível auxiliar finito | 5.670 | $1$ | $1$ |
| Reservatório fotônico Markoviano | 5.670 | $\approx0{,}9999965$ | $\approx0{,}9999971$ |

*Os extremos são calculados sobre amostras possivelmente diferentes; não devem ser interpretados como uma mesma trajetória.*

No caso coerente, o valor entrópico é numericamente zero dentro do erro de arredondamento, mesmo quando a perturbação é observável. Esse resultado valida a distinção **ruído observado ≠ variação de entropia** no protocolo simulado.

Na comparação de canais reduzidos de famílias distintas, a simulação também encontrou situações de coincidência de assinatura. Assim, **nem mesmo a dinâmica reduzida completamente caracterizada garante unicidade da fonte**. A combinação de métricas pode enriquecer a assinatura observável, mas não eliminar impossibilidades fundamentais de identificação quando dois agentes induzem o mesmo processo.

**Rastreabilidade:** [resultados científicos](../results/final/evidence/FINAL_SCIENTIFIC_RESULTS.md), [tabela da tríade](../results/final/tables/agent_noise_entropy_summary.csv), [limitações](../results/final/evidence/FINAL_LIMITATIONS.md), [mapeamento formalismo–código](MATHEMATICAL_MAPPING.md), [análise de identificabilidade](../results/final/evidence/FINAL_IDENTIFIABILITY_ANALYSIS.md).

## 5. Objetivo e próxima hipótese, sem antecipar conclusões

O objetivo da tríade é **estabelecer uma relação auditável entre o mecanismo físico modelado, a perturbação operacional observada e a resposta informacional do estado**, permitindo:

1. caracterizar matematicamente a dinâmica e seus parâmetros;
2. quantificar o efeito em estados e condições experimentais definidos;
3. separar erros coerentes de mudanças entrópicas e identificar limites de reversibilidade;
4. testar quais assinaturas podem distinguir fontes e quais permanecem ambiguamente atribuíveis;
5. formar registros reproduzíveis para eventual comparação futura de estratégias adaptativas.

**Classificação epistemológica:** a teoria CPTP, o traço parcial e a entropia de von Neumann são literatura estabelecida; a especialização autoral por *Agente Causal* e a organização da tríade pertencem à pesquisa; os valores tabelados são **resultados de simulação para modelos controlados**, não medidas de hardware; inferência causal universal e vantagens de ML/QML **não foram demonstradas**.

**Documento autoral de referência:** *Modelagem e Quantificação do Agente Causal*; **registro de evolução:** *Relatório Parcial de Atividades — IC 2026*. A presente nota é a formalização explicativa complementar da implementação, não a substituição desses documentos.

> Tradução comunitária (rascunho) — Política NTARI P2-002, Transmissão Multilíngue Global (Global Multilingual Broadcast). Fonte: CONFORMANCE.md (original em inglês, snapshot de 2026-10-05). Rascunho comunitário assistido por máquina, pendente de revisão por mantenedor regional conforme P2-002 §3.1. As especificações técnicas centrais permanecem em inglês conforme §2.2.
>
> Notou algum erro nesta tradução? Correções de tradução são contribuições
> valiosas e muito bem-vindas: faça um fork do repositório e abra um pull
> request em https://github.com/NTARI-RAND/childcare-trust-network.

> O original em inglês é normativo. Esta tradução é oferecida para leitura, não para interpretação: onde ela divergir de `CONFORMANCE.md`, prevalece o inglês. As palavras-chave normativas (MUST, MUST NOT, SHOULD, SHOULD NOT, MAY), os nomes de campos, os rótulos e os identificadores são mantidos em inglês porque constituem o contrato de conformidade.

# CTN — Autodescrição de conformidade

*Autoatestada até que um conjunto de testes cite estes IDs (registro: `JFA/jfa-conformance-suite.py`). A CTN está em estágio de proposta; "atendido por design" significa que a especificação (`CLAUDE.md`) declara a regra e o critério de aceitação — o código ainda precisa vinculá-la.*

**Forma:** a economia do cuidado de alto risco da Parte VI da arquitetura — distribuição completa das avaliações, camada de segurança centrada na prevenção que tem precedência sobre todas as outras regras.

| ID | Invariante | Status |
|---|---|---|
| COV-1 | Sem médias; distribuição completa | **Atendido por design** — seção "Do not average", critério de aceitação via grep; delegar à CI na construção |
| COV-2 | A avaliação mais baixa é a violação | **Atendido por design** — `-1` é dano, `harm_flagged`, comentário obrigatório |
| COV-3 | Simétrico; toda alegação admite resposta | **Parcial** — avaliação multidirecional, sim; disputa/direito de resposta em aberto (OQ-6) |
| COV-4 | Controla se, nunca quanto | **Atendido por design** — três sinais honestos (verificação, distribuição, tempo de permanência), nunca colapsados |
| REC-1 | Somente de adição | **Atendido por design** — eventos de avaliação imutáveis; testemunho em aberto (OQ-7) |
| REC-2 | Perdoar, nunca ocultar | **Atendido por design** — disputas sinalizam e contextualizam, nunca apagam |
| REC-3 | Nenhuma PII no commons | **Atendido por design** — dados de crianças nunca entram no repositório de eventos nem em qualquer saída de reputação |
| REC-9 | Tipos de relação | **Em aberto** (OQ-8) |
| ECO-4/5 | Custódia (escrow) em primeiro lugar; conquistado, nunca comprado, se o crédito algum dia entrar | **Padrão comprometido** (OQ-5) |
| GOV-9 | Documento vivo de questões em aberto | **Atendido** — `OPEN-QUESTIONS.md` acompanha esta semente |
| GOV-10 | Commons copyleft | **Atendido** — AGPL-3.0, declarado na especificação |

**Precedência nomeada:** a trilha de segurança infantil prevalece sobre o pacto onde houver conflito — o precedente de alto risco da Parte VI, adotado deliberadamente, com o devido processo regendo a durabilidade das consequências, e não a proteção imediata.

**Linha de honestidade:** a CTN não tem registro testemunhado; toda alegação de conduta que ela faz hoje é autoatestada (problema em aberto 2 da arquitetura).

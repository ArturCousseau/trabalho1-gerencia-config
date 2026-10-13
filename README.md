# Todo
- [ ] Arquivo do slide final
- [ ] Arquivos markdown sobre o conteudo
- [ ] Link das referencias
- [x] Descrição tese 
- [ ] Atualizar a estrutura de arquivos do repositorio

# Qualidade e revisão de código na era da IA

Repositório do Trabalho avaliativo 1 da disciplina de Gerência de Configuração, da Universidade de Caxias do Sul (UCS).

O trabalho aborda o **Tema 3: Qualidade e Revisão de Código (Code Review)**. 

## Integrantes
- Miguel Valentini 
- Guilherme Augusto Giehl Garbin
- Artur Dias Cousseau
- Matheus Andreazza Pörsch

## Tese
A revisão de código continua relevante como uma camada de garantia da qualidade, junto a outras. Testes, linters, análise estática e CI/CD automatizam verificações repetíveis; a revisão humana pode avaliar o contexto, a intenção da mudança e as decisões de projeto. À medida que a IA aumenta o volume de código a examinar, a atenção dos revisores pode se tornar um gargalo. Mudanças menores e checagens automáticas ajudam a direcionar essa atenção às questões que exigem julgamento.

## Perguntas norteadoras
**Pergunta principal:** revisar código é relevante no contexto atual? Como a IA alterou o ecossistema de desenvolvimento de software?

- Por que as equipes revisam o código umas das outras? O motivo declarado é o motivo real? 
- Quais defesas um defeito precisa atravessar até chegar em produção — e a revisão é qual delas?
- Existe limite para o quanto um humano consegue revisar com atenção? O que fazer quando o volume passa desse limite?

## Referências sugeridas pelo professor

### Artigo âncora
BACCHELLI, A.; BIRD, C. **Expectations, Outcomes, and Challenges of Modern Code Review.** ICSE, 2013.  
[DOI: 10.1109/ICSE.2013.6606617](https://doi.org/10.1109/ICSE.2013.6606617)

### Complementos
- HAINDL, P.; WEINBERGER, G. **Does ChatGPT Help Novice Programmers Write Better Code? Results From Static Code Analysis.** IEEE Access, v. 12, 2024. [DOI: 10.1109/ACCESS.2024.3445432](https://doi.org/10.1109/ACCESS.2024.3445432)
- CZERWONKA, J.; GREILER, M.; TILFORD, J. **Code Reviews Do Not Find Bugs.** ICSE-SEIP, 2015. [DOI: 10.1109/ICSE.2015.131](https://doi.org/10.1109/ICSE.2015.131)
- McINTOSH, S.; KAMEI, Y.; ADAMS, B.; HASSAN, A. E. **The Impact of Code Review Coverage and Code Review Participation on Software Quality.** MSR, 2014. [DOI: 10.1145/2597073.2597076](https://doi.org/10.1145/2597073.2597076) · [PDF](https://rebels.cs.uwaterloo.ca/papers/msr2014_mcintosh.pdf)
- SADOWSKI, C. et al. **Modern Code Review: A Case Study at Google.** ICSE-SEIP, 2018. [DOI: 10.1145/3183519.3183525](https://doi.org/10.1145/3183519.3183525) · [Página da publicação](https://research.google/pubs/modern-code-review-a-case-study-at-google/)
- THOUGHTWORKS. **The Future of Software Engineering — Retreat Findings.** 2026.
- GOOGLE. **Engineering Practices — Code Review.** [Documentação](https://google.github.io/eng-practices/review/)

## Referências adicionais
- SOBRENOME, N. **Título.** Veículo, ano. [Link](url)
  *Usada para: (uma linha dizendo qual argumento ela sustenta).*

SYSTEMD. ci: Drop codeql workflow (PR #41277). GitHub, 2026. https://github.com/systemd/systemd/pull/41277
Usada para: mostrar que uma camada mal calibrada gasta atenção (218 alertas do CodeQL, 3 correções úteis) e que a decisão de removê-la saiu da própria revisão.

MICROSOFT. Fix using followed by newline ignoring [no LineTerminator here] grammar restriction (PR #3869). GitHub, 2026. https://github.com/microsoft/typescript-go/pull/3869
Usada para: mostrar que a IA corrigiu o defeito, mas foi o revisor humano quem identificou a causa real (erro de port), avaliando contexto e intenção.

PICHAI, S. Alphabet Q3 2024 Earnings Call. Fortune, 2024. https://fortune.com/2024/10/30/googles-code-ai-sundar-pichai
Usada para: o ponto de partida do aumento de código gerado por IA no Google (mais de 25% do código novo, em out/2024).

PICHAI, S. Google CEO says 75% of company’s new code is AI-generated. Semafor, 2026. https://www.semafor.com/article/04/24/2026/google-ceo-says-75-of-companys-new-code-is-ai-generated
Usada para: o ponto de chegada (75% do código novo gerado por IA e revisado por engenheiros, em abr/2026), sustentando que o volume a revisar aumentou.

## Estrutura do repositório
```
.
├── README.md
├── slides/
│   └── apresentacao.pdf
├── conteudo/
│   ├── 01.md
│   ├── 02.md
│   ├── 03.md
│   └── 04.md
```

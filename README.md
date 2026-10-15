# Qualidade e revisão de código na era da IA

Repositório do Trabalho avaliativo 1 da disciplina de Gerência de Configuração, da Universidade de Caxias do Sul (UCS).

O trabalho aborda o **Tema 3: Qualidade e Revisão de Código (Code Review)**. 

## Integrantes
- Artur Dias Cousseau
- Guilherme Augusto Giehl Garbin
- Matheus Andreazza Pörsch
- Miguel Valentini 

## Tese
A revisão de código continua relevante como uma camada de garantia da qualidade, junto a outras. Testes, linters, análise estática e CI/CD automatizam as verificações repetíveis, enquanto a revisão humana avalia o contexto, a intenção da mudança e as decisões de projeto. À medida que a IA aumenta o volume de código, a atenção de quem escreve e revisa pode se tornar o limite do processo. Por isso, o que muda com a IA não é a necessidade de revisar, mas onde a atenção humana precisa estar: automatizar o que é mecânico e respeitar o limite de atenção das pessoas mantém o julgamento humano onde ele realmente importa.

## Perguntas norteadoras
**Pergunta principal:** revisar código é relevante no contexto atual? Como a IA alterou o ecossistema de desenvolvimento de software?

- Por que as equipes revisam o código umas das outras? O motivo declarado é o motivo real? 
- Quais defesas um defeito precisa atravessar até chegar em produção — e a revisão é qual delas?
- Existe limite para o quanto um humano consegue revisar com atenção? O que fazer quando o volume passa desse limite?

## Referências sugeridas pelo professor
 
### Artigo âncora
BACCHELLI, A.; BIRD, C. **Expectations, Outcomes, and Challenges of Modern Code Review.** ICSE, 2013.  
[DOI: 10.1109/ICSE.2013.6606617](https://doi.org/10.1109/ICSE.2013.6606617) · [PDF](https://sback.it/publications/icse2013.pdf)
 
### Complementos
- HAINDL, P.; WEINBERGER, G. **Does ChatGPT Help Novice Programmers Write Better Code? Results From Static Code Analysis.** IEEE Access, v. 12, 2024. [DOI: 10.1109/ACCESS.2024.3445432](https://doi.org/10.1109/ACCESS.2024.3445432)
- CZERWONKA, J.; GREILER, M.; TILFORD, J. **Code Reviews Do Not Find Bugs.** ICSE-SEIP, 2015. [DOI: 10.1109/ICSE.2015.131](https://doi.org/10.1109/ICSE.2015.131)
- McINTOSH, S.; KAMEI, Y.; ADAMS, B.; HASSAN, A. E. **The Impact of Code Review Coverage and Code Review Participation on Software Quality.** MSR, 2014. [DOI: 10.1145/2597073.2597076](https://doi.org/10.1145/2597073.2597076) · [PDF](https://rebels.cs.uwaterloo.ca/papers/msr2014_mcintosh.pdf)
- SADOWSKI, C. et al. **Modern Code Review: A Case Study at Google.** ICSE-SEIP, 2018. [DOI: 10.1145/3183519.3183525](https://doi.org/10.1145/3183519.3183525) · [Página da publicação](https://research.google/pubs/modern-code-review-a-case-study-at-google/)
- THOUGHTWORKS. **The Future of Software Engineering — Retreat Findings.** 2026.
- GOOGLE. **Engineering Practices — Code Review.** [Documentação](https://google.github.io/eng-practices/review/)
## Referências adicionais
 
### Revisão de código
- BELLER, M.; BACCHELLI, A.; ZAIDMAN, A.; JUERGENS, E. **Modern Code Reviews in Open-Source Projects: Which Problems Do They Fix?** MSR, 2014. [PDF](https://sback.it/publications/msr2014.pdf)  
  *Usada para: mostrar o que a revisão realmente corrige em projetos open source, em comparação com o motivo declarado.*
- BOSU, A.; GREILER, M.; BIRD, C. **Characteristics of Useful Code Reviews: An Empirical Study at Microsoft.** MSR, 2015. [PDF](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/bosu2015useful.pdf)
### Casos reais
- SYSTEMD. **ci: Drop codeql workflow (PR #41277).** GitHub, 2026. [Link](https://github.com/systemd/systemd/pull/41277)  
  *Usada para: mostrar que uma camada mal calibrada gasta atenção (218 alertas do CodeQL, 3 correções úteis) e que a decisão de removê-la saiu da própria revisão.*
- MICROSOFT. **Fix using followed by newline ignoring [no LineTerminator here] grammar restriction (PR #3869).** GitHub, 2026. [Link](https://github.com/microsoft/typescript-go/pull/3869)  
  *Usada para: mostrar que a IA corrigiu o defeito, mas foi o revisor humano quem identificou a causa real (erro de port), avaliando contexto e intenção.*
### Volume de código gerado por IA
- PICHAI, S. **Alphabet Q3 2024 Earnings Call.** Fortune, 2024. [Link](https://fortune.com/2024/10/30/googles-code-ai-sundar-pichai)  
  *Usada para: o ponto de partida do aumento de código gerado por IA no Google (mais de 25% do código novo, em out/2024).*
- PICHAI, S. **Google CEO says 75% of company's new code is AI-generated.** Semafor, 2026. [Link](https://www.semafor.com/article/04/24/2026/google-ceo-says-75-of-companys-new-code-is-ai-generated)  
  *Usada para: o ponto de chegada (75% do código novo gerado por IA e revisado por engenheiros, em abr/2026), sustentando que o volume a revisar aumentou.*
### Atenção, fadiga e burnout
- LANEIRO, T.; BRITES, R.; TAP, P.; SILVA, A.; REGUINGA, O.; GUERRA, S. **A Influência da Alteração dos Ciclos Circadianos na Auto-Percepção Individual: a Experiência Subjectiva de Fadiga, Atenção, Tensão e Satisfação na Tarefa.** Psicologia, Saúde & Doenças, Lisboa, v. 12, n. 1, 2011. [PDF](https://www.redalyc.org/pdf/362/36222221007.pdf). Acesso em: 12 out. 2026.  
  *Usada para: sustentar que a fadiga reduz a atenção e o desempenho em tarefas que exigem vigilância.*
- AVEIRO, B. M.; RODRIGUES, C. **Burnout em desenvolvedores e a relação com o trabalho remoto.** Revista Tecnologias em Projeção, v. 14, n. 2, p. 14–26, 2023. [Link](https://revistatecnologias.com/index.php/Projecao4/article/view/2220/1712). Acesso em: 12 out. 2026.  
  *Usada para: relacionar burnout e trabalho remoto entre desenvolvedores.*
- FELDMANN, P. R. **Aplicações de medida do trabalho em atividades de programação de computadores.** Dissertação (Mestrado em Administração) – Fundação Getulio Vargas, São Paulo, 1979. [PDF](https://repositorio.fgv.br/server/api/core/bitstreams/f93103fd-ad4a-47a4-ad23-961df12c3200/content). Acesso em: 12 out. 2026.  
  *Usada para: o tempo gasto em recuperação durante atividades de programação.*
- BRASIL. Ministério da Saúde. **Síndrome de Burnout.** [Link](https://www.gov.br/saude/pt-br/assuntos/saude-de-a-a-z/s/sindrome-de-burnout)  
  *Usada para: a definição de burnout.*

## Estrutura do repositório
```
.
├── README.md
├── slides/
│   └── apresentacao-final.pdf
├── conteudo/
│   ├── 01-por-que-revisamos.md
│   ├── 02-camadas-de-defesa.md
│   ├── 03-cansaco-no-desenvolvimento-de-software.md
│   └── 04-revisao-na-pratica.md
```

# 03 · Revisão na prática: IA e revisão humana em uma equipe pequena
## 1. Contexto: a equipe

Este é um relato da equipe em que trabalho, uma equipe pequena de desenvolvimento.

- **Antes:** havia um estagiário responsável por testar as atividades antes que elas seguissem adiante.
- **A mudança:** quando o estagiário saiu, a decisão da chefia foi não substituí-lo e passar essa função para a IA.
- **Hoje:** usamos o **Codex**, um agente de programação da OpenAI. Ele escreve o código, cria e executa os testes e confere se o que foi pedido foi atendido.

A IA passou a ocupar mais de uma camada da esteira. A revisão humana do PR continuou igual.

---

## 2. O fluxo de trabalho

```
pedido → Codex escreve código e testes → Codex executa os testes
       → verificação pela IA (acionada pelo dev) → PR aberto → revisão humana → merge
```

1. **Pedido:** passo a atividade para o Codex.
2. **Código e testes:** o Codex escreve o código, escreve os testes e os executa.
3. **Verificação pela IA:** antes de abrir o PR, peço que o Codex revise as alterações, procurando erros, possíveis melhorias e se o pedido foi atendido.
4. **PR e revisão humana:** só então abro o PR, e meu chefe revisa manualmente. Ele olha a lógica e se havia um jeito mais simples de resolver. A IA não participa dessa etapa.

### Comparação com a esteira da parte 02

| Camada | Esteira da [parte 02](02-camadas-de-defesa.md) | Nossa equipe |
|---|---|---|
| Checks automáticos (build, testes, linter) | Rodam no CI, a cada PR | Testes criados e executados pelo Codex, antes do PR |
| Revisão por IA | No PR, por uma ferramenta separada | Acionada pelo próprio dev, antes do PR, pela mesma IA que escreveu o código |
| Revisão humana | No PR | No PR, feita pelo chefe |

Na prática, nossa esteira tem **duas camadas**: a verificação da IA, que o próprio desenvolvedor aciona, e a revisão humana.

---

## 3. O que o caso mostra

### 3.1 Menos retrabalho no dia a dia

Quando havia estagiário, muitas atividades voltavam para mim. Um dos principais motivos: como ele estava começando, ainda não conhecia bem o produto, e devolvia atividades apontando problemas que não faziam sentido.

Hoje isso não acontece. Na minha percepção, a IA aponta erros que eu não via e lida melhor com as regras do produto do que o estagiário em início de carreira. É uma observação pessoal, não uma medição (ver [Limitações](#5-limitações)).

### 3.2 O revisor humano fica com o entendimento

O que chega ao meu chefe já passou por um filtro mecânico. Isso vai ao encontro do que Bacchelli e Bird (2013) recomendam: muitos comentários de revisão tratam de melhorias de código e de defeitos pequenos, de baixo nível, e os autores sugerem automatizar essas tarefas, porque isso *"frees reviewers to look for deeper, more subtle defects"*.

Por isso, a revisão do meu chefe é sobre entender:

- o código faz o que foi pedido?
- havia um jeito mais simples de resolver?

Como a [parte 01](01-por-que-revisamos.md) mostrou, revisar sempre foi mais entender e melhorar do que caçar bugs. O mesmo artigo mostra o peso do contexto: **716 dos 873 desenvolvedores pesquisados (82%)** disseram que revisores que conhecem os arquivos alterados dão um feedback diferente, mais profundo e mais conceitual. É esse conhecimento do produto e do código que o revisor humano traz.

### 3.3 O risco: a mesma IA em todas as camadas

No nosso fluxo, **a mesma ferramenta escreve o código, escreve os testes e confere o resultado**. Se ela entender o pedido errado, as três etapas podem errar juntas: o código faz a coisa errada, os testes confirmam a coisa errada e a verificação aprova.

Camadas só protegem de verdade quando são **independentes**. Na [parte 02](02-camadas-de-defesa.md), o caso do typescript-go mostra algo parecido: a IA revisora não questionou a explicação do bug, e foi o humano, comparando com o código original, quem encontrou a causa real.

No nosso caso, o chefe é o **único olhar humano e independente**. E ele recebe código que já parece revisado, o que traz de volta a pergunta da [parte 03](03-limite-da-atencao.md): quando tudo chega "pré-aprovado", a atenção humana se mantém ou cai?

---

## 4. Ligação com a pergunta do tema

**Revisar código é relevante hoje?** Na nossa equipe, sim, mas o que se revisa mudou. A IA absorveu o trabalho mecânico (escrever testes, rodá-los, apontar erros óbvios), e ao humano sobraram o contexto, a intenção e a responsabilidade pela aprovação. Como a IA concentra várias camadas na mesma ferramenta, a revisão humana passou a ser a única verificação independente do processo.

A conclusão completa do grupo está em [05-conclusao.md](05-conclusao.md).

---

## Referências desta parte

- BACCHELLI, A.; BIRD, C. Expectations, Outcomes, and Challenges of Modern Code Review. ICSE, 2013. https://doi.org/10.1109/ICSE.2013.6606617
- OPENAI. Codex. OpenAI, 2025. https://openai.com/codex/

# 02 · Camadas de defesa: onde a revisão humana entra

## 1. A esteira até a produção

Em um fluxo baseado em pull requests (PRs), uma mudança passa por várias verificações antes do merge. Depois do merge, a entrega (CD) leva para produção o que foi aprovado.

```
PR aberto → [ checks automáticos → revisão por IA → revisão humana ] → merge → deploy
                       └──────────── dentro do PR ────────────┘
```

| Camada | O que faz | Tipo de pergunta que responde |
|---|---|---|
| **Checks automáticos (CI)** | Build, testes, linter, análise estática | Objetiva: compila? Os testes passam? Há um padrão conhecido de vulnerabilidade? |
| **Revisão por IA** | Um modelo lê o diff e comenta | Mista: sugere problemas, mas sem garantia de acerto |
| **Revisão humana** | Uma pessoa lê a mudança e aprova ou pede alterações | De julgamento: a mudança faz o que deveria? A explicação está certa? Vale o custo? |

- **CI (integração contínua):** verificar automaticamente cada mudança.
- **CD (entrega contínua):** entregar o que passou.

### 1.1 O que cada verificação automática faz

**Pull request (PR).** É o pedido para juntar uma mudança ao código principal do projeto. O PR mostra o *diff* (as linhas adicionadas e removidas), roda as verificações automáticas e abre um espaço de conversa onde os revisores comentam, pedem alterações ou aprovam.

**Pipeline de CI.** É uma sequência de passos que roda sozinha a cada PR, normalmente em um servidor (no GitHub, pelo GitHub Actions). Cada passo termina com sucesso ou falha, e o resultado aparece no PR como um ✓ ou ✗. O projeto pode exigir que todos os passos passem antes de permitir o merge. Exemplo simplificado de um workflow do GitHub Actions para um projeto Node.js:

```yaml
name: CI
on: pull_request          # roda a cada PR
jobs:
  verificar:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4   # baixa o código do PR
      - run: npm ci                 # instala as dependências
      - run: npm run build          # build
      - run: npm run lint           # linter
      - run: npm test               # testes automatizados
```

**Build.** Transforma o código-fonte em algo executável: compila (C, Java, Go), transpila (TypeScript → JavaScript) ou empacota. Se o build falha, o código nem chega a rodar, e os outros passos geralmente param ali. Pega erros como sintaxe inválida, tipos incompatíveis ou uma função chamada com o nome errado.

**Testes automatizados.** São programas que executam partes do código com entradas conhecidas e conferem se a saída é a esperada. Um teste unitário verifica uma função isolada (`soma(2, 3)` deve dar `5`); um teste de integração verifica várias partes funcionando juntas (a API grava no banco e devolve o registro). Pegam regressões: algo que funcionava e parou de funcionar. Só pegam o que alguém pensou em testar.

**Linter.** Lê o código **sem executá-lo** e aponta problemas de estilo e padrões suspeitos: variável declarada e nunca usada, `==` onde deveria ser `===`, função grande demais, formatação fora do padrão do projeto. Exemplos: ESLint (JavaScript/TypeScript), Checkstyle (Java), `go vet` (Go). Tira da revisão humana as discussões de formatação e erros triviais.

**Análise estática de segurança.** Também lê o código sem executá-lo, mas procura padrões mais profundos, como vulnerabilidades conhecidas. Um exemplo é o **CodeQL**, do GitHub: ele transforma o código em uma espécie de banco de dados e roda consultas que descrevem padrões de falha, como "um dado vindo do usuário chega a uma consulta SQL sem tratamento". Por trabalhar com padrões, pode gerar **falsos positivos**: alertas sobre algo que, no contexto real, não é um problema.

**Revisão por IA.** Ferramentas como o revisor do GitHub Copilot leem o diff e deixam comentários no PR, como um revisor humano faria. Ajudam a apontar problemas, mas não têm garantia de acerto e podem tanto errar quanto deixar passar algo.

**O que nenhuma dessas camadas responde:** se a mudança faz o que o projeto realmente precisa, se a explicação da causa está correta e se a solução combina com as decisões de projeto. Essas perguntas dependem de contexto, e ficam com a revisão humana.

Essa divisão conversa com o artigo-âncora. Bacchelli e Bird (2013) observaram na Microsoft que, embora encontrar defeitos seja a motivação declarada, o resultado real da revisão é menos sobre achar erros do que se espera. Os autores concluem que *"code and change understanding is the key aspect of code reviewing"*. Se o defeito objetivo pode ser pego por uma camada automática, o que sobra para o humano é justamente entender a mudança.

---

## 2. Mais camadas ≠ mais proteção: o caso do systemd

Adicionar camadas só ajuda se elas forem **bem configuradas**, ou seja, se o que a ferramenta encontra compensa o ruído que ela gera.

**O que é o systemd.** É o sistema de inicialização e gerenciador de serviços usado pela maioria das distribuições Linux, como Debian, Ubuntu, Fedora e Arch. Quando o computador liga, o systemd é o primeiro processo a rodar: ele inicia os outros serviços (rede, login, servidores) e os gerencia enquanto o sistema funciona. É um projeto de código aberto, escrito principalmente em C e mantido no GitHub, onde cada mudança passa por PR, CI e revisão dos mantenedores. Por ficar no centro do sistema operacional, um defeito nele afeta a máquina inteira, e por isso a esteira de verificações importa.

**O caso.** No projeto systemd, o PR #41277 (*"ci: Drop codeql workflow"*), aberto por daandemeyer, propôs remover o CodeQL, uma ferramenta de análise estática, da esteira de CI. Na descrição, o autor relata:

- **218 alertas** do CodeQL analisados ao longo da história do projeto;
- apenas **3 correções úteis** em C++ atribuíveis à ferramenta.

**O custo para a revisão.** Os alertas apareciam como comentários dentro da conversa do PR, na mesma tela que o revisor lê. Na discussão, o mantenedor keszybz lembrou que, no PR #40880, o CodeQL havia deixado *"dozens of identical and completely useless comments"*, e acrescentou:

> *"CI fatigue is a real problem, and CI that has so high false positive rate contributes heavily to people **not** looking at CI."*

Ou seja, uma ferramenta mal calibrada não só deixa de ajudar a revisão: ela **gasta a atenção do revisor** e treina as pessoas a ignorar a esteira.

**Quem decidiu.** A remoção não foi automática. Um mantenedor (bluca) se opôs: *"we need more of these, rather than less"*. O autor respondeu que a ferramenta só produzia falsos positivos, e a discussão no próprio PR levou à decisão. A automação responde perguntas objetivas; **decidir se uma ferramenta vale o que custa exige julgamento humano**, e esse julgamento aconteceu dentro da revisão de código.

---

## 3. IA × humano: o caso do typescript-go

**O que é o TypeScript.** É uma linguagem da Microsoft que adiciona tipos ao JavaScript. O código TypeScript passa por um compilador (`tsc`), que verifica os tipos e gera JavaScript comum. Esse compilador sempre foi escrito no próprio TypeScript.

**O que é o typescript-go.** Em 2025, a Microsoft anunciou que estava reescrevendo o compilador em Go, uma linguagem compilada, com ganhos de cerca de 10 vezes no tempo de compilação nos projetos medidos pela equipe (de 9,1x a 13,5x). A Microsoft chama o projeto de *native port*: em vez de redesenhar o compilador do zero, o código existente é **portado**, ou seja, traduzido do TypeScript para Go mantendo o mesmo comportamento. Por isso, em quase todo PR do projeto, a referência de "certo" é o código original em TypeScript.

**O que é o parser.** É a parte do compilador que lê o texto do código e reconhece sua estrutura (isto é uma declaração, isto é uma expressão). O bug deste caso estava em uma regra do parser para a palavra `using`, usada para declarar recursos que são liberados automaticamente. A gramática do JavaScript diz que `using` só inicia uma declaração se não houver **quebra de linha** logo depois dela; com a quebra, `using` é tratado como um nome comum.

**O PR.** No PR #3869 (*"Fix `using` followed by newline ignoring [no LineTerminator here] grammar restriction"*), o agente de IA do GitHub Copilot, acionado a pedido de um mantenedor, corrigiu um bug no parser:

```go
// Antes (Go, com bug)
return p.isBindingIdentifier() || p.token == ast.KindOpenBraceToken && !p.hasPrecedingLineBreak()

// Depois (correção da IA)
return (p.isBindingIdentifier() || p.token == ast.KindOpenBraceToken) && !p.hasPrecedingLineBreak()
```

Simplificando, a regra deveria ser *"(A ou B) e sem quebra de linha"*. Sem os parênteses, a checagem de quebra de linha valia só para o B.

**A explicação da IA.** O agente atribuiu o bug à precedência de operadores do Go: em Go, `&&` tem prioridade sobre `||`. A IA revisora (Copilot reviewer) analisou os 6 arquivos alterados e não fez nenhum comentário.

**A explicação do humano.** O revisor Jake Bailey apontou outra causa e colou a linha do código original em TypeScript:

```ts
// Original (TypeScript)
return (isBindingIdentifier() || token() === SyntaxKind.OpenBraceToken) && !scanner.hasPrecedingLineBreak();
```

> *"This is just a plain porting bug, nothing to do with `&&` vs `||` precedence."*

A precedência de `&&` sobre `||` é a mesma em TypeScript e em Go. O original tinha os parênteses, e eles se perderam na tradução. **O código da IA estava certo; a explicação da causa estava errada.**

**Por que a explicação importa.** Se a causa fosse "o Go", não haveria motivo para procurar outros erros parecidos. Sendo um erro de port, a pergunta seguinte é: onde mais a tradução perdeu parênteses? O revisor chegou à causa certa porque usou o **contexto** (sabia que aquilo era um port) e a **intenção** (comparou com o que o código original queria fazer).

**Leitura do caso.** A IA corrigiu o defeito; o humano entendeu o porquê. Isso ilustra a conclusão de Bacchelli e Bird (2013): revisar é, em boa parte, entender a mudança. É **um caso só**, então serve como ilustração, não como prova de que isso acontece sempre.

---

## 4. O gargalo virou a verificação

Se a revisão humana fica com o julgamento, importa quem escreve o código que chega até ela.

**Mais código gerado por IA.** Segundo declarações do CEO do Google, Sundar Pichai, a parte do código novo da empresa gerada por IA e depois revisada por engenheiros passou de:

| Quando | Código novo gerado por IA no Google |
|---|---|
| Outubro de 2024 | mais de 25% |
| Abril de 2026 | 75% |

**Verificar virou o limite.** No encontro da Thoughtworks sobre o futuro da engenharia de software (2026), a conclusão mais repetida foi:

> *"Code generation is no longer the bottleneck — verification is."*

O mesmo relatório registra que ninguém na sala conseguiu citar dados sobre quantos defeitos a revisão manual realmente encontra, e recomenda medir isso em vez de tratar a revisão como garantia automática de qualidade.

**A pergunta que fica:** se gerar código ficou barato e cada mudança ainda precisa de alguém que entenda o contexto e a intenção, **E quando a atenção de quem escreve e verifica se esgota** 

---

## Referências desta parte

- BACCHELLI, A.; BIRD, C. Expectations, Outcomes, and Challenges of Modern Code Review. ICSE, 2013. https://doi.org/10.1109/ICSE.2013.6606617
- SYSTEMD. ci: Drop codeql workflow (PR #41277). GitHub, 2026. https://github.com/systemd/systemd/pull/41277
- HEJLSBERG, A. A 10x Faster TypeScript. TypeScript Blog, Microsoft, 2025. https://devblogs.microsoft.com/typescript/typescript-native-port/
- MICROSOFT. Fix `using` followed by newline ignoring [no LineTerminator here] grammar restriction (PR #3869). GitHub, 2026. https://github.com/microsoft/typescript-go/pull/3869
- PICHAI, S. Alphabet Q3 2024 Earnings Call. Fortune, 2024. https://fortune.com/2024/10/30/googles-code-ai-sundar-pichai
- PICHAI, S. Google CEO says 75% of company's new code is AI-generated. Semafor, 2026. https://www.semafor.com/article/04/24/2026/google-ceo-says-75-of-companys-new-code-is-ai-generated
- THOUGHTWORKS. The Future of Software Engineering — Retreat Findings. Engelberg, 2026.

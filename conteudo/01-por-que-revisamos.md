# 01 · Por que revisamos: o motivo declarado e o motivo real

## 1. O que é code review moderno

Em um code review moderno, quando uma mudança é realizada, outra pessoa do time de desenvolvimento lê o que foi alterado e comenta, e a partir disso aprova ou pede as alterações. um code review costuma ser vista como uma **camada de segurança contra bugs**. A pergunta desta parte é se isso se confirma na prática.

---

## 2. O motivo declarado: encontrar defeitos

Bacchelli e Bird (2013), pesquisadores da Universidade de Lugano e da Microsoft Research, estudaram como funcionava a revisão de código em times da Microsoft. Eles observaram 17 desenvolvedores, analisaram 570 comentários de revisão e aplicaram questionários a 165 gerentes e 873 programadores.

Quando foram perguntados por que fazem o code review, a principal resposta foi encontrar defeitos:

| Grupo         | Encontrar defeitos como motivação                                                                 |
| ------------- | ------------------------------------------------------------------------------------------------- |
| Gerentes      | principal motivo para **44%**                                                                     |
| Programadores | 1º motivo para 383 (44%), 2º para 204 (23%), 3º para 96 (11%): entre os 3 principais para **78%** |

---

## 3. O resultado real: o que os comentários mostram

Quando os autores classificaram os comentários de revisão, o resultado foi outro. **Defeitos foram apenas a quarta categoria mais frequente**, de nove, com 78 comentários (14%). As três categorias acima foram:

1. **Melhorias de código**, a mais frequente, com 165 comentários (29%): legibilidade, nomes melhores, formas mais simples de fazer a mesma coisa.
2. **Entendimento**: perguntas e esclarecimentos de quem quer entender o porquê da mudança.
3. **Comunicação social**: interação entre os membros do time.

Além disso, os defeitos encontrados eram, na maioria, **problemas lógicos simples**, como casos-limite ou valores de configuração, e não falhas estruturais profundas.

Os autores concluem que *"code and change understanding is the key aspect of code reviewing"*: o centro da revisão é entender o código e a mudança. Eles também apontam benefícios que vão além dos defeitos:

- **transferência de conhecimento** entre os membros do time;
- **consciência do time** (*team awareness*) sobre o que está mudando no projeto;
- **soluções alternativas** para os problemas;
- **propriedade compartilhada do código** (*shared code ownership*): o código deixa de ser "de quem escreveu" e passa a ser do time.

---

## 4. Isso vale fora da Microsoft?

O estudo de Bacchelli e Bird se limita aos times de uma empresa. Para saber se o padrão se repete, Beller et al. (2014) analisaram a revisão em **projetos de código aberto**, classificando manualmente **mais de 1.400 mudanças** feitas por causa da revisão em dois projetos.

Os resultados:

- **Proporção de 75:25** entre problemas de **manutenibilidade** (legibilidade, estrutura, documentação) e problemas **funcionais** (o código fazer a coisa errada). A mesma proporção já aparecia em estudos com empresas e projetos acadêmicos.
- **7% a 35% dos comentários de revisão são descartados**: não resultam em nenhuma mudança no código.
- **10% a 22% das mudanças não foram pedidas por nenhum comentário**: o próprio autor melhorou o código durante a revisão.

Ou seja, também no código aberto a revisão é, principalmente, **melhoria contínua**, não correção de bugs.

---

## 5. O que torna um comentário útil?

Bosu, Greiler e Bird (2015) estudaram a **utilidade** dos comentários de revisão na Microsoft. Eles consideraram útil um comentário que levou a uma mudança no código próximo e aplicaram essa classificação a cerca de **1,5 milhão de comentários** de cinco projetos.

Os achados:

- **34,5% dos comentários não foram úteis** para o autor da mudança.
- Revisores que **já conheciam os arquivos** (porque os haviam alterado ou revisado antes) fizeram comentários mais úteis.
- Quanto **mais arquivos** uma mudança tinha, **menor** a proporção de comentários úteis.

---

## 6. O que esses estudos mostram

O motivo declarado (encontrar defeitos) **não é** o principal resultado da revisão. Na prática, a revisão de código serve para:

- **entender** o código e a intenção da mudança;
- **melhorar** legibilidade, estrutura e arquitetura;
- **espalhar conhecimento** pelo time;
- **dividir a responsabilidade** pelo código, reduzindo a ideia de que cada parte "pertence" a quem a escreveu.

---

## Referências desta parte

- BACCHELLI, A.; BIRD, C. Expectations, Outcomes, and Challenges of Modern Code Review. ICSE, 2013. https://doi.org/10.1109/ICSE.2013.6606617
- BELLER, M.; BACCHELLI, A.; ZAIDMAN, A.; JUERGENS, E. Modern Code Reviews in Open-Source Projects: Which Problems Do They Fix? MSR, 2014. https://doi.org/10.1145/2597073.2597082
- BOSU, A.; GREILER, M.; BIRD, C. Characteristics of Useful Code Reviews: An Empirical Study at Microsoft. MSR, 2015. https://doi.org/10.1109/MSR.2015.21

# ISO29110-Lite — layout de documentação normativa orientado a racional

**Status:** proposta de evolução documental. Não normativa. Deve ser refinada antes de substituir o formato oficial de POPs, DOCs ou demais artefatos.

## Intenção

O ISO29110-Lite já defende documentação padronizada, progressiva, rastreável e voltada ao aprendizado consciente. Esta proposta acrescenta uma exigência: a documentação normativa não deve apresentar apenas a conclusão vigente; deve permitir compreender, em níveis progressivos de detalhe, o caminho racional que sustenta essa conclusão.

A intenção é inaugurar um formato no qual a norma consolidada continue curta e utilizável, mas permaneça explicitamente conectada ao percurso decisório que a produziu.

## Princípio de apresentação

Cada determinação relevante deve poder ser lida em dois sentidos complementares:

1. **da origem à conclusão**, para compreender como a decisão foi construída;
2. **da conclusão à origem**, para aprofundar o racional somente quando necessário.

Uma representação mínima pode assumir a forma:

**princípio/origem → contexto/evidência → decisão intermediária → consequência → determinação vigente**

Cada etapa deve apontar para o conteúdo atômico que explica seu racional. A seta é apenas uma primeira convenção visual; o requisito real é preservar o encadeamento e a rastreabilidade entre os nós.

## Consolidado e racional

A norma consolidada continua necessária para operação, auditoria e, quando aplicável, conformidade. Porém, ela deve funcionar como a última projeção visível de uma base decisória mais rica, não como substituta dessa base.

Quando uma determinação for obrigatória, o documento deve deixar claro qual versão da conclusão é autoritativa. A possibilidade de consultar o racional não relativiza a obrigação vigente; ela permite compreendê-la, criticá-la, ensiná-la e revisá-la conscientemente em outro momento.

## Documentação atômica e progressiva

O racional deve ser organizado em unidades pequenas e relacionáveis. Cada documento ou seção atômica deve responder a uma questão durável e permitir ligação explícita com princípios, decisões, evidências e consequências relacionadas.

A leitura deve seguir progressividade: um leitor começa por uma visão pequena e aprofunda apenas quando a necessidade exigir. O desenho desejado é:

**entrada curta → encadeamento resumido → aprofundamento seletivo → fonte exata do racional → artefato ou ação aplicável**

Esse modelo evita duas falhas opostas: esconder o racional atrás de um consolidado excessivamente curto ou obrigar todo leitor a percorrer um histórico cognitivo integral e desorganizado.

## Primeira materialização em Markdown

Enquanto não existir documentação dinâmica gerada a partir de uma base cognitiva estruturada, Markdown pode oferecer uma materialização inicial simples.

Devem ser explorados:

- seções pequenas e semanticamente nomeadas;
- links explícitos entre princípio, decisão, evidência, consequência e determinação;
- `<details>` e `<summary>` para revelar aprofundamentos opcionais sem remover informação do próprio documento;
- resumos de caminho que permitam enxergar rapidamente de onde uma determinação surgiu;
- documentação atômica reutilizável em diferentes percursos de leitura;
- versão e rastreabilidade das conclusões autoritativas.

`<details>`/`<summary>` não é o modelo final; é uma primeira forma leve de permitir que a pessoa escolha quanto precisa aprofundar sem perder acesso ao racional completo.

## Horizonte de documentação dinâmica

A direção futura é que o consolidado deixe de ser necessariamente um documento estático único. Uma base cognitiva estruturada poderá gerar projeções adequadas ao papel, contexto, objetivo e profundidade necessários ao leitor.

Nesse horizonte, a informação fonte permanece estruturada e rastreável, enquanto diferentes leituras podem ser produzidas dinamicamente sem criar novas origens independentes de conhecimento.

## Relação com FlowED

Esta proposta é coerente com o **Princípio do Foco no Caminho Cognitivo** em desenvolvimento no FlowED: o caminho cognitivo estruturado ocupa a posição de base primária do conhecimento normativo, enquanto o consolidado é uma projeção contextual dessa base.

O ISO29110-Lite pode funcionar como um laboratório inicial dessa ideia por já possuir compromisso com documentação padronizada, progressividade, rastreabilidade e aprendizado consciente.

## Próximos passos

Antes de adotar este layout como formato oficial do ISO29110-Lite, devem ser definidos e testados pelo menos:

- o conjunto mínimo de tipos de nó do racional;
- a maneira de representar o encadeamento resumido;
- critérios para decidir quando uma decisão merece racional próprio;
- regras de atomicidade e reutilização;
- convenções de links e IDs;
- versionamento de conclusões normativas;
- experiência de leitura progressiva em Markdown;
- futura integração com uma base cognitiva estruturada, como a linha MyTrues/CCP em desenvolvimento no ecossistema FlowED.

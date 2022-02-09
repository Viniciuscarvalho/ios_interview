# Questões de entrevistas em iOS

O intuito deste repositório é montar um guia de perguntas mais comuns em entrevistas para vagas em iOS, onde é uma transcrição dos vídeos da [Harsivu Edu](https://www.youtube.com/channel/UCKIpdz6fS_CTemcqMrFhDwQ)

A versão em PT-Br será a principal e teremos uma versão em EN-US também.

### Importante

Alguns termos não são literalmente traduzidos pois não temos algo relativo em PT-BR ou não faria sentido ler de acordo com a linguagem.

## Contribuindo

Caso queira contribuir com alguma pergunta que viu em algum teste, seu PR será muito bem vindo!

## Questões 

1. [Copy vs Readonly](#copy-vs-readonly)
2. [Copy vs Strong](#copy-vs-strong)
3. [Weak vs Strong](#weak-vs-strong)
4. [Weak vs Unowned](#weak-vs-unowned) 
5. [Gist of all the attributes](#gist-of-all-the-attributes)
6. [ARC & Retain Cycle](#arc-and-retain-cycle) 
7. [Optional in Swift](#optional-in-swift)
8. [What is ??](#what-is-??)
9. [Optional Chaining](#optional-chaining)
10. [Optional Binding](#optional-binding)

## Copy vs Readonly

- Copy

Ele cria uma nova cópia de um objeto e, uma vez que o novo objeto é criado, a contagem de retenção será 1;
Use copy quando precisar do valor de um objeto como está e não quiser que outro objeto atualize o valor do seu objeto;
Criar setters e getters 

- Readonly

Indica que a propriedade é somente leitura;
Só gera getter, nenhum setter será gerado;
Se você tentar alterar o valor, receberá um erro do compilador

# Copy vs Strong

- Copy

Ele cria uma nova cópia de um objeto e, uma vez que o novo objeto é criado, a contagem de retenção será 1;
Use copy quando precisar do valor de um objeto como está e não quiser que outro objeto atualize o valor do seu objeto;
Criar setters e getters 

- Strong

Aumenta a contagem de retenção em 1;
Cria setters e getters;
O objeto será mais mutável

# Weak vs Strong

- Weak

Não aumenta a contagem de retenção
Não proteja o objeto de ser desalocado pelo ARC
Na desalocação, objetos fracos serão definidos como nil, e todas as referências fracas são opcionais
Cria setters e getters

- Strong

Aumenta a contagem de retenção em 1
Protege o objeto de ser desalocado pelo ARC
Cria setters e getters
O objeto será mutável

# Weak vs Unonwned

- Weak

Não aumenta a contagem de retenção
Não proteja o objeto de ser desalocado pelo ARC
Na desalocação, objetos fracos serão definidos como nil, e todas as referências fracas são opcionais
Cria setters e getters

- Unowned

Não aumenta a contagem de retenção
Na desalocação, objetos fracos serão definidos como nil, e é por isso que todas as referências fracas são opcionais
Cria setters e getters

Nota: É importante que você use apenas referências sem dono quando você realmente sabe que o objeto nunca será nulo depois de definido

# Gist of all the attributes

- Strong: Adiciona referência para manter o objeto vivo;
- Weak: não adiciona referência para que o objeto possa se tornar nil por arco;
- Assign: atribuição normal, sem referência, usado principalmente para tipos de dados primitivos;
- Copy: faz nova cópia de um objeto, a cópia será imutável;
- Nonatomic: não torna objetos thread-safe, aumenta o desempenho;
- Readwrite: Cria os getters e setters;
- Readonly: Cria apenas getters;

# ARC & Retain Cycle

ARC é uma maneira que a Apple lida com o gerenciamento de memória para nós. Para cada objeto, ele mantém uma contagem de quantas referências fortes estão apontando para aquele objeto. E enquanto houver uma referência forte para um objeto, o objeto permanecerá na memória.

# Optional in Swift

Permite escrever código flexível e mais seguro;
Ponto de interrogação significa que pode ser nulo ou algum valor

# What is ??

Para fornecer o valor padrão para uma variável que pode ser nula
Ele diz ei, se não houver nada lá, use esse valor
É semelhante a “!=nil”

# Optional Chaining

O encadeamento opcional é a maneira pela qual tentamos recuperar valores de uma cadeia de valores opcionais
Permite que você falhe normalmente ao tentar acessar uma propriedade de um objeto que é nil

ex: `let album = albumReleased(year: 2006)?.uppercased()`

O encadeamento opcional pode ser tão longo quanto necessário

# Optional Binding


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
11. [Delegate vs Notification](#delegate-vs-notification)
12. [Class vs Struct](#class-vs-struct)
13. [Enum](#enum)
14. [Guard](#guard)
15. [Defer](#defer)
16. [MVVM](#mvvm)
17. [Dynamic Dispatch](#dynamic-dispatch)
18. [Static Dispatch](#static-dispatch)
19. [Closure](#closure)
20. [@escaping & nonescaping](#@escaping-and-nonescaping)
21. [What is "lazy"?](#what-is-lazy?)
22. [Unowned self & weak self](#unowned-self-&-weak-self)
23. [Process & Threads](#process-&-threads)
24. [Operation & GCD](#operation-&-GCD)
25. [Operation](#operation)
26. [OperationQueue](#operationQueue)
27. [GCD - Grand Center Dispatch](#GCD-grand-center-dispatch)
28. [What does a Dispatchgroup do?](#what-does-a-dispatchgroup-do?)
29. [Codable & Decodable in Swift](#codable-&-decodable-in-swift)
30. [Codable for complex JSON](#codable-for-complex-JSON)
31. [Any vs AnyObject](#any-vs-anyobject)
32. [Access Specifiers in Swift](#access-specifiers-in-swift)
33. [Generics](#generics)
34. [CoreData Stack](#coredata-stack)
35. [Why use NSFetchedResultsController?](#why-use-nsfetcherresultscontroller?)
36. [POP: Protocol Oriented Programming](#pop-protocol-oriented-programming)
37. [KVC & KVO](#kvc-&-kvo)
38. [Push Notification](#push-notification)
39. [Content Hugging & Compression resistance](#content-hugging-&-compression-resistance)
40. [Singleton](#singleton)
41. [Why Singleton is bad?](#why-singleton-is-bad?)
42. [Dependency Injection](#dependency-injection)
43. [What is ABI?](#what-is-ABI?)
44. [What is viewDidLayoutSubviews?](#what-is-viewDidLayoutSubviews?)
45. [What is loadView?](#what-is-loadView?)

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

Além do desempacotamento forçado, a vinculação opcional é uma maneira simples e recomendada de desempacotar um opcional. Você usa a ligação opcional para verificar se o opcional contém um valor ou não. Se contiver um valor, desembrulhe-o e coloque-o em uma constante ou variável temporária; Com a vinculação opcional, você está criando uma nova referência para o que acabou de desempacotar e, geralmente, essa é uma referência forte.

ex: 

```
if let constantName = someOptional {
   statements
}
```

# Delegate vs Notification

Delegates: usado em comunicação um para um
Notication: usado em comunicação um para vários

# Class vs Struct

Class: tipo de referência, significa que qualquer alteração em uma referência afetará outras referências também;
Struct: tipo de valor, significa que as alterações em um valor não afetarão os outros

ex:

```
class SomeClass {
	var name: String
		init(name: String) {
			self.name = name
		}
}

Var aClass = SomeClass(name: “”Bob)
Var bClass = aClass // aClass and bClass now reference the same instance!
bClass.name = “Sue”
print(aClass.name) //“Sue” print(bClass.name) //“Sue”
```

```
struct SomeStruct {
	var name: string
		init(name: String) {
			self.name = name
		}
}

var aStruct = SomeStruct(name: “Bob”)
var bStruct = aStruct // aStruct and bStruct now reference the same instance
bStruct.name = “Sue” 
print(aStruct.name) // “Bob”
print(bStruct.name) // “Sue”
```

# Enum

Grupo de valores relacionados

Raw = valores definidos no Enum

```
Enum Directions: Int {
  case up = 1
	case down
	case left	
  case right
}
```

Associated = Passagem de parametrôs pelo o Enum

```
Enum ExampleAssociation {
	case name(String)
}
```

# Guard

Fornece saída antecipada e não permite nenhum código se a condição não for verdadeira

# DEFER

A instrução Defer é usada para executar um trecho de código exatamente antes da execução sair do escopo recente;
A instrução defer é executada após o retorno!
A instrução defer é executada independentemente de como você sai

```
Func deferEx() {	
  print(“”beginning)	
  var value: String?	
  defer {		
    if let v = value {			
      print(“Ending execution of \(v)”)		
      }	
    }
	value = “defer function”	
  print(“Ending”)
}
```

# MVVM

No MVC - View envia eventos para o Controller, o controller então envia solicitação para model para dados e executa lógica de negócios se necessário, model notifica controller em caso de qualquer mudança de dados e controller envia dados para View to presentMVC - Resultou em massivo view controller que eram difíceis de administrar;
No MVVM - View Controller e View são combinados para se tornarem “View” 
E mais uma camada é adicionada chamada “ViewModel”, essa nova camada se comunicará com o modelo e processará os dados e executará alguma lógica de negócios se necessário e enviará os dados finais para o ViewController que só é necessário para atualizar a interface do usuário.

# Dynamic Dispatch

O despacho dinâmico é o processo de selecionar qual implementação de uma operação polimórfica (método ou função) chamar em tempo de execução;
Por exemplo, se uma subclasse substituir um método de sua superclasse, o despacho dinâmico descobre qual implementação do método precisa ser invocada, a da subclasse ou a da classe pai;
Ao aplicar o modificador de declaração “dynamic” a um membro de uma classe, você informa ao compilador que o dispatch dinâmico deve ser usado para acessar esse membro;

O modificador de declaração “Dinâmico” só pode ser usado para membros de uma classe. Estruturas e enumerações não suportam herança, o que significa que o tempo de execução não precisa descobrir qual implementação precisa usar; O Swift oferece 2 maneiras de obter dinamismo: Despacho de Tabela e Despacho de Mensagem;

Table Dispatch: Com este método, uma classe é associada a uma chamada tabela virtual que compreende uma matriz de ponteiros de função para a implementação real correspondente a essa classe. Observe que a tabela é construída em tempo de compilação. Assim, existem apenas duas instruções adicionais (ler e pular) em comparação com o despacho estático. Portanto, o despacho deve ser teoricamente bem rápido.

Message Dispatch: É o objetivo-c que fornece esse mecanismo. Toda vez que um método Objective-C é chamado, a invocação é passada para “objc_msgSend”, que trata das pesquisas. Ao contrário do despacho de tabela, o dicionário de passagem de mensagens pode ser modificado em tempo de execução, permitindo-nos ajustar os comportamentos do programa durante a execução.

# Static Dispatch

Quando algo é despachado estaticamente, estamos lidando com o cenário oposto. Com o despacho estático, o compilador de fato sabe qual propriedade ou método está sendo chamado em tempo de execução, o que aumenta o desempenho. Você pode obter despacho estático marcando uma classe base com a palavra-chave “final”. Isso permite que o compilador saiba que esta classe não pode ter nenhuma subclasse e que o método/propriedade a que você está se referindo é sua única implementação. 
Outro exemplo é a palavra-chave “static“ para definir métodos de tipo de propriedades. Esta palavra-chave é realmente a abreviação de “classe final”. Isso permite que o compilador saiba que esta é a implementação final desse método e não será substituída. Portanto, ele será despachado estaticamente.

Ao definir um método de tipo você pode marcá-lo com “classe” ou “estático”, mas o que você escolhe determina como ele será despachado.

# Closure

Closures são blocos autocontidos de funcionalidade que podem ser passados e usados em seu código;
Os fechamentos são funções sem cabeça. Closures são funções sem a palavra-chave func e o nome da função. Eles também são conhecidos como funções anônimas.

Syntax -
```
{ (parameter) -> return type in
	statement 
}
```

ex:
```
var sayHello = {(name: String) -> String in
	return “Hello \(name)” 
}
sayHello(“Richa”)

Passing inside a function syntax -

Func sayHello(name: string, closure(String) -> void) {
	closure(“Hello \(name)”)
}
sayHello(name: “Richa”) { name in 
	print(name)
}
```

# @escaping & @nonescaping

Se uma closure é passada como argumento para uma função e é invocada após o retorno da função, a closure está escapando;
É principalmente útil/necessário para chamadas de rede, você deseja que seu manipulador de conclusão viva após a instrução de retorno;
Existem muitos benefícios diferentes de fazer sem escape, ele cuidará da alocação de memória para a closure.

# What is “lazy”?

Uma propriedade armazenada lenta é uma propriedade cujo valor inicial não é calculado até a primeira vez que é usado. Você indica uma propriedade armazenada lazy escrevendo o modificador “lazy” antes de sua declaração. Se o seu aplicativo for complexo, os problemas de memória serão um dos principais desafios. Então, o desenvolvedor deve estar realmente escrevendo um código otimizado que considere alocação de memória em primeiro lugar. O desenvolvedor precisa evitar fazer um trabalho caro, a menos que seja realmente necessário. Podemos conseguir isso usando lazy;

Você não pode usar lazy com let;
Você não pode usá-lo com propriedades computadas. Pois, uma propriedade computada retorna o valor toda vez que tentamos acessá-la após executar o código dentro do bloco de computação;
Você pode usar lazy apenas com membros de struct e class;
As variáveis lazy não são inicializadas automaticamente e, portanto, não são seguras para threads.

# [unowned self] & [weak self]

A única vez em que você realmente deseja usar [unowned self] ou [weak self] é quando você pode criar um ciclo de referência forte. Um ciclo de referência forte é quando há um loop de propriedade onde os objetos acabam se possuindo (talvez por meio de terceiros) e, portanto, eles nunca serão desalocados porque ambos estão garantindo que um ao outro permaneça;

No caso de uma closure, você só precisa perceber que qualquer variável que é referenciada dentro dele, fica “propriedade” do encerramento. Enquanto o fechamento estiver por perto, esses objetos estarão garantidos. A única maneira de parar essa propriedade é usar o [unowned self] ou [weak self]. Portanto, se uma classe possui uma closure e essa closure captura uma referência forte a essa classe, você tem um ciclo de referência forte entre a closure e a classe. Isso também inclui se a classe possui algo que possui a closure;

Se self pudesse ser nulo na closure, use [weak self];
Se self nunca será nulo na closure, use [unowned self]

# Process & Threads

Um processo pode conter vários encadeamentos de execução e cada encadeamento pode executar várias tarefas, uma de cada vez;
Task: Um trabalho simples e único que precisa ser feito;
Thread: Um mecanismo fornecido pelo sistema operacional que permite que vários conjuntos de instruções operem ao mesmo tempo em um único aplicativo;
Process: Um pedaço de código executável, que pode ser composto de vários threads

# Operation & GCD

Ambos são usados para fazer qualquer tipo de operação multithread no iOS
GCD: É uma maneira leve de representar unidades de trabalho que serão executadas simultaneamente. Você não agenda essas unidades de trabalho; O sistema cuida do agendamento para você. Adicionar dependência entre blocos pode ser uma dor de cabeça. Cancelar ou suspender um bloco cria um trabalho extra para você como desenvolvedor! 
Operation: Adiciona um pouco de sobrecarga extra em comparação com o GCD, mas você pode adicionar dependência entre várias operações e reutilizá-las, cancelá-las ou suspendê-las.

Operation e OperationQueue são construídos sobre o GCD. Como regra geral, a apple recomenda usar a abstração de nível mais alto e, em seguida, descer para níveis mais baixos quando as medições mostrarem que isso é necessário.

# Operation

Operation é uma classe abstrata, projetada para subclasses. Cada subclasse representa uma tarefa específica.
Main() é o método que você substitui nas subclasses de Operação para realmente realizar o trabalho.

```
Class imageDownloader: Operation {
	let photoRecord: PhotoRecord
	init (_ photoRecord: PhotoRecord) {
		self.photoRecord = photoRecord	
	}
	override func main() {
		guard let imageData = try? Data(contentsOf: photoRecord.url) else { return }
		if !imageData.isEmpty {
			photoRecord.image = UIImage(data: imageData)
		}
	}
}
```

# OperationQueue

Uma fila que regula a execução das operações;
Uma fila de operação executa seus objetos de operação enfileirados com base em sua prioridade e prontidão. Depois de ser adicionada a uma fila de operações, uma operação permanece em sua fila até relatar que terminou com sua tarefa; 
O OperationQueue é particularmente poderoso porque permite controlar com precisão quantas operações simultâneas podem ser executadas e qual qualidade de serviço você precisa, além de permitir que você agende o trabalho usando encerramentos. Você pode até pedir à fila de operações que espere até que todas as suas operações sejam concluídas, o que facilita o agendamento.

```
let queue = OperationQueue()
	for image in images {
		queue.addOperation {
			self.process(image)
		}
	}
queue.waitUntiAllOperationsAreFinished()
```

Você pode adicionar quantas operações quiser, mas nem todas são executadas ao mesmo tempo. Em vez disso, o OperationQueue limita o número de operações com base nas condições do sistema - se for um dispositivo mais poderoso que não está fazendo muito agora, você obterá mais operações do que um dispositivo menos poderoso ou um dispositivo ocupado com outro trabalho.

# GCD - Grand Center Dispatch

É uma API de baixo nível para gerenciar operações simultâneas
DispatchQueue - 
  - Global Queue: usado para executar trabalho sem interface do usuário em segundo plano
  - Main Queue: usado para atualizar a interface do usuário após concluir o trabalho em uma tarefa em uma fila simultânea

List of priority:
- .userInteractive
- .userInitiated
- .default 
- .utility
- .background
- .unspecified

```
DispatchQueue.global(cos: .background).async {
	// Call your background task
	DispatchQueue.main.async {
		// UI updates here for task complete.
	}
}
```

# What does a DispatchGroupd do?

Digamos que você tenha várias tarefas de longa duração para executar. Depois que todos eles terminarem, você gostaria de executar mais alguma lógica. Você pode executar cada tarefa de forma sequencial, mas isso não é tão eficiente - você realmente gostaria que as tarefas anteriores fossem executadas simultaneamente. DispatchGroup permite que você faça exatamente isso.

Ex:
Você precisa executar duas chamadas de rede distintas. Somente depois que ambos retornarem, você terá os dados necessários para analisar as respostas.
Uma animação está em execução, paralela a uma longa chamada de banco de dados. Depois que ambos terminarem, você gostaria de ocultar um spinner de carregamento.

# Codable & Decodable in Swift

Torne seus tipos de dados codificáveis e decodificáveis para compatibilidade com representações externas, como JSON.
O protocolo Codadle é o novo protocolo introduzido pela Apple no Swift 4 que pode fornecer o recurso embutido Encodable e Decodable. Isso tornará a análise de JSON mais fácil.

```
Struct User: Codable {
	var userId: Int
	var id: Int
	var title: String
	var completed: Bool
}
do {
	let decoder = JSONDecoder()
	let model = try decoder.decode([User].self, from: dataResponse)
	print(model)
} catch let parsingError {
	print(“Error”, parsingError)
}
```

# Codable for complex JSON

```
Let jsonDataString = “” {
    	“status”: “success”,	
        “statusCode”: 123,	
        “document”: {		
            “count”: 1,		
            “profiles”: [{
                “name”: “Luísa”,
                “email”: “luisa@gmail.com”
		}]
	}
}“”.data(using: .utf8)!

struct Response: Codable {
	let status: String?	let statusCode: Int?	let document: Document?
}struct Document: Codable {
	let count: Int?	let profiles: [Profiles]?}

struct Profiles: Codable {
	let name: String?
	let email: String?	
}
do {
	let response = try JSONDecoder().decode(Response.self, from: jsonData)	print(response)
} catch {	
    print(error)
}
```

# Any vs AnyObject

Any pode representar uma instância de qualquer tipo, incluindo tipo de função e tipo opcional;
AnyObject pode representar uma instância de qualquer tipo de classe.

Ex:

```
Var anyArray: [Any] = [1,2, “Hello”, true]
Var myPerson: AnyObject = Person()
```

# Access Specifiers in Swift

Open e Public: pode ser acessado a partir das entidades do módulo e de qualquer entidade do módulo que importe o módulo definidor;

Public: classes e membros de classe só podem ser subclassificados e substituídos dentro do módulo de definição (destino). 

Open: classes e membros de classe podem ser subclassificados e sobrescrever dentro e fora do módulo de definição (destino). 

Internal: só pode ser acessado a partir das entidades do módulo. É o nível de acesso padrão.

Fileprivate e Private: só podem ser acessados em um escopo limitado onde você os define. 
Fileprivate: restringe o uso da entidade em seu arquivo fonte de definição.
Privado: restringe o uso da entidade à sua declaração anexa.

# Generics

O Generic permite escrever funções e tipos flexíveis e reutilizáveis que podem funcionar com qualquer tipo;
Por exemplo, os tipos de array e dicionário do swift são coleções genéricas. Você pode criar um array que contenha valores Int, ou um array que contenha valores String, ou mesmo um array para qualquer outro tipo que possa ser criado no Swift. Da mesma forma, você pode criar um dicionário para armazenar valores de qualquer tipo especificado.

Ex:
```
Func doNothing<Y>(x: T) {
	return x
}
doNothing(x: “Hello”) // Hello
doNothing(x: 123) // 123
doNothing(x: true) // true
```

# CoreData Stack

Managed Object - é uma classe ou subclasse NSManagedObject e representa um único registro de dados baseado no modelo;

Managed Object Context - é como um espaço de trabalho que contém muitos objetos gerenciados. O aplicativo pode ter muitos objetos gerenciados. Com o MOC realizamos a operação CRUD;

Managed Object Model - descreve a estrutura de dados e relacionamentos, definimos usando o editor de modelo de dados no Xcode. E este modelo é salvo como .xcdatamodelId;

Persistent Store Coordinator: mediar entre o armazenamento persistente e o modelo e contexto de dados;

ManagedObjectContext está em armazenamento persistente. O armazenamento persistente representa o arquivo real no disco com seus dados. Você pode ter vários armazenamentos persistentes. Para gerenciar o caso em que existem vários armazenamentos persistentes, existe um coordenador de armazenamento persistente;

CoreData oferece três tipos de arquivos nativos para um armazenamento persistente: binário, XML e SQLite;

Data Model - cria modelo de dados com entidade e atributos. Entidade é como classe ou tabela e atributos são como campos dessa classe ou tabela.


# Why to use NSFetchedResultsController?

Um controlador de resultados buscados gerencia os resultados de uma solicitação de busca. Ele notifica seu delegado sobre quaisquer alterações que afetem os resultados dessa solicitação de busca. Ele ainda oferece a capacidade de usar um cache na memória para melhorar o desempenho;

Embora a classe NSFetchResultsController tenha sido projetada com visualizações de tabela em mente, ela também funciona muito bem com visualizações de coleção.

# POP: Protocol Oriented Programming

Desvantagens da programação orientada a objetos. 
- Tem apenas uma herança. Se tivermos todas as hierarquias complicadas de herança, a classe inferior pode ter muitos estados desnecessários para manter. 
- usa classe que é um tipo de referência. O tipo de referência pode tornar o código inseguro. Processando a coleção de tipos de referência enquanto eles estão sendo modificados. 

Enquanto programação orientada a protocolos em Swift: 
- Pode conformar múltiplos protocolos; 
- Pode ser usado não apenas por classe, mas também por estruturas e enumerações; 
- possui extensão de protocolo que nos dá funcionalidade comum a todos os tipos que estão em conformidade com um protocolo;
- Prefere usar um tipo de valor em vez de um tipo de referência

# KVC & KVO

KVC: Adiciona significa codificação de valor-chave. É um mecanismo pelo qual as propriedades de um objeto podem ser acessadas usando strings em tempo de execução, em vez de ter que saber estaticamente os nomes das propriedades em tempo de desenvolvimento.

KVO: significa observação de valor-chave e permite que um controlador ou classe observe alterações em um valor de propriedade. No KVO, um objeto pode pedir para ser notificado de alguma propriedade específica, sempre que essa propriedade mudar de valor, o observador é automaticamente notificado das mudanças. Você pode usar KVO em Swift, mas apenas para propriedades dinâmicas da subclasse NSObject.

Ex:
KVC: `let robertLastName = self.value(forKey: “lastName”)`

KVO:
```
@objc class Person: NSObject {
	@objc dynamic var name = “Taylor Swift” 
}

Let taylor = Person()
Taylor.observe(\Person.name, options: .new) { person, change in 
	print(“I’m now called \(person.name)”)
}
````

# Push Notification

Device -> APP -> Server -> APNS

1. Registre-se para notificação por push
2. Enviar solicitação ao APNS
3. Responda com o token do dispositivo
4. O dispositivo envia token para o aplicativo
5. Envia o token do dispositivo para o servidor
6. O servidor encerra a carga útil de notificação com o token do dispositivo para APNS
7. Envia notificação ao dispositivo

Então a lista de verificação do APNS:
- Criar appId permitido com notificação push
- Criar certificado SSL com certificado válido e ID do aplicativo
- Crie um perfil de provisionamento com o mesmo certificado e certifique-se de adicionar dispositivo em caso de sandboxing (provisionamento de desenvolvimento)

# Content Hugging & Compression resistance

Hugging - o conteúdo não quer crescer
Compression Resistance - o conteúdo não quer encolher

# Singleton

O padrão singleton é um padrão muito útil. Há momentos em que você deseja garantir que apenas uma instância de uma classe seja instanciada e que seu aplicativo use apenas essa instância. Esse é o objetivo principal e único do padrão singleton. Objetos singleton podem ser acessados globalmente

Se você já trabalhou com os frameworks da Apple, é provável que já tenha usado o padrão Singleton.

Ex:
```
Let sharedURLSession = URLSession.shared
Let standardUserDefaults = UserDefaults.Standard

Class LocationManager {
	static let shared = LocationManager()
	var locationGranted: Bool?	// Initializer access level change now private init() {}
		func requestForLocation() {
		locationGranted = true
		print(“Location granted”)
	}
}
// Access class function in a single line
LocationManager.shared.requestForLocation()
```

# Why Singleton is bad?

O padrão singleton tem um efeito colateral que geralmente é o verdadeiro motivo para adotar o padrão singleton, o acesso global. Muitos desenvolvedores usam o padrão singleton para ter acesso fácil ao objeto singleton de qualquer lugar em seu projeto. Embora isso seja conveniente, essa conveniência tem um preço.

Desvantagens de usar Singleton:
- Sacrificar a transparência por conveniência: Ao usar singletons, você quase sempre sacrifica a transparência por conveniência. Como os singletons são tão convenientes e fáceis de acessar - usá-los extensivamente geralmente leva a uma manutenção muito difícil do "código espaguete" que não possui separações claras entre os objetos.
- Eles são um estado compartilhado mutável global: seu estado é compartilhado automaticamente em todo o aplicativo, e os bugs podem começar a ocorrer quando esse estado muda inesperadamente.
- Gerenciar seu ciclo de vida pode ser complicado: como os singletons estão ativos durante toda a vida útil de um aplicativo, gerenciá-los pode ser muito difícil e eles geralmente precisam contar com opcionais para acompanhar os valores.

# Dependency Injection

A cura para resolver a doença singleton é a injeção de dependência. Embora a principal vantagem do padrão singleton seja a conveniência, a vantagem mais importante da injeção de dependência é a transparência.
Se um objeto requer um objeto de usuário válido para fazer seu trabalho, esse objeto de usuário deve ser injetado como uma dependência.

Ex:

```
Class User {
	var firstName = “”
	var lastName = “”
}

Class NetworkController {
	let user: User
	init (user: user) {
		self.user = user
	}
}
```

# What is ABI?

As ABIs são importantes quando se trata de aplicativos que usam bibliotecas externas. Se um programa for criado para usar uma biblioteca específica e essa biblioteca for atualizada posteriormente, você não precisará recompilar esse aplicativo (e do ponto de vista do usuário final, talvez você não tenha o código-fonte). Se a biblioteca atualizada usar a mesma ABI, seu programa não precisará ser alterado.

# What is viewDidLayoutSubviews?

viewDidLayoutSubviews é chamado para notificar o controlador de visualização de que sua visualização acabou de apresentar suas subvisualizações.
Em outras palavras, viewDidLayoutSubviews é chamado toda vez que a exibição é atualizada, girada ou alterada ou seus limites são alterados. A palavra-chave aqui é mudança de limites.

# What is a loadView?

Apenas substitua este método se você criar suas visualizações manualmente (ou seja, NÃO storyboard). loadView() cria e instancia o UIView.

viewDidLoad() é chamado quando a visualização termina de carregar, enquanto loadView() é chamado quando a visualização começa a ser carregada.

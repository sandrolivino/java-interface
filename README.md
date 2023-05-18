# Interfaces em Java
###### DevSuperior

**Comunidade no Discord**:
https://discord.gg/SbjpsFv

Não perca as novidades:
- https://instagram.com/devsuperior.ig
- https://facebook.com/devsuperior.fb
- https://youtube.com/devsuperior
- https://twitter.com/devsuperior

Vídeo desta aula:

[![Image](https://img.youtube.com/vi/-_ObFKxG30Q/mqdefault.jpg "Vídeo no Youtube")](https://youtu.be/-_ObFKxG30Q)

## Sumário
- [O que você vai aprender](#O-que-você-vai-aprender)
- [Pré-requisitos](#pré-requisitos)
- [Enunciado do exercício](#Enunciado-do-exercício)
- [Exemplo](#Exemplo)
- [Diagramas](#Diagramas)

## Aprendizados
- Composição de entidades: no exemplo utilizado, as classes que se compõem são Contract e Installment,
onde um Contrato (Contract) pode ter um ou N Prestações (Installments), ou seja, temos que 
implementar de tal modo que Contract contenha uma lista de Installment. Ex: List<Installment> installments;
- Composição de serviços
- Interfaces: criamos a interface OnlinePaymentService que contém os métodos que as classes
de serviço que a utilizarem serão "obrigadas" a implementar

```
// Método para calcular o valor da taxa de processamento
double paymentFee(double amount);
    
// Método para calcular os juros mensais
double interest(double amount, int months);
```



- Inversão de controle / injeção de dependência: significa, na prática, que a classe ContractService,
que faz irá consumir a classe PaypalService, não o fará diretamente, ela "pedirá" que a classe que a
invocar, irá dizer qual o método de pagamento será utilizado e não necessariamente será o PayplaService,
pode ser qualquer outra que implementar a interface OnlinePaymentService (ex: GooglePay, WePay, Payline etc.)
Para isso, a classe ContractService deverá ter um construtor recebendo como parâmetro, a interface, para que,
quem a invocar, informe a forma de pagamento, invertendo assim o controle.

```
  // Construtor da classe ContractService
  public ContractService(OnlinePaymentService onlinePaymentService) {
      this.onlinePaymentService = onlinePaymentService;
  }
  
  // Classe principal Program, invocando ContractService. Inversão de controle. 
  ContractService cs = new ContractService(new PaypalService());
```

## Pré-requisitos

- Lógica de programação
- OOP básica
  - Classes, atributos, métodos, objetos
  - Construtores, encapsulamento
  - List
  - Herança e polimorfismo

## Enunciado do exercício

Uma empresa deseja automatizar o processamento de seus contratos. O processamento de um contrato consiste em gerar as parcelas a serem pagas para aquele contrato, com base no número de meses desejado.

A empresa utiliza um serviço de pagamento online para realizar o pagamento das parcelas. Os serviços de pagamento online tipicamente cobram um juro mensal, bem como uma taxa por pagamento. Por enquanto, o serviço contratado pela empresa é o do Paypal, que aplica juros simples de 1% a cada parcela, mais uma taxa de pagamento de 2%.

Fazer um programa para ler os dados de um contrato (número do contrato, data do contrato, e valor total do contrato). Em seguida, o programa deve ler o número de meses para parcelamento do contrato, e daí gerar os registros de parcelas a serem pagas (data e valor), sendo a primeira parcela a ser paga um mês após a data do contrato, a segunda parcela dois meses após o contrato e assim por diante. Mostrar os dados das parcelas na tela.

## Exemplo

![myImage](https://github.com/devsuperior/aulao008/raw/master/example.png)

### Cálculos

```
Parcela #1: 
200 + 1% * 1 = 202 
202 + 2% = 206.04
```

```
Parcela #2: 
200 + 1% * 2 = 204 
204 + 2% = 208.08
```

```
Parcela #3: 
200 + 1% * 3 = 206 
206 + 2% = 210.12
```

## Diagramas

### Entidades

![myImage](https://github.com/devsuperior/aulao008/raw/master/entities.png)

### Serviços

![myImage](https://github.com/devsuperior/aulao008/raw/master/services.png)

# 🕦 🃏 **Usando Mocks de Date.Now com Jest**

## **Descricão do problema**

Geralmente em aplicações com grande nível de testes eventualmente deparamos com a necessidade de testar alguma operação envolvendo a data atual.

Um exemplo simples é quando estamos validando se algo é maior ou menor que a data atual, como no exemplo abaixo:

```
Sistema de pagamento de boletos bancários
* Ao efetuar o pagamento, é necessário validar se o boleto está vencido ou não
* O sistema deverá retornar um erro caso ele esteja vencido
* O sistema deverá alterar o status do boleto para pago caso ele não esteja vencido
```
O sistema foi implementado da seguinte forma:
```typescript
efetuarPagamentoDeBoleto(boleto: Boleto) {
  if (boleto.dataVencimento > new Date(Date.now())) {
    throw new Error('Boleto Vencido');
  }
  boleto.setPago();
  <...>
}
```
Levando em consideração que a entidade `Boleto` possui estas propriedades;
```typescript
export class Boleto {
  private _dataVencimento: Date;
  private _isPago: boolean;
  <...>

  constructor(dados) {
    this._dataVencimento = dados.dataVencimento;
  <...>
  }

  <...>
  public get dataVencimento(): Date {
    return this._dataVencimento;
  }
  public setPago(): void {
    this._isPago = true;
  }
  <...>
}

```
Conforme a implementação acima, devemos então realizar testes unitários para validar os dois fluxos desta operação.

## **Implementação do teste unitário para a operação**

A primeira coisa que precisamos levar em consideração é que a data de hoje é diferente da de amanhã, que é diferente da de semana que vem, ano que vem e etc. 
Logo precisamos fazer com que o teste entenda que a data atual é **fixa** para podermos fazer as devidas validações.
Para isso vamos usar a operação `Jest.mock` da biblioteca [Jest](https://jestjs.io/pt-BR/).

*Então nosso mock vai ficar mais ou menos assim:*
```typescript
Date.now = jest.fn(() => new Date('2022/01/01').getTime());
```
Desta forma qualquer operação `Date.now` de agora em diante irá retornar a mesma data "2022/01/01".

Com isso podemos realizar nossos dois testes:
- Deverá alterar o status do boleto para pago caso não esteja vencido
  - Primeiramente precisamos criar um mock do nosso `Date.now` para uma data específica.
  - Depois criamos uma entidade boleto e colocamos uma data de vencimento **menor** do que a mockada no `Date.now`.
  - Em seguida executamos o método `efetuarPagamentoDeBoleto` e nenhum erro deverá acontecer.
- Deverá retornar um erro caso o boleto esteja vencido
  - Primeiramente precisamos criar um mock do nosso `Date.now` para uma data específica.
  - Depois criamos uma entidade boleto e colocamos uma data de vencimento **maior** do que a mockada no `Date.now`.
  - Em seguida executamos o método `efetuarPagamentoDeBoleto` e a aplicação deverá retornar um erro.

*A implementação deste teste unitário completo será mais ou menos:*
```typescript
describe('Teste operação efetuar pagamento de boleto', () => {
  it('Deverá alterar o status do boleto para pago caso não esteja vencido', () => {
    const dateMock = (Date.now = jest.fn(() =>
      new Date('2022/01/01').getTime()
    ));

    const boleto = new Boleto({
      dataVencimento: new Date('2020/01/01'),
    });

    expect(() => efetuarPagamentoDeBoleto(boleto)).not.toThrow();
    dateMock.mockClear();
  });
  it('Deverá retornar um erro caso o boleto esteja vencido', () => {
    const dateMock = (Date.now = jest.fn(() =>
      new Date('2019/01/01').getTime()
    ));

    const boleto = new Boleto({
      dataVencimento: new Date('2020/01/01'),
    });
    
    expect(() => efetuarPagamentoDeBoleto(boleto)).toThrow(new Error('Boleto Vencido'));
    dateMock.mockClear();
  });
});

```
*👮 Polícia da boa prática 👮*
*⚠️ Sempre que fizermos um mock qualquer em um teste unitário, é recomendado limpar este mock após a execução do teste. Acima usamos a função `mockClear()` da referência do teste⚠️*

## **Considerações**
Esta forma de realizar mocks em `Date` só funciona com a função estática `Date.Now` do javascript, caso a implementação esteja como `new Date()`, vale considerar um refactor na operação para adicionar o `Date.now()` dentro dela ;).

## **Conclusão**

Usar a estratégia de criar um mock em cima do `Date.now` é simples e facilita bastante a vida nos demais testes em casos de validação com a data atual.

**Referências:** Este artigo foi construído principalmente a partir da experiência pessoal do contribuinte. Mas segue um link útil com várias formas de fazer este tipo de operação https://jestjs.io/pt-BR/docs/mock-functions
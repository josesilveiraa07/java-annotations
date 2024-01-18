Os pilares da OOP são:
- Encapsulamento
- Herança
- Polimorfismo

**Definição:**
Polimorfismo é o recurso que permite que variáveis do tipo mais genérico possam apontar para objetos de tipos específicos diferentes, tendo assim outro comportamento de acordo com o tipo instanciado.

**Exemplo:**
```java
Account acc1 = new Account(1, "Alex", 200.0);
Account acc2 = new SavingsAccount(2, "Bob", 500.0, 0.01);

acc1.withdraw(50.0);
acc2.withdraw(50.0);
```

**Implementação do método `withdraw` na classe `Account`:**
```java
public void withdraw(double amount) {
	this.balance -= amount + 5.0;
}
```

**Implementação do método `withdraw` na classe `SavingsAccount`:**
```java
@Override
public void withdraw(double amount) {
	this.balance -= amount;
}
```

No 1º exemplo, quando `acc1.withdraw()` for chamado, o comportamento vai ser diferente (haverá uma taxa de 5.0 unidades no saque) do que quando `acc2.withdraw()` for chamado, sem qualquer tipo de taxa.

Em suma, polimorfismo (muitas formas) é quando uma variável de mesmo tipo tem comportamentos diferentes dentro de seus construtores ou métodos, baseando-se apenas em nos seus valores.
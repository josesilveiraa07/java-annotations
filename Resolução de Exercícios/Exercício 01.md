Este é um execício que aborda diversos conceitos de OOP:
- Encapsulamento
- Herança
- Sobreposições (overriding)
- Polimorfismo

## **Enunciado:**
Uma empresa possui funcionários próprios e terceirizados. Para cada funcionário, deseja-se registrar nome, horas trabalhadas e valor por hora. Funcionários terceirizado possuem ainda uma despesa adicional. O pagamento dos funcionários corresponde ao valor da hora multiplicado pelas horas trabalhadas, sendo que os funcionários terceirizados ainda recebem um bônus correspondente a 110% de sua despesa adicional. Fazer um programa para ler os dados de N funcionários (N fornecido pelo usuário) e armazená-los em uma lista. Depois de ler todos os dados, mostrar nome e pagamento de cada funcionário na mesma ordem em que foram digitados.

## Exemplo em execução:
![[Pasted image 20240117211550.png]]

Para resolver esse exercício, devemos fazer o seguinte:
- [x] Implementar a entidade `Employee`
- [x] Implementar a entidade `OutsourcedEmployee`, que herda a classe `Employee`
- [x] Implementar o campo `additionalCharge` na classe `OutsourcedEmployee`
- [x] Sobrepor o método `payment()` na classe `OutsourcedEmployee`, considerando os 110% de adicional
- [x] Implementar a interface em texto para criação de `Employee`s.

## Resolução:
- Classe `Employee`:
```java
public class Employee {  
    private String name;  
    protected Integer hours;  
    protected Double valuePerHour;  
  
    public Employee() {
    }  
  
    public Employee(String name, Integer hours, Double valuePerHour) {
        this.name = name;  
        this.hours = hours;  
        this.valuePerHour = valuePerHour;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public Integer getHours() {  
        return hours;  
    }  
  
    public void setHours(Integer hours) {  
        this.hours = hours;  
    }  
  
    public Double getValuePerHour() {  
        return valuePerHour;  
    }  
  
    public void setValuePerHour(Double valuePerHour) {  
        this.valuePerHour = valuePerHour;  
    }  
  
    public Double payment() {  
        return this.valuePerHour * this.hours;  
    }  
}
```

- Classe `OutsourcedEmployee`:
```java
public class OutsourcedEmployee extends Employee {  
    private Double additionalCharge;  
  
    public OutsourcedEmployee() {  
        super();  
    }  
  
    public OutsourcedEmployee(String name, Integer hours, Double valuePerHour, Double additionalCharge) {  
        super(name, hours, valuePerHour);  
        this.additionalCharge = additionalCharge;  
    }  
  
    public Double getAdditionalCharge() {  
        return additionalCharge;  
    }  
  
    public void setAdditionalCharge(Double additionalCharge) {  
        this.additionalCharge = additionalCharge;  
    }  
  
    @Override  
    public Double payment() {  
        double bonus = this.additionalCharge + this.additionalCharge * 0.1;  
  
        return this.valuePerHour * this.hours + bonus;  
    }  
}
```

Note que sobrepomos o método `payment` nessa classe, considerando os 110% de valor adicional que os trabalhadores terceirizados tem na hora do pagamento.


Agora, podemos finalmente implementar a interface em texto exemplificada no programa em execução.

```java
public static void main(String[] args) {  
    Locale.setDefault(Locale.US);  
    Scanner sc = new Scanner(System.in);  
  
    System.out.print("Enter the number of employees: ");  
    int employeesAmount = sc.nextInt();  
  
    List<Employee> employees = new ArrayList<>();  
  
    for (int i = 0; i < employeesAmount; i++) {  
        System.out.printf("Employee #%d data:%n", i + 1);  
  
        System.out.print("Outsourced (y/n)? ");  
        char outsourced = sc.next().charAt(0);  
  
        sc.nextLine();  
  
        System.out.print("Name: ");  
        String name = sc.nextLine();  
  
        System.out.print("Hours: ");  
        int hours = sc.nextInt();  
  
        System.out.print("Value per hour: ");  
        double valuePerHour = sc.nextDouble();  
  
        if (outsourced == 'y') {  
            System.out.print("Additional charge: ");  
            double additionalCharge = sc.nextDouble();  
  
            employees.add(new OutsourcedEmployee(name, hours, valuePerHour, additionalCharge));  
        } else {  
            employees.add(new Employee(name, hours, valuePerHour));  
        }  
    }  
  
    System.out.println();  
  
    System.out.println("PAYMENTS:");  
  
    for (Employee employee : employees) {  
        System.out.printf("%s - $ %.2f%n", employee.getHours(), employee.payment());  
    }  
  
    sc.close();  
}
```

Polimorfismo não poderia estar mais presente nessa aplicação: como a lista `employees` é uma instância do tipo `List<Employee>`, estamos instanciando uma lista do tipo mais genérico possível da nossa entidade `Employee`, e estamos adicionando ou um `Employee` ou um `OutsourcedEmployee` à essa lista. O compilador só sabe distinguir isso em tempo de execução, já que a lista é do tipo `Employee`. Por fim, chamamos o método `payment()`, que varia de acordo com o tipo da instância de `Employee`.
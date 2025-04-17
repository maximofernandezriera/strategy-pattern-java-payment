# Ejemplo sencillo de patron estrategia en Java aplicado en una pasarela de pago.

## Introducción
El patrón de estrategia es un patrón de diseño de comportamiento que permite definir una familia de algoritmos, encapsular cada uno de ellos y hacerlos intercambiables. Este patrón permite que el algoritmo varíe independientemente de los clientes que lo utilicen. En este ejemplo, aplicamos el patrón de estrategia a una pasarela de pago.

## Beneficios del Patrón Estrategia
- **Flexibilidad**: Permite cambiar el algoritmo o estrategia en tiempo de ejecución.
- **Reutilización de código**: Las estrategias pueden ser reutilizadas en diferentes contextos.
- **Mantenimiento**: Facilita el mantenimiento y la extensión del código.

## Prerrequisitos
- Tener instalado Java Development Kit (JDK) 8 o superior.

## Instalación
1. Clona el repositorio: `git clone https://github.com/maximofernandezriera/strategy-pattern-java-payment.git`
2. Navega al directorio del proyecto: `cd strategy-pattern-java-payment`

## Uso
1. Compila el código: `javac StrategyDemo.java`
2. Ejecuta el programa: `java StrategyDemo`

## Ejemplo de Código

```java
// Interfaz de Estrategia
interface PaymentStrategy {
    void pay(int amount); // Método que implementarán las estrategias concretas
}

// Estrategias Concretas
class CreditCardPayment implements PaymentStrategy {
    private String cardNumber;
    public CreditCardPayment(String cn){ this.cardNumber = cn; }
    @Override
    public void pay(int amount) { 
        // Implementación del pago con tarjeta de crédito
        System.out.println(amount + " pagado con tarjeta de crédito."); 
    }
}

class PaypalPayment implements PaymentStrategy {
    private String email;
    public PaypalPayment(String em){ this.email = em; }
    @Override
    public void pay(int amount) { 
        // Implementación del pago con PayPal
        System.out.println(amount + " pagado con PayPal."); 
    }
}

// Contexto
class ShoppingCart {
    private PaymentStrategy paymentStrategy;

    // Establece la estrategia de pago
    public void setPaymentStrategy(PaymentStrategy strategy) {
        this.paymentStrategy = strategy;
    }

    // Realiza el pago utilizando la estrategia establecida
    public void checkout(int amount) {
        paymentStrategy.pay(amount);
    }
}

// Cliente
public class StrategyDemo {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();
        
        // Paga con tarjeta de crédito
        cart.setPaymentStrategy(new CreditCardPayment("1224-2278-9012-1456"));
        cart.checkout(100); // Salida: 100 pagado con tarjeta de crédito.

        // Paga con PayPal
        cart.setPaymentStrategy(new PaypalPayment("maximo@fernandez.com"));
        cart.checkout(50);  // Salida: 50 pagado con PayPal.
    }
}
```

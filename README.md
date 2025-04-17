# strategy-pattern-java-payment
### Finalidad: Definir una familia de algoritmos, encapsular cada uno y hacerlos intercambiables. Ejemplo sencillo aplicado en una pasarela de pago.


```
// Interfaz de Estrategia
interface PaymentStrategy {
    void pay(int amount);
}

// Estrategias Concretas
class CreditCardPayment implements PaymentStrategy {
    private String cardNumber;
    public CreditCardPayment(String cn){ this.cardNumber = cn; }
    @Override
    public void pay(int amount) { System.out.println(amount + " pagado con tarjeta de crédito."); }
}

class PaypalPayment implements PaymentStrategy {
     private String email;
    public PaypalPayment(String em){ this.email = em; }
    @Override
    public void pay(int amount) { System.out.println(amount + " pagado con PayPal."); }
}

// Contexto
class ShoppingCart {
    private PaymentStrategy paymentStrategy;

    public void setPaymentStrategy(PaymentStrategy strategy) {
        this.paymentStrategy = strategy;
    }

    public void checkout(int amount) {
        paymentStrategy.pay(amount);
    }
}

// Cliente
public class StrategyDemo {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();
        cart.setPaymentStrategy(new CreditCardPayment("1234-5678-9012-3456"));
        cart.checkout(100); // Salida: 100 pagado con tarjeta de crédito.

        cart.setPaymentStrategy(new PaypalPayment("user@example.com"));
        cart.checkout(50);  // Salida: 50 pagado con PayPal.
    }
}
```

# Guice

## Mental model

https://github.com/google/guice/wiki/MentalModel

- Guice is a map of **keys** to **providers**
    - **key**: type + optional annotation
    - **provider**: function that returns an instance of the type (`T get()`)

## Scopes

- `@Singleton` - one instance per injector
- `@RequestScoped` - one instance per HTTP request
- `@SessionScoped` - one instance per HTTP session

## Bindings

- `bind(DatabaseTransactionLog.class).to(MySqlDatabaseTransactionLog.class);`

### Binding annotations

- if there are multiple bindings (implementations) for the same type, use `@Named` or `@Qualifier`
- `@Named` is a pre-built annotation accepting the name as a parameter, ts's less to code to write but not type safe
- using `@Qualifier`:

```java

@Qualifier
@Target({FIELD, PARAMETER, METHOD})
@Retention(RUNTIME)
public @interface PayPal {
}

// in Guice module
bind(CreditCardProcessor .class).

annotatedWith(PayPal .class).

to(PayPalCreditCardProcessor .class);

// apply
@Inject
public RealBillingService(@PayPal CreditCardProcessor processor, TransactionLog transactionLog) { ...}
```

### Instance bindings

- for constants, easy to create (no dependencies) objects (like thread executors)
```java
bind(String.class).annotatedWith(Names.named("JDBC URL")).toInstance("jdbc:mysql://localhost/pizza");

// shortcut
bindConstant().annotatedWith(HttpPort.class).to(8080);
```
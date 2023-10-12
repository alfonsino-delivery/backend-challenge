## Code challenge 2: Modularità / OOP

## Scenario:

Il reparto marketing dell'azienda mette a disposizione dei clienti una serie di codici sconto al fine di promuovere la
crescita e l'uso della piattaforma.
Successivamente sorge la necessita di ottimizzare il budget allocato, richiedendo l'applicazione di filtri ai codici
sconto
in modo che siano applicabili solamente a determinate condizioni.

## Obiettivo:

Progettare e sviluppare un sistema **focalizzato sulla modularità** per la creazione e l'applicazione condizionale di
codici sconto, in modo che essi
possano essere filtrati in base a diverse condizioni relative agli ordini, al partner, al cliente e, in futuro,
potenzialmente
altre variabili.
Utilizzare le conoscenze di programmazione orientata agli oggetti, design pattern e modularità per creare un sistema
estendibile e facilmente manutenibile.

## Requisiti:

1. **Definizione dei Modelli di Base:**
    - `Order`: rappresenta un ordine con un importo totale e le relazioni a `Partner` e `Customer`.
    - `Partner`: rappresenta un partner con i dati associati.
    - `Customer`: rappresenta un cliente con i dati associati.
    - `Coupon`: rappresenta un codice sconto composto da un codice univoco e un valore di sconto applicato espresso in
      euro €.

2. **Refactoring della classe `CartHelper`:**
    - Modificare il metodo esistente `calculateTotal` della classe `CartHelper` in modo che sia possibile applicare dei
      filtri ai codici sconto.

3. **Implementazione di un Sistema di Gestione dei Codici Sconto Modulare:**
    - Ogni modulo di codice sconto può definire le proprie regole e condizioni per l'applicazione dei codici sconto.
    - Nella pratica è richiesto che i codici sconti siano applicabili soltanto se si rispettano delle condizioni:
        1. Applicabile solo per uno specifico `Partner` id.
        2. Applicabile solo per uno specifico `Customer` id.
        3. Applicabile solo per `Order` subtotal maggiore di un valore variabile.
    - È richiesto che i diversi tipi di filtri siano applicabili anche contemporaneamente, ad esempio: `filtro partner`
      **e** `filtro subtotal`

4. **Integrazione dei Moduli di Codice Sconto:**
    - Integrazione dei moduli di codice sconto nel sistema in modo che possano essere facilmente aggiunti o rimossi in
      base alle esigenze.
    - Il sistema dovrebbe essere in grado di applicare automaticamente i codici sconto in base alle condizioni
      specificate.

5. **Utilizzo di Design Pattern:**
    - Utilizzare design pattern appropriati alla risoluzione del problema.

## Indicazioni Aggiuntive:

- È preferibile l'utilizzo del framework Laravel, o in alternativa un framework a scelta libera, basandosi comunque
  sulla struttura dati proposta.
- Prestare attenzione alla progettazione delle classi, alla separazione delle responsabilità e alla modularità.
- Assicurarsi che il sistema sia altamente estendibile e che i nuovi moduli di codice sconto possano essere aggiunti
  senza impattare i moduli esistenti.

## Codice di partenza

```php
/** Esempio Order.php */
class Order extends Model
{
    protected $fillable = ['id', 'total_amount', 'partner_id', 'customer_id', 'created_at', 'updated_at', /* [...] */];

    public function partner()
    {
        return $this->belongsTo(Partner::class);
    }

    public function customer()
    {
        return $this->belongsTo(Customer::class);
    }
    
    // [...]
}
```

```php
/** Esempio Partner.php */
class Partner extends Model
{
    protected $fillable = ['id', 'business_name', 'name', /* [...] */];

    // [...]
}
```

```php
/** Esempio Customer.php */
class Customer extends Model
{
    protected $fillable = ['id', 'first_name', 'last_name', 'username', /* [...] */];

    // [...]
}
```

```php
/** Esempio Coupon.php */
class Coupon extends Model
{
    protected $fillable = ['id', 'alfanumeric_code', 'amount',  /* [...] */];

    // [...]
}
```

```php
class CartHelper
{
    // [...]
    
    public function calculateTotal(Order $order, ?Coupon $coupon = null)
    {
        // Calcola il totale iniziale utilizzando il subtotale dell'ordine
        $total = $order->subtotal;

        if ($coupon) {
        
            // TODO inserire l'ulteriore codice di controllo richiesto
        
            // Se è stato fornito un coupon valido, riduci il totale dell'ordine in base all'importo dello sconto
            $total -= $coupon->amount;
        }

        return max($total, 0);
    }
    
    // [...]
}
```
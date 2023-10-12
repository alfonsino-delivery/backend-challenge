## Code challenge 1: Ottimizzazione

## Scenario:

L'analista dell'azienda effettua *regolarmente* un'esportazione dei dati del sistema al fine di ottimizzare il business.
La costante crescita dei dati sul database tuttavia comporta un aumento lineare dei tempi di esportazione rendendo
sempre più lenta l'operazione in oggetto.

## Obiettivo:

Supponiamo di avere un'applicazione ospitata su un WebServer, in particolare un progetto **Laravel**/**PHP**, in cui
sono presenti alcuni Models tra cui:

- **Order**
- **OrderProduct**
- **Partner**
- **Customer**

Tali `Models` mappano tabelle ospitate in un cluster MySQL Master-Replica, raggiungibile in rete locale, che - in
determinate circostanze - è *particolarmente congestionata*.

Si richiede al candidato, in base ad una accurata analisi delle premesse effettuate, l'ottimizzazione delle query
generate dal
seguente snippet di codice, ponendo attenzione all'efficienza:

Di seguito alcuni snippet di riferimento:

```php
/** Esempio Order.php */
class Order extends Model
{
    protected $fillable = ['total_amount', 'partner_id', 'customer_id', 'state_id',  /* [...] */];
    
    // [...]

    public function partner()
    {
        return $this->belongsTo(Partner::class);
    }

    public function customer()
    {
        return $this->belongsTo(Customer::class);
    }

    public function orderProducts()
    {
        return $this->hasMany(OrderProduct::class);
    }
    
    // [...]
}
```

```php
/** Esempio OrderProduct.php */
class OrderProduct extends Model
{
    protected $fillable = ['title', 'description', 'quantity', 'price', 'category_title', /* [...] */];
    
    // [...]

    public function order()
    {
        return $this->belongsTo(Order::class);
    }
    
    // [...]
}

```

```php
/** Esempio Partner.php */
class Partner extends Model
{
    protected $fillable = ['id', 'public_name', 'description', 'city', 'business_name', 'hidden_at', /* [...] */];
    
    // [...]

    public function orders()
    {
        return $this->hasMany(Order::class);
    }
    
    // [...]
}
```

```php
/** Esempio Customer.php */
class Customer extends Model
{
    protected $fillable = ['email', 'username', 'first_name', 'last_name', 'date_of_birthday', 'address', 'marketing_consent', '', /* [...] */];
    
    // [...]

    public function orders()
    {
        return $this->hasMany(Order::class);
    }
    
    // [...]
}
```

```php
// [...]

$csv = Writer::createFromString('');
$csv->insert(['Order ID', 'Partner Business Name', 'Customer Email', 'Product Details']);

// Esempio di query per l'ottenimento di tutte gli ordini.
$orders = Order::all();

foreach ($orders as $order) {
    $productDetails = [];
    foreach ($order->products as $product) {
        // Eseguire operazioni sui dettagli dei prodotti
        $productDetails[] = $product->title;
    }

    // Unisci i dettagli dei prodotti in una stringa separata da virgole
    $productDetailsString = implode(', ', $productDetails);

    // Aggiungi riga al CSV
    $csv->insert([$order->id, $order->partner->business_name, $order->customer->email, $productDetailsString]);
}

// Converti il CSV in una stringa
$csvData = $csv->output();

// [...]
```
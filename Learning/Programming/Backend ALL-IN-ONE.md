#OOP #PHP #cheatsheet
# Core PHP
`bool`, `int`, `float`, `string`, `array`, `object`, `callable`, `mixed`, `resource`, `null`


# SOLID
- **Single Responsibility**: 1 class - 1 reason
- **Open/Closed**: Extendable without modifying
- **Liskov Substitution**: Child should replace parent
- **Interface Segregation**: No use - no depend (Small interfaces)
- **Dependency Inversion**: High no depend on low. Depend on abstraction

# OOP Principles
***Encapsulation*** - private/protected/public
***Abstraction*** - WHAT instead of HOW
***Inheritance*** - child extends parent
***Polymorphism*** - same interface for different types (Log to file/database)

# Magic Methods
1. `__construct()` - *constructor*
2. `__destruct()` - *destructor*
3. `__get($property)`
4. `__set($property, $value)`
5. `__call($method, $arguments)` - *non-existent method called*
6. `__callStatic($method, $args)` - *non-existent static method called*
7. `__isset($property)` 
8. `__unset($property)` - *unset() on non-visible/undefined property*
9. `__toString()` - *object is treated like a string*
10. `__invoke()` - *when an object is used as a function*
11. `__debugInfo()` - *when `var_dump()` on object*
12. `__clone()`
13. `__wakeup()` - *an object is being deserialized, so that the object may be restored to its working condition*

# Traits - use
# Interface - implements
- ***For unrelated classes*** with ***same functionality / different implementation*** 
- ***No implementation***
- Only contains ***public*** method declarations
- Class can implement ***multiple*** interfaces
- ***Enforces*** implementation
# Abstract Classes
- ***Has implementation***
- ***No concrete*** object
- Child can ***extend only one*** abstract class
- Has a ***constructor***

# PHP Features (7.4–8.x+)
```php 
// Typed Properties
class User { public int $id; }
// Arrow Functions
$names = array_map(fn($user) => $user->name, $users);
// Null Coalescing Assignment
$data['name'] ??= 'Guest';
// Match Expression (PHP 8)
echo match($statusCode) {
    200 => 'OK',
    404 => 'Not Found',
    default => 'Unknown',
};
// Constructor Property Promotion (PHP 8)
class User {
    public function __construct(
        public string $name, // automatically declares and assigns
        public int $age
    ) {}
}
```

# PSR Standards
- **PSR-1/2/12**: Coding standards (indentation, brackets, namespaces)
- **PSR-4**: Autoloading using namespaces
- **PSR-7**: HTTP request/response interfaces
- **PSR-11**: Container Interface

# include vs require
- **include:**
	- ***Optional*** files
	- ***Warning*** if no file
- **require**
	- ***Mandatory*** files
	- ***Fatal error*** if no file

***require_once 'autoload.php'*** when ***namespace + use*** is used

-----------------------
# REST API

1xx – Informational
2xx – Success
3xx – Redirection
4xx – Client Error
5xx – Server Error

(GET, HEAD, OPTIONS, TRACE, PUT, DELETE, POST, PATCH, CONNECT)

# JSON
- Limited types (string, number, boolean, null, object, array)
- No Comments Allowed
- No Complex Keys (keys **must** be strings)
- Slow if big
- Issues with number precision
- `json_decode` returns code, so safety issues

--------

# API Security
- Authentication (API keys, JWT, OAuth2, Session tokens)
- Authorization (roles/permissions **on every request**)
- API Versioning
- HTTPS Only
- Input Validation & Sanitization
- Rate Limiting & Abuse Protection
- CORS (Cross-Origin Resource Sharing)
- Error Handling (don't show details to client)
- Sensitive Data Exposure

---------------------------
# SQL JOINS

**Joins:**`INNER` / `LEFT` / `RIGHT` / `FULL OUTER` / `CROSS` / `SELF`

**INNER JOIN:**
```SQL
SELECT customers.name, orders.total
FROM customers
INNER JOIN orders ON customers.id = orders.customer_id;
```
```php
|name |total|
|Alice|100|
|Bob  |150|
|Bob  |200|
```

**RIGHT JOIN:**
```php
|name |total|
|Alice|100|
|Bob  |150|
|Bob  |200|
|NULL |300|
```

**FULL OUTER JOIN:**
```php
|name |total|
|Alice|100|
|Bob  |150|
|Bob  |200|
|Carol|NULL|
|NULL |300|
```

**CROSS JOIN:**
```php
// Every customer is paired with every order. If 3 customers and 4 orders, that’s 12 rows.
```

**SELF JOIN:**
```SQL
SELECT a.name, b.name
FROM customers a
JOIN customers b ON a.name = b.name AND a.id <> b.id;
```
```php
// Same table - same name (search for duplicates)
```


**Set operations:** `UNION`, `UNION ALL`, `INTERSECT`, `EXCEPT`

# SQL INDEXES

- Quick data access
- Uses extra storage and can slow down writes (INSERT, UPDATE, DELETE)

**Types of indexes:**
- **Single-column** - just one column
- **Composite** - multiple columns together (Good for queries filtering by several columns)
- **Unique** - all values are unique
- **Full-text** - for fast text searching (like `MATCH ... AGAINST` in MySQL)
- **Primary Key** - Every primary key is automatically indexed
- **Partial** (PostgreSQL) - Basically conditional indexing
- **Spatial Index** - location-based queries (requires spatial column type)
- **Covering** - INDEX(username, email, age)
- **Function-based** - INDEX(LOWER(email))

**CREATE INDEX:**
```SQL
-- Create a simple index
CREATE INDEX idx_users_email ON users(email);
-- Create a unique index (no duplicate values allowed)
CREATE UNIQUE INDEX idx_users_phone ON users(phone);
-- Composite index (multiple columns)
CREATE INDEX idx_orders_customer_date ON orders(customer_id, order_date);
```

**Show ALL Indexes:**
```sql
-- MySQL
SHOW INDEXES FROM users;

-- PostgreSQL
\d users
```

# SQL Transactions
```sql
START TRANSACTION;

UPDATE accounts SET balance = balance - 100 WHERE user_id = 1;
UPDATE accounts SET balance = balance + 100 WHERE user_id = 2;

COMMIT; -- If both updates succeed, save changes
-- ROLLBACK; -- If there’s an error, undo everything
```

```php
$db->beginTransaction(); // PDO in PHP

try {
    $db->exec("UPDATE accounts SET balance = balance - 100 WHERE user_id = 1");
    $db->exec("UPDATE accounts SET balance = balance + 100 WHERE user_id = 2");
    $db->commit();
} catch (Exception $e) {
    $db->rollBack();
    // handle error
}
```

# SQL Subquery
- In most cases same as JOINS
- Can be used instead of JOINS when:
	- You Only Need to Compare or Filter, Not Combine Rows
	- You Need to Calculate an Aggregate Per Row
	- You Want to Avoid Duplicate Rows
	- You Need to Check for Existence or Non-existence
	- You Need to Filter with a Calculation That’s Hard to Join

# SQL Aggregate Functions
Common functions:
- `COUNT()` — number of rows
- `SUM()` — total
- `AVG()` — average
- `MIN()` — minimum
- `MAX()` — maximum
```sql
-- Total Sales
SELECT SUM(total) AS total_sales FROM orders;
-- Result: 1000

-- Order Count Per Customer
SELECT customer_id, COUNT(*) AS order_count
FROM orders
GROUP BY customer_id;
```

-----------

# Laravel
- *Service Container, Service Providers*
- *Eloquent ORM, Relationships, Accessors*
- *Jobs, Queues, Events*
- *Middleware, Policies, Gates*

- “Batteries included”, developer-friendly.
- Opinionated, magic-heavy.
- Uses many Symfony components under the hood.

# Service Provider
- Class in Laravel where you register things for Laravel to boot up, like services, events, or custom logic.
- **Central place** for setting up stuff your app will need
- Used for:
	- Registering Third-party Services
	- Binding Interfaces to Implementations
	- Registering Singletons
	- Bootstrapping Package Services

-----------------

# Symfony
  - *DependencyInjection, Console, Messenger*
  - *Routing, Twig, Doctrine ORM*

- Older, “pure” PHP framework
- Component-based: You can use only what you need, or all of it (the full “Framework Bundle”)
- More config-driven, explicit, and convention-light
- Used as the foundation of Laravel, Drupal, and more
- Uses Twig instead of Blade (stricter)
- **Doctrine** (Data Mapper) instead of **Eloquent** (Active Record)

```php
src/       // your PHP code (controllers, entities, services)
config/    // YAML/XML/PHP config files
templates/ // Twig templates (like Blade, but stricter)
public/    // public web root (like Laravel’s public/)
bin/       // console commands (e.g., `bin/console`)
```

# Symfony Routing
Example: YAML routing:
```yaml
# config/routes.yaml
app_home:
  path: /
  controller: App\Controller\HomeController::index
```
Example: Attribute (PHP 8+):
```php
// src/Controller/HomeController.php

#[Route('/', name: 'app_home')]
public function index() { ... }
```

# Symfony Doctrine
- **Pattern:** Data Mapper.
- Entities are plain PHP objects (POPOs).
- All database operations go through a repository or the `EntityManager`.
- Repository (`findAll()`)

# Symfony Service Container (DI)
- Every controller is a service.
- Custom classes in `src/Service/` are services.
- Services are auto-wired (in most modern Symfony setups).

----------------------

# Patterns (Design Patterns)
##### Creational Design Patterns:

![[Pasted image 20250531213539.png]]
```php
interface Transport {
    public function deliver(): string;
}

class Truck implements Transport {
    public function deliver(): string {
        return "Delivered by truck";
    }
}
class Ship implements Transport {
    public function deliver(): string {
        return "Delivered by ship";
    }
}

class TransportFactory {
    public static function make(string $type): Transport {
        return match($type) {
            'truck' => new Truck(),
            'ship' => new Ship(),
            default => throw new Exception("Invalid type")
        };
    }
}

// Usage
$transport = TransportFactory::make('truck');
echo $transport->deliver();  // Delivered by truck
```

![[Pasted image 20250531213601.png]]
```php
// Product interfaces
interface Button {
    public function render(): string;
}

interface Checkbox {
    public function check(): string;
}

// Concrete products for Windows
class WindowsButton implements Button {
    public function render(): string {
        return "Windows Button";
    }
}

class WindowsCheckbox implements Checkbox {
    public function check(): string {
        return "Windows Checkbox Checked";
    }
}

// Concrete products for Mac
class MacButton implements Button {
    public function render(): string {
        return "Mac Button";
    }
}

class MacCheckbox implements Checkbox {
    public function check(): string {
        return "Mac Checkbox Checked";
    }
}

// Abstract Factory
interface GUIFactory {
    public function createButton(): Button;
    public function createCheckbox(): Checkbox;
}

// Concrete Factories
class WindowsFactory implements GUIFactory {
    public function createButton(): Button {
        return new WindowsButton();
    }
    public function createCheckbox(): Checkbox {
        return new WindowsCheckbox();
    }
}

class MacFactory implements GUIFactory {
    public function createButton(): Button {
        return new MacButton();
    }
    public function createCheckbox(): Checkbox {
        return new MacCheckbox();
    }
}

// Usage
function renderUI(GUIFactory $factory): void {
    $button = $factory->createButton();
    $checkbox = $factory->createCheckbox();
    echo $button->render() . "\n";
    echo $checkbox->check() . "\n";
}

renderUI(new MacFactory());
```

![[Pasted image 20250531213626.png]]
```php
class Logger {
    private static ?Logger $instance = null;

    private function __construct() {}   // Private constructor

    public static function getInstance(): Logger {
        if (self::$instance === null) {
            self::$instance = new Logger();
        }
        return self::$instance;
    }

    public function log(string $message): void {
        echo "[LOG]: $message\n";
    }

    private function __clone() {}
    private function __wakeup() {}
}

// Usage
$logger = Logger::getInstance();
$logger->log("System started");
```

![[Pasted image 20250531213639.png]]
```php
class User {
    public string $name;
    public ?string $email = null;
    public ?string $phone = null;

    public function __construct(string $name) {
        $this->name = $name;
    }
}

class UserBuilder {
    private User $user;

    public function __construct(string $name) {
        $this->user = new User($name);
    }

    public function withEmail(string $email): self {
        $this->user->email = $email;
        return $this;
    }

    public function withPhone(string $phone): self {
        $this->user->phone = $phone;
        return $this;
    }

    public function build(): User {
        return $this->user;
    }
}

// Usage
$user = (new UserBuilder("Alice"))
    ->withEmail("alice@example.com")
    ->withPhone("123-456")
    ->build();
```

![[Pasted image 20250531213704.png]]
```php
class User {
    public string $name;
    public string $role;

    public function __construct(string $name, string $role = 'user') {
        $this->name = $name;
        $this->role = $role;
    }

    public function __clone() {
        // Optional: deep clone logic if needed
    }
}

// Usage
$prototype = new User("Default");
$user1 = clone $prototype;
$user1->name = "Alice";

$user2 = clone $prototype;
$user2->name = "Bob";
```

#### Structural Patterns:

![[Pasted image 20250531213729.png]]
```php
// Target interface
interface PaymentGateway {
    public function pay(float $amount): string;
}

// Adaptee (incompatible interface)
class LegacyBank {
    public function makePayment(int $cents): string {
        return "Paid {$cents} cents via LegacyBank";
    }
}

// Adapter
class LegacyBankAdapter implements PaymentGateway {
    private LegacyBank $legacyBank;

    public function __construct(LegacyBank $legacyBank) {
        $this->legacyBank = $legacyBank;
    }

    public function pay(float $amount): string {
        return $this->legacyBank->makePayment((int)($amount * 100));
    }
}

// Usage
$gateway = new LegacyBankAdapter(new LegacyBank());
echo $gateway->pay(25.50);
```

![[Pasted image 20250531213755.png]]
```php
interface Notifier {
    public function send(string $message): void;
}

class BasicNotifier implements Notifier {
    public function send(string $message): void {
        echo "Sending: $message\n";
    }
}

class EmailDecorator implements Notifier {
    public function __construct(private Notifier $notifier) {}

    public function send(string $message): void {
        $this->notifier->send($message);
        echo "Also sending email: $message\n";
    }
}
class SmsDecorator implements Notifier {
    public function __construct(private Notifier $notifier) {}

    public function send(string $message): void {
        $this->notifier->send($message);
        echo "Also sending SMS: $message\n";
    }
}

// Usage
$notifier = new SmsDecorator(new EmailDecorator(new BasicNotifier()));
$notifier->send("Order confirmed");
```

![[Pasted image 20250531213808.png]]
```php
class EmailService {
    public function send(string $to, string $msg): void {
        echo "Email sent to $to: $msg\n";
    }
}
class SmsService {
    public function send(string $to, string $msg): void {
        echo "SMS sent to $to: $msg\n";
    }
}

class NotifierFacade {
    private EmailService $email;
    private SmsService $sms;

    public function __construct() {
        $this->email = new EmailService();
        $this->sms = new SmsService();
    }

    public function notify(string $to, string $msg): void {
        $this->email->send($to, $msg);
        $this->sms->send($to, $msg);
    }
}

// Usage
$notifier = new NotifierFacade();
$notifier->notify("user@example.com", "Welcome!");
```

![[Pasted image 20250531213820.png]]
```php
interface FileService {
    public function read(string $filename): string;
}

class RealFileService implements FileService {
    public function read(string $filename): string {
        echo "Reading from file: $filename\n";
        return "File content";
    }
}

class FileServiceProxy implements FileService {
    private RealFileService $realService;
    private array $cache = [];

    public function __construct(RealFileService $realService) {
        $this->realService = $realService;
    }

    public function read(string $filename): string {
        if (!isset($this->cache[$filename])) {
            $this->cache[$filename] = $this->realService->read($filename);
        }
        return $this->cache[$filename];
    }
}

// Usage
$fileService = new FileServiceProxy(new RealFileService());
echo $fileService->read("data.txt");
echo $fileService->read("data.txt"); // Cached
```

#### Behavioral Patterns:

![[Pasted image 20250531213852.png]]
```php
interface PaymentStrategy {
    public function pay(float $amount): string;
}

class CreditCardPayment implements PaymentStrategy {
    public function pay(float $amount): string {
        return "Paid $amount using Credit Card";
    }
}
class PayPalPayment implements PaymentStrategy {
    public function pay(float $amount): string {
        return "Paid $amount using PayPal";
    }
}

class Checkout {
    public function __construct(private PaymentStrategy $strategy) {}

    public function process(float $amount): void {
        echo $this->strategy->pay($amount) . "\n";
    }
}

// Usage
$checkout = new Checkout(new CreditCardPayment());
$checkout->process(99.99);

$checkout = new Checkout(new PayPalPayment());
$checkout->process(49.99);
```

![[Pasted image 20250531213904.png]]
```php
interface Observer {
    public function update(string $event): void;
}

interface Subject {
    public function attach(Observer $observer): void;
    public function detach(Observer $observer): void;
    public function notify(string $event): void;
}

class Order implements Subject {
    private array $observers = [];

    public function attach(Observer $observer): void {
        $this->observers[] = $observer;
    }

    public function detach(Observer $observer): void {
        $this->observers = array_filter($this->observers, fn($o) => $o !== $observer);
    }

    public function notify(string $event): void {
        foreach ($this->observers as $observer) {
            $observer->update($event);
        }
    }

    public function ship(): void {
        echo "Order shipped.\n";
        $this->notify("shipped");
    }
}

class EmailNotifier implements Observer {
    public function update(string $event): void {
        echo "Email: Order has been $event.\n";
    }
}
class SmsNotifier implements Observer {
    public function update(string $event): void {
        echo "SMS: Order has been $event.\n";
    }
}

// Usage
$order = new Order();
$order->attach(new EmailNotifier());
$order->attach(new SmsNotifier());
$order->ship();
```

![[Pasted image 20250531213921.png]]
```php
interface Command {
    public function execute(): void;
}

class CreateFileCommand implements Command {
    public function __construct(private string $filename) {}

    public function execute(): void {
        echo "Creating file: {$this->filename}\n";
    }
}
class DeleteFileCommand implements Command {
    public function __construct(private string $filename) {}

    public function execute(): void {
        echo "Deleting file: {$this->filename}\n";
    }
}

class FileInvoker {
    private array $commands = [];

    public function addCommand(Command $command): void {
        $this->commands[] = $command;
    }

    public function run(): void {
        foreach ($this->commands as $command) {
            $command->execute();
        }
    }
}

// Usage
$invoker = new FileInvoker();
$invoker->addCommand(new CreateFileCommand("test.txt"));
$invoker->addCommand(new DeleteFileCommand("test.txt"));
$invoker->run();
```

![[Pasted image 20250531213935.png]]
```php
interface State {
    public function proceed(OrderContext $context): void;
    public function status(): string;
}

class NewOrder implements State {
    public function proceed(OrderContext $context): void {
        $context->setState(new ProcessingOrder());
    }

    public function status(): string {
        return "New";
    }
}
class ProcessingOrder implements State {
    public function proceed(OrderContext $context): void {
        $context->setState(new ShippedOrder());
    }

    public function status(): string {
        return "Processing";
    }
}
class ShippedOrder implements State {
    public function proceed(OrderContext $context): void {
        $context->setState(new DeliveredOrder());
    }

    public function status(): string {
        return "Shipped";
    }
}
class DeliveredOrder implements State {
    public function proceed(OrderContext $context): void {
        echo "Order is already delivered.\n";
    }

    public function status(): string {
        return "Delivered";
    }
}

class OrderContext {
    private State $state;

    public function __construct() {
        $this->state = new NewOrder();
    }

    public function setState(State $state): void {
        $this->state = $state;
    }

    public function next(): void {
        $this->state->proceed($this);
    }

    public function getStatus(): string {
        return $this->state->status();
    }
}

// Usage
$order = new OrderContext();
echo $order->getStatus() . "\n";
$order->next();

echo $order->getStatus() . "\n";
$order->next();

echo $order->getStatus() . "\n";
$order->next();

echo $order->getStatus() . "\n";
$order->next(); // Already delivered
```

![[Pasted image 20250531213950.png]]
```php
interface Handler {
    public function setNext(Handler $handler): Handler;
    public function handle(string $request): ?string;
}

abstract class AbstractHandler implements Handler {
    protected ?Handler $next = null;

    public function setNext(Handler $handler): Handler {
        $this->next = $handler;
        return $handler;
    }

    public function handle(string $request): ?string {
        if ($this->next) {
            return $this->next->handle($request);
        }
        return null;
    }
}

class AuthHandler extends AbstractHandler {
    public function handle(string $request): ?string {
        if ($request === "auth") {
            return "Authenticated\n";
        }
        return parent::handle($request);
    }
}
class LogHandler extends AbstractHandler {
    public function handle(string $request): ?string {
        if ($request === "log") {
            return "Logged\n";
        }
        return parent::handle($request);
    }
}
class ValidationHandler extends AbstractHandler {
    public function handle(string $request): ?string {
        if ($request === "validate") {
            return "Validated\n";
        }
        return parent::handle($request);
    }
}

// Usage
$auth = new AuthHandler();
$log = new LogHandler();
$validate = new ValidationHandler();

$auth->setNext($log)->setNext($validate);

echo $auth->handle("log");        // Logged
echo $auth->handle("validate");   // Validated
echo $auth->handle("auth");       // Authenticated
```

![[Pasted image 20250531214009.png]]
```php
abstract class ReportGenerator {
    public function generate(): void {
        $this->fetchData();
        $this->formatData();
        $this->export();
    }

    abstract protected function fetchData(): void;
    abstract protected function formatData(): void;

    protected function export(): void {
        echo "Exporting report...\n";
    }
}

class SalesReport extends ReportGenerator {
    protected function fetchData(): void {
        echo "Fetching sales data...\n";
    }

    protected function formatData(): void {
        echo "Formatting sales data...\n";
    }
}

class InventoryReport extends ReportGenerator {
    protected function fetchData(): void {
        echo "Fetching inventory data...\n";
    }

    protected function formatData(): void {
        echo "Formatting inventory data...\n";
    }
}

// Usage
$report = new SalesReport();
$report->generate();

$report = new InventoryReport();
$report->generate();
```

#### Bonus Patterns and Principles:
#### Repository Pattern
```php
// Entity
class Product {
    public function __construct(
        public int $id,
        public string $name,
        public float $price
    ) {}
}

// Repository Interface
interface ProductRepository {
    public function find(int $id): ?Product;
    public function save(Product $product): void;
}

// Concrete Repository
class InMemoryProductRepository implements ProductRepository {
    private array $products = [];

    public function find(int $id): ?Product {
        return $this->products[$id] ?? null;
    }

    public function save(Product $product): void {
        $this->products[$product->id] = $product;
        echo "Saved product: {$product->name}\n";
    }
}

// Usage
$repo = new InMemoryProductRepository();
$product = new Product(1, "Laptop", 1200.00);
$repo->save($product);

$found = $repo->find(1);
echo "Found product: {$found->name}";
```
#### Service Layer Pattern
```php
// Entity
class Order {
    public function __construct(
        public int $id,
        public float $amount,
        public bool $paid = false
    ) {}
}

// Repository
class OrderRepository {
    private array $orders = [];

    public function find(int $id): ?Order {
        return $this->orders[$id] ?? null;
    }

    public function save(Order $order): void {
        $this->orders[$order->id] = $order;
    }
}

// Service Layer
class OrderService {
    public function __construct(private OrderRepository $repository) {}

    public function payOrder(int $orderId): void {
        $order = $this->repository->find($orderId);
        if (!$order) {
            throw new Exception("Order not found");
        }

        if ($order->paid) {
            echo "Order already paid\n";
            return;
        }

        $order->paid = true;
        $this->repository->save($order);
        echo "Order {$order->id} paid successfully\n";
    }
}

// Usage
$repo = new OrderRepository();
$order = new Order(1, 150.00);
$repo->save($order);

$service = new OrderService($repo);
$service->payOrder(1);

```














# 🧠 PHP Backend Developer Cheat sheet

## 1. Core PHP
- OOP: Classes, Interfaces, Traits, Magic Methods
- SOLID: Single Responsibility, Open/Closed, Liskov, Interface Segregation, Dependency Inversion
- PSR: 
  - PSR-1/2/12: Code Style
  - PSR-4: Autoloading
  - PSR-7: HTTP Message Interface
- Composer: `require`, `autoload`, `psr-4`

## 2. Frameworks (Laravel/Symfony)
- Laravel:
  - Service Container, Service Providers
  - Eloquent ORM, Relationships, Accessors
  - Jobs, Queues, Events
  - Middleware, Policies, Gates
- Symfony:
  - DependencyInjection, Console, Messenger
  - Routing, Twig, Doctrine ORM

## 3. API Design
- REST:
  - Resource URIs, HTTP verbs, Status Codes
  - Versioning (`/v1/products`)
- Auth:
  - JWT, OAuth2, API Key, HMAC
- Tools: Postman, Swagger/OpenAPI
- SOAP: XML WSDLs, `SoapClient`

## 4. Database (MySQL/PostgreSQL)
- Design:
  - Normalization, Indexing, Partitioning
  - EAV vs Flat Table for flexible attributes
- Queries:
  - Joins, CTEs, JSON/JSONB
  - `EXPLAIN`, `ANALYZE`
- ORM Tools:
  - Laravel Migrations
  - Doctrine Migrations

## 5. Data Handling
- File I/O: `SplFileObject`, `fopen()`, `fputcsv()`
- Streaming: Generators, Chunking
- Formats: CSV, JSON, XML
- Validation: Laravel `Validator`, XML Schema (XSD)

## 6. Performance
- Profilers: Xdebug, Blackfire, Tideways
- Caching:
  - OPcache, Redis, Laravel Cache (`remember()`)
- Queues: Redis, Horizon, RabbitMQ
- Async: Event Dispatching, Workers

## 7. Security
- Validate: `filter_var`, Laravel Form Requests
- Protect:
  - CSRF, XSS, SQL Injection
  - Laravel: `csrf_field()`, `e()`
- Auth: Laravel Sanctum, Passport
- Secrets: `.env`, `vault`, avoid hardcoding

## 8. CI/CD
- Git: Branching, PRs, tagging
- CI: GitHub Actions, GitLab CI
- Testing: PHPUnit, Pest
- Static Analysis: PHPStan, Psalm
- Docker: `Dockerfile`, `docker-compose.yml`

## 9. Architecture
- Monolith vs Microservices
- Patterns: Event-driven, CQRS, Hexagonal
- Queues: Decoupling with RabbitMQ/SQS
- Availability: Load balancers, Health checks
- Monitoring: Sentry, ELK Stack, New Relic


# Clean Code PHP

## Table of Contents

  1. [Introduction](#introduction)
  2. [Variables](#variables)
     * [Utiliser des noms de variables prononçables et significatives](#utiliser-des-noms-de-variables-prononcables-et-significatives)
     * [Utiliser le même vocabulaire pour le même type de variable](#utiliser-le-même-vocabulaire-pour-le-meme-type-de-variable)
     * [Utiliser des noms recherchables (partie 1)](#utiliser-des-noms-recherchables-partie-1)
     * [Utiliser des noms recherchables (partie 2)](#utiliser-des-noms-recherchables-partie-2)
     * [Utiliser des variables explicatives](#utiliser-des-variables-explicatives)
     * [Eviter de partir trop loin et retourner rapidement (partie 1)](#eviter-de-partir-trop-loin-et-retourner-rapidement-partie-1)
     * [Eviter de partir trop loin et retourner rapidement (partie 2)](#eviter-de-partir-trop-loin-et-retourner-rapidement-partie-2)
     * [Eviter le mapping mental](#eviter-le-mapping-mental)
     * [Ne pas ajouter pas de contexte inutile](#ne-pas-ajouter-de-contexte-inutile)
     * [Utiliser les arguments par défaut plutôt que le circuit court ou conditionnel](#utiliser-les-arguments-par-defaut-plutot-que-le-circuit-court-ou-conditionnel)
  3. [Fonctions](#fonctions)
     * [Les arguments de fonction (2 ou moins idéalement)](#les-arguments-de-fonction-2-ou-moins-idéalement)
     * [Les fonctions ne doivent faire qu'une seule action](#les-fonctions-ne-doivent-faire-qu-une-seule-action)
     * [Le nom des fonctions doit dire ce qu'elles font](#le-nom-des-fonctions-doit-dire-ce-qu-elles-font)
     * [Les fonctions doivent avoir un seul niveau d'abstraction](#les-fonctions-doivent-avoir-un-seul-niveau-d-abstraction)
     * [Ne pas utiliser les indicateurs comme paramètres de fonction](#ne-pas-utiliser-les-indicateurs-comme-parametres-de-fonction)
     * [Eviter les effets secondaires](#eviter-les-effets-secondaires)
     * [Ne pas écrire de fonctions globals](#ne-pas-ecrire-de-fonctions-globals)
     * [Ne pas utiliser le modèle Singleton](#ne-pas-utilise-le-modele-singleton)
     * [Conditions d'encapsulation](#conditions-d-encapsulation)
     * [Éviter les conditions négatives](#eviter-les-conditions-negatives)
     * [Éviter le conditionnel](#eviter-le-conditionnel)
     * [Éviter la vérification de type (partie 1)](#eviter-la-verification-de-type-partie-1)
     * [Éviter la vérification de type (partie 2)](#eviter-la-verification-de-type-partie-2)
     * [Supprimer le code inutile](#supprimer-le-code-inutile)
  4. [Objets et Structures des données](#objets-et-structures-des-donnees)
     * [Utiliser l'encapsulation d'objet](#utiliser-l-encapsulation-d-objet)
     * [Les objets doivent avoir des membres private/protected](#les-objets-doivent-avoir-des-membres-private/protected)
  5. [Classes](#classes)
     * [Privilégier la composition à l'héritage](#privilegier-la-composition-a-l-heritage)
     * [Éviter les désignations chainées](#eviter-les-designations-chainees)
  6. [SOLID](#solid)
     * [Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
     * [Open/Closed Principle (OCP)](#openclosed-principle-ocp)
     * [Liskov Substitution Principle (LSP)](#liskov-substitution-principle-lsp)
     * [Interface Segregation Principle (ISP)](#interface-segregation-principle-isp)
     * [Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)
  7. [Don’t repeat yourself (DRY)](#dont-repeat-yourself-dry)
  8. [Traductions](#traductions)

## Introduction

Software engineering principles, from Robert C. Martin's book
[*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882),
adapted for PHP. This is not a style guide. It's a guide to producing
readable, reusable, and refactorable software in PHP.
Principe de développement logiciel, du livre 
[*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) 
de Robert C.Martin, adapté pour le language PHP. Il s'agit d'un guide pour la production de logiciels
lisable, réutilisable et réfactorable en PHP.

Not every principle herein has to be strictly followed, and even fewer will be universally 
agreed upon. These are guidelines and nothing more, but they are ones codified over many 
years of collective experience by the authors of *Clean Code*.
Tous les principes n'ont pas à être strictement suivit, et certains ne seront pas reconnus universellement.
il s'agit de conseils, rien de plus, mais sont basés sur les nombreuses années d'expériences de l'auteur de *Clean Code*.

Inspired from [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)
Inspiré par [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)

Although many developers still use PHP 5, most of the examples in this article only work with PHP 7.1+.
Malgré que de nombreux développeurs utilisent encore PHP 5, la plus part des exemples dans cet article
ne fonctionneront que sur PHP 7.1+.

Étant de coutume d'utiliser des noms anglais dans le code, les noms de variables, fonctions, classes ne sont pas traduits.

## Variables

### Use meaningful and pronounceable variable names
### Utilise des noms de variables prononçables et significatives

**Bad:**
**Mauvaise pratique:**

```php
$ymdstr = $moment->format('y-m-d');
```

**Good:**
**Bonne pratique:**

```php
$currentDate = $moment->format('y-m-d');
```

**[⬆ Retour au sommaire](#table-of-contents)**
**[⬆ Retour au sommaire](#table-of-contents)**

### Use the same vocabulary for the same type of variable
### Utiliser le même vocabulaire pour le même type de variable

**Bad:**
**Mauvaise pratique:**

```php
getUserInfo();
getUserData();
getUserRecord();
getUserProfile();
```

**Good:**
**Bonne pratique:**

```php
getUser();
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Use searchable names (part 1)
### Utiliser des noms recherchables (partie 1)

We will read more code than we will ever write. It's important that the code we do write is 
readable and searchable. By *not* naming variables that end up being meaningful for 
understanding our program, we hurt our readers.
Make your names searchable.
Nous lisons plus de codes que nous en écrivons. Il est important que le code que nous écrivons 
soit lisible et recherchable. En ne nommant pas les variables de manière significative 
pour rendre notre programme compréhensible, nous heurtons nos lecteurs.
Rendez vos noms recherchables.


**Bad:**
**Mauvaise pratique:**

```php
// What the heck is 448 for?
// A quoi correspond 448 ?
$result = $serializer->serialize($data, 448);
```

**Good:**
**Bonne pratique:**

```php
$json = $serializer->serialize($data, JSON_UNESCAPED_SLASHES | JSON_PRETTY_PRINT | JSON_UNESCAPED_UNICODE);
```

### Use searchable names (part 2)
### Utiliser des noms recherchables (partie 2)

**Bad:**
**Mauvaise pratique:**

```php
// What the heck is 4 for?
// A qoui correspond 4 ?
if ($user->access & 4) {
    // ...
}
```

**Good:**
**Bonne pratique:**

```php
class User
{
    const ACCESS_READ = 1;
    const ACCESS_CREATE = 2;
    const ACCESS_UPDATE = 4;
    const ACCESS_DELETE = 8;
}

if ($user->access & User::ACCESS_UPDATE) {
    // code executé ...
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Use explanatory variables
### Utiliser des variables explicatives

**Bad:**
**Mauvaise pratique:**

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,]+,\s*(.+?)\s*(\d{5})$/';
preg_match($cityZipCodeRegex, $address, $matches);

saveCityZipCode($matches[1], $matches[2]);
```

**Not bad:**
**Pas une mauvaise pratique :**

It's better, but we are still heavily dependent on regex.
C'est mieux, mais nous dépendons encore fortement des regex.
```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,]+,\s*(.+?)\s*(\d{5})$/';
preg_match($cityZipCodeRegex, $address, $matches);

[, $city, $zipCode] = $matches;
saveCityZipCode($city, $zipCode);
```

**Good:**
**Bonne pratique:**

Decrease dependence on regex by naming subpatterns.
Diminuer la dépendance aux regex en appelant des sous-modèles.

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,]+,\s*(?<city>.+?)\s*(?<zipCode>\d{5})$/';
preg_match($cityZipCodeRegex, $address, $matches);

saveCityZipCode($matches['city'], $matches['zipCode']);
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Avoid nesting too deeply and return early (part 1)
### Éviter de partir trop loin et retourner rapidement (partie 1)

Too many if else statements can make your code hard to follow. Explicit is better
than implicit.
Beaucoup de conditions if else peuvent rendre votre code dur à comprendre.
Explicite est meilleur qu'implicite

**Bad:**
**Mauvaise pratique:**

```php
function isShopOpen($day): bool
{
    if ($day) {
        if (is_string($day)) {
            $day = strtolower($day);
            if ($day === 'friday') {
                return true;
            } elseif ($day === 'saturday') {
                return true;
            } elseif ($day === 'sunday') {
                return true;
            } else {
                return false;
            }
        } else {
            return false;
        }
    } else {
        return false;
    }
}
```

**Good:**
**Bonne pratique:**

```php
function isShopOpen(string $day): bool
{
    if (empty($day)) {
        return false;
    }

    $openingDays = [
        'friday', 'saturday', 'sunday'
    ];

    return in_array(strtolower($day), $openingDays, true);
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Avoid nesting too deeply and return early (part 2)
### Éviter de partir trop loin et retourner rapidement (partie 2)

**Bad:**
**Mauvaise pratique:**

```php
function fibonacci(int $n)
{
    if ($n < 50) {
        if ($n !== 0) {
            if ($n !== 1) {
                return fibonacci($n - 1) + fibonacci($n - 2);
            } else {
                return 1;
            }
        } else {
            return 0;
        }
    } else {
        return 'Not supported';
    }
}
```

**Good:**
**Bonne pratique:**

```php
function fibonacci(int $n): int
{
    if ($n === 0 || $n === 1) {
        return $n;
    }

    if ($n > 50) {
        throw new \Exception('Not supported');
    }

    return fibonacci($n - 1) + fibonacci($n - 2);
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Avoid Mental Mapping
### Éviter le mapping mental

Don’t force the reader of your code to translate what the variable means.
Explicit is better than implicit.
N'obligez pas le lecteur de votre code à traduire la définition de vos variables.
Explicite est plus compréhensible qu'implicite

**Bad:**
**Mauvaise pratique:**

```php
$l = ['Austin', 'New York', 'San Francisco'];

for ($i = 0; $i < count($l); $i++) {
    $li = $l[$i];
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    // Heu, que faut `$li`déjà ?
    dispatch($li);
}
```

**Good:**
**Bonne pratique:**

```php
$locations = ['Austin', 'New York', 'San Francisco'];

foreach ($locations as $location) {
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    dispatch($location);
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Don't add unneeded context
### Ne pas ajouter de contexte inutile

If your class/object name tells you something, don't repeat that in your
variable name.
Si le nom de votre classe/objet est parlant, ne le répétez pas dans vos noms de variables.

**Bad:**
**Mauvaise pratique:**

```php
class Car
{
    public $carMake;
    public $carModel;
    public $carColor;

    //...
}
```

**Good:**
**Bonne pratique:**

```php
class Car
{
    public $make;
    public $model;
    public $color;

    //...
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Use default arguments instead of short circuiting or conditionals
### Utiliser les arguments par défaut plutôt que le circuit court ou conditionnel

**Not good:**
**Mauvais pratique:**
This is not good because `$breweryName` can be `NULL`.
Ce n'est pas une bonne partique car `$breweryName` peut être `NULL`

```php
function createMicrobrewery($breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
```

**Not bad:**
**Pas une mauvaise pratique:**
This opinion is more understandable than the previous version, but it better controls the value of the variable.
C'est option est plus lisible que la version précedente, mais il est plus sur de controller la valeur de la variable.
```php
function createMicrobrewery($name = null): void
{
    $breweryName = $name ?: 'Hipster Brew Co.';
    // ...
}
```

**Good:**
**Bonne pratique:**

If you support only PHP 7+, then you can use [type hinting](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration) and be sure that the `$breweryName` will not be `NULL`.
Si seulement vous supporter  PHP7+, vous pouvez dans ce cas utiliser la [déclaration de type](http://php.net/manual/fr/functions.arguments.php#functions.arguments.type-declaration) et vous assure que `$breweryName` ne sera pas `ǸULL`.

```php
function createMicrobrewery(string $breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

## Functions
## Fonctions

### Function arguments (2 or fewer ideally)
### Les arguments de fonction (2 ou moins idéalement)

Limiting the amount of function parameters is incredibly important because it makes 
testing your function easier. Having more than three leads to a combinatorial explosion 
where you have to test tons of different cases with each separate argument.
Limiter le nombre de paramètres de fonction est incroyablement important car cela rends 
votre fonction plus facile a tester. Avoir plus de  3 paramètres conduit a un nombre croissant de tests
où vous devrez test de nombreux cas différents avec chaques arguments.

Zero arguments is the ideal case. One or two arguments is ok, and three should be avoided. 
Anything more than that should be consolidated. Usually, if you have more than two 
arguments then your function is trying to do too much. In cases where it's not, most 
of the time a higher-level object will suffice as an argument.
Zéro argument est le cas idéal. Un ou deux arguments est bon, mais trois doit être évité.
Plus d'arguments devrait être redéfini. Généralement, si vous avez plus que deux 
arguments alors votre fonction essaie de faire trop d'actions. Dans les situations où ce n'est pas le cas,
la plus part du temps l'utilisation d'un objet pourra être utilisé comme arguments.

**Bad:**
**Mauvaise pratique:**

```php
function createMenu(string $title, string $body, string $buttonText, bool $cancellable): void
{
    // ...
}
```

**Good:**
**Bonne pratique:**

```php
class MenuConfig
{
    public $title;
    public $body;
    public $buttonText;
    public $cancellable = false;
}

$config = new MenuConfig();
$config->title = 'Foo';
$config->body = 'Bar';
$config->buttonText = 'Baz';
$config->cancellable = true;

function createMenu(MenuConfig $config): void
{
    // ...
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Functions should do one thing
### Les fonctions ne doivent faire qu'une seule action

This is by far the most important rule in software engineering. When functions do more 
than one thing, they are harder to compose, test, and reason about. When you can isolate 
a function to just one action, they can be refactored easily and your code will read much 
cleaner. If you take nothing else away from this guide other than this, you'll be ahead 
of many developers.
Cela est de loin la règle la plus important en développement logiciel. Quand une fonction fait plus 
qu'une action, elle peut facilement être refactorisée et votre code sera plus lisible. Si vous ne retenez 
que cette règle, vous serez en avance sur de nombreux développeurs.

**Bad:**
**Mauvaise pratique:**
```php
function emailClients(array $clients): void
{
    foreach ($clients as $client) {
        $clientRecord = $db->find($client);
        if ($clientRecord->isActive()) {
            email($client);
        }
    }
}
```

**Good:**
**Bonne pratique:**

```php
function emailClients(array $clients): void
{
    $activeClients = activeClients($clients);
    array_walk($activeClients, 'email');
}

function activeClients(array $clients): array
{
    return array_filter($clients, 'isClientActive');
}

function isClientActive(int $client): bool
{
    $clientRecord = $db->find($client);

    return $clientRecord->isActive();
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Function names should say what they do
### Le nom des fonctions doit dire ce qu'elles font

**Bad:**
**Mauvaise pratique:**

```php
class Email
{
    //...

    public function handle(): void
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// What is this? A handle for the message? Are we writing to a file now?
// Qu'est ce que c'est ? Un handle pour un message ? Est ce qu'on écrit dans un fichier là ?
$message->handle();
```

**Good:**
**Bonne pratique:**

```php
class Email 
{
    //...

    public function send(): void
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// Clear and obvious
// Clair et compréhensible
$message->send();
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Functions should only be one level of abstraction
### Fonctions doivent avoir un seule niveau d'abstraction

When you have more than one level of abstraction your function is usually
doing too much. Splitting up functions leads to reusability and easier
testing.
Quand vous avez plus d'un niveau d'abstraction votre fonction fait généralement trop.
Découpez vos fonctions vous menes vers un code réutilisable et facilement testable.

**Bad:**
**Mauvaise pratique:**

```php
function parseBetterJSAlternative(string $code): void
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            // ...
        }
    }

    $ast = [];
    foreach ($tokens as $token) {
        // lex...
    }

    foreach ($ast as $node) {
        // parse...
    }
}
```

**Bad too:**
**Autre mauvaise pratique:**

We have carried out some of the functionality, but the `parseBetterJSAlternative()` function is still very complex and not testable.
Nous avons extériorisé certaines fonctionnalités, mais la fonction `parseBetterJSAlternative()` reste encore complexe et non testable.

```php
function tokenize(string $code): array
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            $tokens[] = /* ... */;
        }
    }

    return $tokens;
}

function lexer(array $tokens): array
{
    $ast = [];
    foreach ($tokens as $token) {
        $ast[] = /* ... */;
    }

    return $ast;
}

function parseBetterJSAlternative(string $code): void
{
    $tokens = tokenize($code);
    $ast = lexer($tokens);
    foreach ($ast as $node) {
        // parse...
    }
}
```

**Good:**
**Bonne pratique:**

The best solution is move out the dependencies of `parseBetterJSAlternative()` function.
La meilleure solution est d'extérioriser les dépendances de la fonction `parseBetterJSAlternative()`.

```php
class Tokenizer
{
    public function tokenize(string $code): array
    {
        $regexes = [
            // ...
        ];

        $statements = explode(' ', $code);
        $tokens = [];
        foreach ($regexes as $regex) {
            foreach ($statements as $statement) {
                $tokens[] = /* ... */;
            }
        }

        return $tokens;
    }
}

class Lexer
{
    public function lexify(array $tokens): array
    {
        $ast = [];
        foreach ($tokens as $token) {
            $ast[] = /* ... */;
        }

        return $ast;
    }
}

class BetterJSAlternative
{
    private $tokenizer;
    private $lexer;

    public function __construct(Tokenizer $tokenizer, Lexer $lexer)
    {
        $this->tokenizer = $tokenizer;
        $this->lexer = $lexer;
    }

    public function parse(string $code): void
    {
        $tokens = $this->tokenizer->tokenize($code);
        $ast = $this->lexer->lexify($tokens);
        foreach ($ast as $node) {
            // parse...
        }
    }
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Don't use flags as function parameters
### Ne pas utiliser les indicateurs comme paramètres de fonction

Flags tell your user that this function does more than one thing. Functions should 
do one thing. Split out your functions if they are following different code paths 
based on a boolean.
Les indicateurs signalent à vos utilisateurs que vos fonctions font plus q'une seule action.
Les fonctions ne doivent avoir qu'une seule action. Faites plusieurs fonctions si elles executent
différentes actions en fonction d'un booléan

**Bad:**
**Mauvaise pratique:**

```php
function createFile(string $name, bool $temp = false): void
{
    if ($temp) {
        touch('./temp/'.$name);
    } else {
        touch($name);
    }
}
```

**Good:**
**Bonne pratique:**

```php
function createFile(string $name): void
{
    touch($name);
}

function createTempFile(string $name): void
{
    touch('./temp/'.$name);
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Avoid Side Effects
### Éviter les effets secondaires

A function produces a side effect if it does anything other than take a value in and 
return another value or values. A side effect could be writing to a file, modifying 
some global variable, or accidentally wiring all your money to a stranger.
Une fonction produit un effet secondaire si elle fait autre chose que prendre une valeur 
et retourner une ou plusieurs autre valeur(s).Un effet secondaire peut être écrire dans un fichier,
modifier une variable global ou accidentellement virer tout votre argent à un inconnu.

Now, you do need to have side effects in a program on occasion. Like the previous 
example, you might need to write to a file. What you want to do is to centralize where 
you are doing this. Don't have several functions and classes that write to a particular 
file. Have one service that does it. One and only one.
Occasionnellement, vous aurez besoin d'effets secondaire dans un programme. Comme dans l'exemple 
précédent, vous pourriez vouloir écrire dans un fichier. Ce que vous avez à faire est centraliser
où vous ferrez tout cela. Ne créer pas plusieurs fonctions ou class qui écrivent dans un fichier particulier.
Faites un service qui execute cela, un seul.

The main point is to avoid common pitfalls like sharing state between objects without
any structure, using mutable data types that can be written to by anything, and not 
centralizing where your side effects occur. If you can do this, you will be happier 
than the vast majority of other programmers.
Le point principal est d'éviter les pièges communs tel que le partage d'état entre objets sans aucunes structures,
utilisé des données modifiables qui peuvent être écrit par n'importe qui et ne pas 
centraliser l'endroit où se produisent les effets secondaires. Si vous faites cela,
vous serez plus heureux que la majorité des autres développeurs.

**Bad:**
**Mauvaise pratique:**

```php
// Global variable referenced by following function.
// Variable global réferencé par la fonction suivante.
// If we had another function that used this name, now it'd be an array and it could break it.
// Si nous ajoutons une autre fonction qui utilise ce nom en le transformant en array, 
// Cela pourrait caser le code
$name = 'Ryan McDermott';

function splitIntoFirstAndLastName(): void
{
    global $name;

    $name = explode(' ', $name);
}

splitIntoFirstAndLastName();

var_dump($name); // ['Ryan', 'McDermott'];
```

**Good:**
**Bonne pratique:**

```php
function splitIntoFirstAndLastName(string $name): array
{
    return explode(' ', $name);
}

$name = 'Ryan McDermott';
$newName = splitIntoFirstAndLastName($name);

var_dump($name); // 'Ryan McDermott';
var_dump($newName); // ['Ryan', 'McDermott'];
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Don't write to global functions
### Ne pas écrire de fonctions globals

Polluting globals is a bad practice in many languages because you could clash with another 
library and the user of your API would be none-the-wiser until they get an exception in 
production. Let's think about an example: what if you wanted to have configuration array. 
You could write global function like `config()`, but it could clash with another library 
that tried to do the same thing.
La pollution des globals est une mauvaise pratique dans plusieurs languages car vous pouvez 
créer des bugs avec d'autres librairies et l'utilisateur de votre API ne s'en renderait compte
que lorsqu'il aura une exception en production. Prenons un exemple : et si vous vouliez un 
tableau de configuration. Vous pourriez écrire une fonction global comme `config()`, mais cela 
pourrait poser problème avec d'autre librairie qui tente de faire la même action 

**Bad:**
**Mauvaise pratique:**

```php
function config(): array
{
    return  [
        'foo' => 'bar',
    ]
}
```

**Good:**
**Bonne pratique:**

```php
class Configuration
{
    private $configuration = [];

    public function __construct(array $configuration)
    {
        $this->configuration = $configuration;
    }

    public function get(string $key): ?string
    {
        return isset($this->configuration[$key]) ? $this->configuration[$key] : null;
    }
}
```

Load configuration and create instance of `Configuration` class 
Charge configuration et crée une instance de la classe `Configuration`

```php
$configuration = new Configuration([
    'foo' => 'bar',
]);
```

And now you must use instance of `Configuration` in your application.
Et maintenant vous devez utiliser une instance de `Configuration` dans votre application

**[⬆ Retour au sommaire](#table-of-contents)**

### Don't use a Singleton pattern
### Ne pas utiliser le modèle Singleton

Singleton is an [anti-pattern](https://en.wikipedia.org/wiki/Singleton_pattern). Paraphrased from Brian Button:
 1. They are generally used as a **global instance**, why is that so bad? Because **you hide the dependencies** of your application in your code, instead of exposing them through the interfaces. Making something global to avoid passing it around is a [code smell](https://en.wikipedia.org/wiki/Code_smell).
 2. They violate the [single responsibility principle](#single-responsibility-principle-srp): by virtue of the fact that **they control their own creation and lifecycle**.
 3. They inherently cause code to be tightly [coupled](https://en.wikipedia.org/wiki/Coupling_%28computer_programming%29). This makes faking them out under **test rather difficult** in many cases.
 4. They carry state around for the lifetime of the application. Another hit to testing since **you can end up with a situation where tests need to be ordered** which is a big no for unit tests. Why? Because each unit test should be independent from the other.
Singleton est un [anti-pattern](https://fr.wikipedia.org/wiki/Singleton_(patron_de_conception)). Paraphrase de Brian Button:
 1. Ils sont généralement utilisé comme des **instance global**, pourquoi est ce si mauvais ? Parce que **vous cachez les dépendances** de votre code dans votre code, au lieu de les montrer par le biais d'interface. Faire du global pour eviter cela c'est un [code smell](https://en.wikipedia.org/wiki/Code_smell).
 2. Ils ne respectent pas le [principe de simple responsabilité](#single-responsibility-principle-srp): par le fait qu'**ils controllent leur propre création et leur cycle de vie**.
 3. Ils obligent le code à être [couplé](https://en.wikipedia.org/wiki/Coupling_%28computer_programming%29). Cela les rends **difficile à les test** dans la plus part des cas.
 4. Ils portent l'état de l'application pendant son cycle de vie. Un autre problème pour les tests car **vous pouvez vous retrouver dans des cas de tests commandés** ce qui est un gros soucis. Pourquoi ? Car chaques tests doit être indépendant d'autres.

There is also very good thoughts by [Misko Hevery](http://misko.hevery.com/about/) about the [root of problem](http://misko.hevery.com/2008/08/25/root-cause-of-singletons/).
Il y a aussi les pensés de [Misko Hevery](http://misko.hevery.com/about/) à propos du [cœur du problème](http://misko.hevery.com/2008/08/25/root-cause-of-singletons/).

**Bad:**
**Mauvaise pratique:**

```php
class DBConnection
{
    private static $instance;

    private function __construct(string $dsn)
    {
        // ...
    }

    public static function getInstance(): DBConnection
    {
        if (self::$instance === null) {
            self::$instance = new self();
        }

        return self::$instance;
    }

    // ...
}

$singleton = DBConnection::getInstance();
```

**Good:**
**Bonne pratique:**

```php
class DBConnection
{
    public function __construct(string $dsn)
    {
        // ...
    }

     // ...
}
```

Create instance of `DBConnection` class and configure it with [DSN](http://php.net/manual/en/pdo.construct.php#refsect1-pdo.construct-parameters).
Créez une instance de la classe `DBConnection` et la configurer avec les [DNS](http://php.net/manual/fr/pdo.construct.php#refsect1-pdo.construct-parameters).

```php
$connection = new DBConnection($dsn);
```

And now you must use instance of `DBConnection` in your application.
Et maintenant vous devez utiliser une instance de `DBConnection` in your application.

**[⬆ Retour au sommaire](#table-of-contents)**

### Encapsulate conditionals
### Conditions d'encapsulation

**Bad:**
**Mauvaise pratique:**

```php
if ($article->state === 'published') {
    // ...
}
```

**Good:**
**Bonne pratique:**

```php
if ($article->isPublished()) {
    // ...
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Avoid negative conditionals
### Éviter les conditions négatives

**Bad:**
**Mauvaise pratique:**

```php
function isDOMNodeNotPresent(\DOMNode $node): bool
{
    // ...
}

if (!isDOMNodeNotPresent($node))
{
    // ...
}
```

**Good:**
**Bonne pratique:**

```php
function isDOMNodePresent(\DOMNode $node): bool
{
    // ...
}

if (isDOMNodePresent($node)) {
    // ...
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Avoid conditionals
### Éviter le conditionnel

This seems like an impossible task. Upon first hearing this, most people say,
"how am I supposed to do anything without an `if` statement?" The answer is that
you can use polymorphism to achieve the same task in many cases. The second
question is usually, "well that's great but why would I want to do that?" The
answer is a previous clean code concept we learned: a function should only do
one thing. When you have classes and functions that have `if` statements, you
are telling your user that your function does more than one thing. Remember,
just do one thing.
Cela semble être une tache impossible. Après avoir entendu cela, la plupart des 
gens demandent "Comment puis je faire quoi que ce soit sans `if` ?" La réponse est
que vous pouvez utiliser le polymorphisme pour faire les même taches dans la 
plupart des cas. La seconde question est généralement, "C'est bien mais pourquoi
voudrais je faire cela ?" La réponse est un concept de code propre appris 
précédemment : une fonction ne doit faire qu'une seule tache. Quand vous avez des 
classes et fonctions qui possèdent des `if`, vous dites à vos utilisateurs que vos
fonctions font plus qu'une action. Souvenez vous, une seule action.


**Bad:**
**Mauvaise pratique:**

```php
class Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        switch ($this->type) {
            case '777':
                return $this->getMaxAltitude() - $this->getPassengerCount();
            case 'Air Force One':
                return $this->getMaxAltitude();
            case 'Cessna':
                return $this->getMaxAltitude() - $this->getFuelExpenditure();
        }
    }
}
```

**Good:**
**Bonne pratique:**

```php
interface Airplane
{
    // ...

    public function getCruisingAltitude(): int;
}

class Boeing777 implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude() - $this->getPassengerCount();
    }
}

class AirForceOne implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude();
    }
}

class Cessna implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude() - $this->getFuelExpenditure();
    }
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Avoid type-checking (part 1)
## Éviter la vérification de type (partie 1)

PHP is untyped, which means your functions can take any type of argument.
Sometimes you are bitten by this freedom and it becomes tempting to do
type-checking in your functions. There are many ways to avoid having to do this.
The first thing to consider is consistent APIs.
PHP est non-typé, cela signifie que vos fonctions peuvent accepter n'importe quel
type d'arguments. Par moment vous serrez ennuyer par cette liberté et serrez tenté
de vérifier le type dans vos fonctions. Il y a plusieurs façon d'éviter cela.
La premiere est de considérer les cohérences d'API.

**Bad:**
**Mauvaise pratique:**

```php
function travelToTexas($vehicle): void
{
    if ($vehicle instanceof Bicycle) {
        $vehicle->pedalTo(new Location('texas'));
    } elseif ($vehicle instanceof Car) {
        $vehicle->driveTo(new Location('texas'));
    }
}
```

**Good:**
**Bonne pratique:**

```php
function travelToTexas(Traveler $vehicle): void
{
    $vehicle->travelTo(new Location('texas'));
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Avoid type-checking (part 2)
## Éviter la vérification de type (partie 2)

If you are working with basic primitive values like strings, integers, and arrays,
and you use PHP 7+ and you can't use polymorphism but you still feel the need to
type-check, you should consider
[type declaration](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration)
or strict mode. It provides you with static typing on top of standard PHP syntax.
The problem with manually type-checking is that doing it will require so much
extra verbiage that the faux "type-safety" you get doesn't make up for the lost
readability. Keep your PHP clean, write good tests, and have good code reviews.
Otherwise, do all of that but with PHP strict type declaration or strict mode.
Si vous travaillez avec des type primitifs tels que texte, nombre et tableau,
et que vous utilisez PHP 7+ et que vous n'utilisé pas le polymorphisme mais 
resentez quand même le besoin de vérifier le type des paramètres vous devriez 
penser à [déclaration des types](http://php.net/manual/fr/functions.arguments.php#functions.arguments.type-declaration)
ou le mode strict. Cela vous fournit un type static en plus de la syntaxe standard
de PHP. Le problème de la vérification manuelle du typage est que cela crée plus
de code supplémentaire pour le faux "type sécurisé" que vous obtenez en vous fesant
perdre en lisibilité. Gardez votre code propre, faites de bons test, et faites de 
bonnes revues de codes. Sinon, faites tous cela mais avec la déclaration de typage
de PHP ou du mode strict. 

**Bad:**
**Mauvaise pratique:**

```php
function combine($val1, $val2): int
{
    if (!is_numeric($val1) || !is_numeric($val2)) {
        throw new \Exception('Must be of type Number');
    }

    return $val1 + $val2;
}
```

**Good:**
**Bonne pratique:**

```php
function combine(int $val1, int $val2): int
{
    return $val1 + $val2;
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Remove dead code
### Supprimer le code inutile

Dead code is just as bad as duplicate code. There's no reason to keep it in
your codebase. If it's not being called, get rid of it! It will still be safe
in your version history if you still need it.
Un code inutilisé est aussi mauvais que du code duplicer. Il n'y a aucunes raisons
d'en conserver dans votre code source. S'il n'est pas utilisé, supprimer le ! Il 
sera toujours en securité dans l'historique de votre versionning si vous en avez besoins.

**Bad:**
**Mauvaise pratique:**

```php
function oldRequestModule(string $url): void
{
    // ...
}

function newRequestModule(string $url): void
{
    // ...
}

$request = newRequestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**Good:**
**Bonne pratique:**

```php
function requestModule(string $url): void
{
    // ...
}

$request = requestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**[⬆ Retour au sommaire](#table-of-contents)**


## Objects and Data Structures
## Objets et Structures des données

### Use object encapsulation
### Utiliser l'encapsulation d'objet

In PHP you can set `public`, `protected` and `private` keywords for methods. 
Using it, you can control properties modification on an object. 
En PHP vous pouvez utiliser les mots clé `public`, `protected` and `private`
pour les méthodes. En les utilisant, vous pouvez controller les modifications
faites sur un objet.

* When you want to do more beyond getting an object property, you don't have
to look up and change every accessor in your codebase.
* Makes adding validation simple when doing a `set`.
* Encapsulates the internal representation.
* Easy to add logging and error handling when getting and setting.
* Inheriting this class, you can override default functionality.
* You can lazy load your object's properties, let's say getting it from a
server.
* Lorsque vous voulez faire plus que récuperer une propriété d'un objet, vous 
n'avez pas à rechercher et modifier chaques accesseurs de votre code source.
* Rendre l'ajout de validation simple en fessant un `set`.
* Encapsuler la représentation interne.
* Facilité d'ajouter l'enregistrement et la gestion d'erreurs lors de getter et setter.
* Hérité de cette classe, vous pouvez facilement écrasser les fonctionnalités de base.
* 

Additionally, this is part of [Open/Closed](#openclosed-principle-ocp) principle.
De plus, cela fait partie du [Open/Closed](#openclosed-principle-ocp) principe.

**Bad:**
**Mauvaise pratique:**

```php
class BankAccount
{
    public $balance = 1000;
}

$bankAccount = new BankAccount();

// Achat de chaussures...
$bankAccount->balance -= 100;
```

**Good:**
**Bonne pratique:**

```php
class BankAccount
{
    private $balance;

    public function __construct(int $balance = 1000)
    {
      $this->balance = $balance;
    }

    public function withdraw(int $amount): void
    {
        if ($amount > $this->balance) {
            throw new \Exception('Amount greater than available balance.');
        }

        $this->balance -= $amount;
    }

    public function deposit(int $amount): void
    {
        $this->balance += $amount;
    }

    public function getBalance(): int
    {
        return $this->balance;
    }
}

$bankAccount = new BankAccount();

// Achat de chaussure...
$bankAccount->withdraw($shoesPrice);

// Obtenir le solde
$balance = $bankAccount->getBalance();
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Make objects have private/protected members
### Les objets doivent avoir des membres private/protected

* `public` methods and properties are most dangerous for changes, because some outside code may easily rely on them and you can't control what code relies on them. **Modifications in class are dangerous for all users of class.**
* `protected` modifier are as dangerous as public, because they are available in scope of any child class. This effectively means that difference between public and protected is only in access mechanism, but encapsulation guarantee remains the same. **Modifications in class are dangerous for all descendant classes.**
* `private` modifier guarantees that code is **dangerous to modify only in boundaries of single class** (you are safe for modifications and you won't have [Jenga effect](http://www.urbandictionary.com/define.php?term=Jengaphobia&defid=2494196)).
* Les méthodes et proprietés `public` sont extremement dangereux pour les modification, car certains  codes externe peuvent facilement compter sur eux et vous ne pouvez pas controller quel code est relier. **Modifications dans une classe est dangereux pour tous les utilisateurs de la class.** 
* Les modificateurs `protected` sont aussi dangereux qu'en public, car ils sont accessible dans n'importe quelle classe enfant. Cela signifie que la difference entre public et protected est uniquement dans le mechanisme d'accès, mais la guarantie d'encapsulation reste la même. **Modifications dans une classe est dangereux pour tous les utilisateurs de la class.**
* Les modificateurs `private` guarantissent que le code est **dangeureux à modifier uniquement dans les limites d'une seule classe** (vous êtes sur de vos modifications et vous ne pouvez avoir d'[effet Jenga](http://www.urbandictionary.com/define.php?term=Jengaphobia&defid=2494196))

Therefore, use `private` by default and `public/protected` when you need to provide access for external classes.
En conclusion, utilisé `private` par défaut et `public/protected` quand vous devez autoriser l'accès depuis l'exterieur de la classe.

For more informations you can read the [blog post](http://fabien.potencier.org/pragmatism-over-theory-protected-vs-private.html) on this topic written by [Fabien Potencier](https://github.com/fabpot).
Pour plus d'information, vous pouvez lire le [post de blog](http://fabien.potencier.org/pragmatism-over-theory-protected-vs-private.html)sur ce sujet écrit par [Fabien Potencier](https://github.com/fabpot).

**Bad:**
**Mauvaise pratique:**

```php
class Employee
{
    public $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }
}

$employee = new Employee('John Doe');
echo 'Employee name: '.$employee->name; // Employee name: John Doe
```

**Good:**
**Bonne pratique:**

```php
class Employee
{
    private $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }

    public function getName(): string
    {
        return $this->name;
    }
}

$employee = new Employee('John Doe');
echo 'Employee name: '.$employee->getName(); // Employee name: John Doe
```

**[⬆ Retour au sommaire](#table-of-contents)**

## Classes

### Prefer composition over inheritance
### Privilégier la composition à l'héritage

As stated famously in [*Design Patterns*](https://en.wikipedia.org/wiki/Design_Patterns) by the Gang of Four,
you should prefer composition over inheritance where you can. There are lots of
good reasons to use inheritance and lots of good reasons to use composition.
The main point for this maxim is that if your mind instinctively goes for
inheritance, try to think if composition could model your problem better. In some
cases it can.
Comme expliqué dans [*Design Patterns*](https://en.wikipedia.org/wiki/Design_Patterns) par le "Gang of Four",
vous devez privilégier la composition à l'héritage quand vous le pouvez. Il y a
un bon nombre de bonne raisons d'utiliser l'héritage et un bon nombre de bonne raisons
d'utiliser la composition. Le point principal de cette maxime est que si vous partez 
instinctivement sur de l'héritage, essayez de voir si la composition ne serait pas une 
meilleure solution. Dans certains cas, cela est possible.

You might be wondering then, "when should I use inheritance?" It
depends on your problem at hand, but this is a decent list of when inheritance
makes more sense than composition:
Du coup vous devez surement vous demandez " Quand puis je utilisé l'héritage ?"
Cela dépends de votre problème, mais voici une liste correcte où l'héritage 
prends plus de sens que la composition:

1. Your inheritance represents an "is-a" relationship and not a "has-a"
relationship (Human->Animal vs. User->UserDetails).
2. You can reuse code from the base classes (Humans can move like all animals).
3. You want to make global changes to derived classes by changing a base class.
(Change the caloric expenditure of all animals when they move).
1. Votre héritage représente une relation "est un" et non une relation "a un"
(Human->Animal vs. User->UserDetails).
2. Vous pouvez réutiliser le code source de la classe mère (Humain peut se 
déplacer comme tout les animaux).
3. Vous voulez faire des mofications globals aux classes enfants en modifiant
la classe mère.( Changer les dépenses énergétiques de tous les animaux
quand ils se déplacent).

**Bad:**
**Mauvaise pratique:**

```php
class Employee 
{
    private $name;
    private $email;

    public function __construct(string $name, string $email)
    {
        $this->name = $name;
        $this->email = $email;
    }

    // ...
}

// Bad because Employees "have" tax data. 
// EmployeeTaxData is not a type of Employee
// Mauvais car Employees "ont" des données fiscals
// EmployeeTaxData n'est pas du type Employee
 
class EmployeeTaxData extends Employee 
{
    private $ssn;
    private $salary;
    
    public function __construct(string $name, string $email, string $ssn, string $salary)
    {
        parent::__construct($name, $email);

        $this->ssn = $ssn;
        $this->salary = $salary;
    }

    // ...
}
```

**Good:**
**Bonne pratique:**

```php
class EmployeeTaxData 
{
    private $ssn;
    private $salary;

    public function __construct(string $ssn, string $salary)
    {
        $this->ssn = $ssn;
        $this->salary = $salary;
    }

    // ...
}

class Employee 
{
    private $name;
    private $email;
    private $taxData;

    public function __construct(string $name, string $email)
    {
        $this->name = $name;
        $this->email = $email;
    }

    public function setTaxData(string $ssn, string $salary)
    {
        $this->taxData = new EmployeeTaxData($ssn, $salary);
    }

    // ...
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Avoid fluent interfaces
### Éviter les désignations chainée

A [Fluent interface](https://en.wikipedia.org/wiki/Fluent_interface) is an object
oriented API that aims to improve the readability of the source code by using
[Method chaining](https://en.wikipedia.org/wiki/Method_chaining).
Une [désignation chainée](https://fr.wikipedia.org/wiki/D%C3%A9signation_cha%C3%AEn%C3%A9e)
est un objet orienté API qui vise à améliorer la lisibilité du code source en 
utilisant la [méthode de chainage](https://en.wikipedia.org/wiki/Method_chaining).

While there can be some contexts, frequently builder objects, where this
pattern reduces the verbosity of the code (for example the [PHPUnit Mock Builder](https://phpunit.de/manual/current/en/test-doubles.html)
or the [Doctrine Query Builder](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/query-builder.html)),
more often it comes at some costs:
Bien qu'il puisse y avoir certains contextes, souvent des constructeurs d'objets, 
où le modèle reduits la verbosité du code ( pour exemple le [PHPUnit Mock Builder](https://phpunit.de/manual/current/en/test-doubles.html)
ou le [Doctrine Query Builder](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/query-builder.html)),
cela arrive plus souvent à certains coûts:

1. Breaks [Encapsulation](https://en.wikipedia.org/wiki/Encapsulation_%28object-oriented_programming%29)
2. Breaks [Decorators](https://en.wikipedia.org/wiki/Decorator_pattern)
3. Is harder to [mock](https://en.wikipedia.org/wiki/Mock_object) in a test suite
4. Makes diffs of commits harder to read
1. Casse [l'encapsulation](https://fr.wikipedia.org/wiki/Encapsulation_(programmation))
2. Casse [les Décorateurs](https://fr.wikipedia.org/wiki/D%C3%A9corateur_(patron_de_conception))
3. Il est plus dur de [mocker](https://fr.wikipedia.org/wiki/Mock_(programmation_orient%C3%A9e_objet))
dans une suite de tests.
4. Rends les diffs de commits difficile à lire.

For more informations you can read the full [blog post](https://ocramius.github.io/blog/fluent-interfaces-are-evil/)
on this topic written by [Marco Pivetta](https://github.com/Ocramius).
Pour plus d'informations vous pouvez lire l'intégralité de [l'article](https://ocramius.github.io/blog/fluent-interfaces-are-evil/)
sur ce sujet écrit par [Marco Pivetta](https://github.com/Ocramius).

**Bad:**
**Mauvaise pratique:**

```php
class Car
{
    private $make = 'Honda';
    private $model = 'Accord';
    private $color = 'white';

    public function setMake(string $make): self
    {
        $this->make = $make;

        // NOTE: Returning this for chaining
        // NOTE: Retourn this pour chainage
        return $this;
    }

    public function setModel(string $model): self
    {
        $this->model = $model;

        // NOTE: Returning this for chaining
        // NOTE: Retourn this pour chainage
        return $this;
    }

    public function setColor(string $color): self
    {
        $this->color = $color;

        // NOTE: Returning this for chaining
        // NOTE: Retourn this pour chainage
        return $this;
    }

    public function dump(): void
    {
        var_dump($this->make, $this->model, $this->color);
    }
}

$car = (new Car())
  ->setColor('pink')
  ->setMake('Ford')
  ->setModel('F-150')
  ->dump();
```

**Good:**
**Bonne pratique:**

```php
class Car
{
    private $make = 'Honda';
    private $model = 'Accord';
    private $color = 'white';

    public function setMake(string $make): void
    {
        $this->make = $make;
    }

    public function setModel(string $model): void
    {
        $this->model = $model;
    }

    public function setColor(string $color): void
    {
        $this->color = $color;
    }

    public function dump(): void
    {
        var_dump($this->make, $this->model, $this->color);
    }
}

$car = new Car();
$car->setColor('pink');
$car->setMake('Ford');
$car->setModel('F-150');
$car->dump();
```

**[⬆ Retour au sommaire](#table-of-contents)**

## SOLID

**SOLID** is the mnemonic acronym introduced by Michael Feathers for the first five principles named by Robert Martin, which meant five basic principles of object-oriented programming and design.
**SOLID** est le acronyme mnémonique introduit par Michael Feathers avec les cinq premiers principes nommés par Robert Martin, qui definissent les cinq principales bases de la programmation orienté objet et design.


 * [S: Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
 * [O: Open/Closed Principle (OCP)](#openclosed-principle-ocp)
 * [L: Liskov Substitution Principle (LSP)](#liskov-substitution-principle-lsp)
 * [I: Interface Segregation Principle (ISP)](#interface-segregation-principle-isp)
 * [D: Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)

### Single Responsibility Principle (SRP)

As stated in Clean Code, "There should never be more than one reason for a class
to change". It's tempting to jam-pack a class with a lot of functionality, like
when you can only take one suitcase on your flight. The issue with this is
that your class won't be conceptually cohesive and it will give it many reasons
to change. Minimizing the amount of times you need to change a class is important.
It's important because if too much functionality is in one class and you modify a piece of it,
it can be difficult to understand how that will affect other dependent modules in
your codebase.
Comme indiqué dans le Code Propre, "Il ne devrait pas avoir plus d'une raison pour une 
classe de changer". Il est tentant de confectionner une classe avec de nombreuses
fonctionnalités, comme quand on ne peut avoir qu'un seul bagage à main sur notre vol.
L'issue avec cette technique est que notre classe ne sera pas conceptuellement cohésive
et donnera plusieurs raisons de modifier cette classe. Minifier le temps que vous passez
à modifier vos classes est important. C'est important car s'il y a trop de fonctionnalités
dans une classe et vous en modifier une partie il peut être compliquer de savoir quel effect
cela aura sur les autres modules dans votre code source.

**Bad:**
**Mauvaise pratique:**

```php
class UserSettings
{
    private $user;

    public function __construct(User $user)
    {
        $this->user = $user;
    }

    public function changeSettings(array $settings): void
    {
        if ($this->verifyCredentials()) {
            // ...
        }
    }

    private function verifyCredentials(): bool
    {
        // ...
    }
}
```

**Good:**
**Bonne pratique:**

```php
class UserAuth 
{
    private $user;

    public function __construct(User $user)
    {
        $this->user = $user;
    }
    
    public function verifyCredentials(): bool
    {
        // ...
    }
}

class UserSettings 
{
    private $user;
    private $auth;

    public function __construct(User $user) 
    {
        $this->user = $user;
        $this->auth = new UserAuth($user);
    }

    public function changeSettings(array $settings): void
    {
        if ($this->auth->verifyCredentials()) {
            // ...
        }
    }
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Open/Closed Principle (OCP)

As stated by Bertrand Meyer, "software entities (classes, modules, functions,
etc.) should be open for extension, but closed for modification." What does that
mean though? This principle basically states that you should allow users to
add new functionalities without changing existing code.
Comme décrit par Bertrand Meyer, "les entités logiciel (classes, modules, fonctions,
etc.) doivent être ouverte au extension, mais fermé au modification." Qu'est ce que 
cela signifie ? Ce principe fondamental énonce que vous pouvez autoriser les utilisateurs
à ajouter des fonctionnalités sans changer le code existant. 

**Bad:**
**Mauvaise pratique:**

```php
abstract class Adapter
{
    protected $name;

    public function getName(): string
    {
        return $this->name;
    }
}

class AjaxAdapter extends Adapter
{
    public function __construct()
    {
        parent::__construct();

        $this->name = 'ajaxAdapter';
    }
}

class NodeAdapter extends Adapter
{
    public function __construct()
    {
        parent::__construct();

        $this->name = 'nodeAdapter';
    }
}

class HttpRequester
{
    private $adapter;

    public function __construct(Adapter $adapter)
    {
        $this->adapter = $adapter;
    }

    public function fetch(string $url): Promise
    {
        $adapterName = $this->adapter->getName();

        if ($adapterName === 'ajaxAdapter') {
            return $this->makeAjaxCall($url);
        } elseif ($adapterName === 'httpNodeAdapter') {
            return $this->makeHttpCall($url);
        }
    }

    private function makeAjaxCall(string $url): Promise
    {
        // request and return promise
    }

    private function makeHttpCall(string $url): Promise
    {
        // request and return promise
    }
}
```

**Good:**
**Bonne pratique:**

```php
interface Adapter
{
    public function request(string $url): Promise;
}

class AjaxAdapter implements Adapter
{
    public function request(string $url): Promise
    {
        // request and return promise
    }
}

class NodeAdapter implements Adapter
{
    public function request(string $url): Promise
    {
        // request and return promise
    }
}

class HttpRequester
{
    private $adapter;

    public function __construct(Adapter $adapter)
    {
        $this->adapter = $adapter;
    }

    public function fetch(string $url): Promise
    {
        return $this->adapter->request($url);
    }
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Liskov Substitution Principle (LSP)

This is a scary term for a very simple concept. It's formally defined as "If S
is a subtype of T, then objects of type T may be replaced with objects of type S
(i.e., objects of type S may substitute objects of type T) without altering any
of the desirable properties of that program (correctness, task performed,
etc.)." That's an even scarier definition.
C'est un terme effrayant pour un concept vraiment simple. Il est formellement 
définie comme "Si S est un sous-type de T alors les objets de type T peuvent être 
remplacés par des objets de type S(i.e., les objets de type S sont peut être des substitues
d'objets de type T) sans altérer des proprietés principales de ce programme (correction,
performance de taches, ...)." C'est une définition plutôt effrayante

The best explanation for this is if you have a parent class and a child class,
then the base class and child class can be used interchangeably without getting
incorrect results. This might still be confusing, so let's take a look at the
classic Square-Rectangle example. Mathematically, a square is a rectangle, but
if you model it using the "is-a" relationship via inheritance, you quickly
get into trouble.
La meilleur explication pour ce terme est si vous avez une classe parent et une
classe enfant, alors la class de basse et la classe enfant peuvent être interchangé 
sans avoir de resultats incorrect. Cela reste encore un peu confus, donc jetons un
oeil au classique exemple Carré-Rectangle. Mathématiquement, un carré est un rectangle,
mais si vous le modeler en utilisant la relation "est un" par héritage, vous aurez 
rapidement des erreurs.


**Bad:**
**Mauvaise pratique:**

```php
class Rectangle
{
    protected $width = 0;
    protected $height = 0;

    public function render(int $area): void
    {
        // ...
    }

    public function setWidth(int $width): void
    {
        $this->width = $width;
    }

    public function setHeight(int $height): void
    {
        $this->height = $height;
    }

    public function getArea(): int
    {
        return $this->width * $this->height;
    }
}

class Square extends Rectangle
{
    public function setWidth(int $width): void
    {
        $this->width = $this->height = $width;
    }

    public function setHeight(int $height): void
    {
        $this->width = $this->height = $height;
    }
}

/**
 * @param Rectangle[] $rectangles
 */
function renderLargeRectangles(array $rectangles): void
{
    foreach ($rectangles as $rectangle) {
        $rectangle->setWidth(4);
        $rectangle->setHeight(5);
        $area = $rectangle->getArea(); // BAD: Will return 25 for Square. Should be 20. Mauvais: Retournera 25 pour Square. Au lieu de 20
        $rectangle->render($area);
    }
}

$rectangles = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles($rectangles);
```

**Good:**
**Bonne pratique:**

```php
abstract class Shape
{
    protected $width = 0;
    protected $height = 0;

    abstract public function getArea(): int;

    public function render(int $area): void
    {
        // ...
    }
}

class Rectangle extends Shape
{
    public function setWidth(int $width): void
    {
        $this->width = $width;
    }

    public function setHeight(int $height): void
    {
        $this->height = $height;
    }

    public function getArea(): int
    {
        return $this->width * $this->height;
    }
}

class Square extends Shape
{
    private $length = 0;

    public function setLength(int $length): void
    {
        $this->length = $length;
    }

    public function getArea(): int
    {
        return pow($this->length, 2);
    }
}

/**
 * @param Rectangle[] $rectangles
 */
function renderLargeRectangles(array $rectangles): void
{
    foreach ($rectangles as $rectangle) {
        if ($rectangle instanceof Square) {
            $rectangle->setLength(5);
        } elseif ($rectangle instanceof Rectangle) {
            $rectangle->setWidth(4);
            $rectangle->setHeight(5);
        }

        $area = $rectangle->getArea(); 
        $rectangle->render($area);
    }
}

$shapes = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles($shapes);
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Interface Segregation Principle (ISP)

ISP states that "Clients should not be forced to depend upon interfaces that
they do not use." 
ISP stipule que "Les clients ne doivent pas être forcé de dépendre d'interface 
qu'il n'utilise pas."

A good example to look at that demonstrates this principle is for
classes that require large settings objects. Not requiring clients to setup
huge amounts of options is beneficial, because most of the time they won't need
all of the settings. Making them optional helps prevent having a "fat interface".
Un bon exemple pour démontrer ce principe est pour les classes qui requièrent 
de nombreux paramètres. Ne pas obliger les utilisateurs à configurer d'énormes 
quantités d'options est bénéfique, car la plus part du temps ils n'auront pas 
besoin de tous les paramètres.

**Bad:**
**Mauvaise pratique:**

```php
interface Employee
{
    public function work(): void;

    public function eat(): void;
}

class Human implements Employee
{
    public function work(): void
    {
        // ....Travail
    }

    public function eat(): void
    {
        // ...... Mange dans le bureau
    }
}

class Robot implements Employee
{
    public function work(): void
    {
        //.... travail encore plus
    }

    public function eat(): void
    {
        //.... un robot ne mange pas mais doit implémenter cette méthode
    }
}
```

**Good:**
**Bonne pratique:**

Not every worker is an employee, but every employee is a worker.
Tout travailleur n'est pas un employé mais tout employé est un travailleur.

```php
interface Workable
{
    public function work(): void;
}

interface Feedable
{
    public function eat(): void;
}

interface Employee extends Feedable, Workable
{
}

class Human implements Employee
{
    public function work(): void
    {
        // ....travail
    }

    public function eat(): void
    {
        //.... mange à la pause déjeuné
    }
}

// robot peut seulement travailler
class Robot implements Workable
{
    public function work(): void
    {
        // ....travail
    }
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

### Dependency Inversion Principle (DIP)

This principle states two essential things:
1. High-level modules should not depend on low-level modules. Both should
depend on abstractions.
2. Abstractions should not depend upon details. Details should depend on
abstractions.
Le principe décrit deux choses éssentielle :
1. Les modules de haut niveau ne doivent pas dépendre de module de bas niveau.
Les deux doivent dépendre d'abstractions.
2. Les abstractions ne doivent pas dépendre de détails. Les détails doivent
dépendre d'abstractions.

This can be hard to understand at first, but if you've worked with PHP frameworks (like Symfony), you've seen an implementation of this principle in the form of Dependency
Injection (DI). While they are not identical concepts, DIP keeps high-level
modules from knowing the details of its low-level modules and setting them up.
It can accomplish this through DI. A huge benefit of this is that it reduces
the coupling between modules. Coupling is a very bad development pattern because
it makes your code hard to refactor.
Il peut être dur à comprendre la première fois, si vous avez travaillé avec des frameworks PHP (comme Symfony), vous avez vu une implémentation de ce principe sous la form de l'Injection Dependance
(DI). Comme ils ne sont pas des concepts identique, DIP empêche ses module haut 
niveau de connaitre les details de ces modules bas niveau et les configure.
Il peut effectuer cela à travers le DI. Un important bénefice de ce principe est
que cela réduit le couplage entre modules. Le couplage est vraiment un mauvais 
modèle de développement car il rends votre code dur à reprendre.

**Bad:**
**Mauvaise pratique:**

```php
class Employee
{
    public function work(): void
    {
        // ....travail
    }
}

class Robot extends Employee
{
    public function work(): void
    {
        //.... travail plus dur
    }
}

class Manager
{
    private $employee;

    public function __construct(Employee $employee)
    {
        $this->employee = $employee;
    }

    public function manage(): void
    {
        $this->employee->work();
    }
}
```

**Good:**
**Bonne pratique:**

```php
interface Employee
{
    public function work(): void;
}

class Human implements Employee
{
    public function work(): void
    {
        // ....travail
    }
}

class Robot implements Employee
{
    public function work(): void
    {
        //.... travail plus dur
    }
}

class Manager
{
    private $employee;

    public function __construct(Employee $employee)
    {
        $this->employee = $employee;
    }

    public function manage(): void
    {
        $this->employee->work();
    }
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

## Don’t repeat yourself (DRY)

Try to observe the [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) principle.
Essayer de comprendre le principe [DRY](https://fr.wikipedia.org/wiki/Ne_vous_r%C3%A9p%C3%A9tez_pas).

Do your absolute best to avoid duplicate code. Duplicate code is bad because 
it means that there's more than one place to alter something if you need to 
change some logic.
Faites toujours de votre mieux pour ne pas duplicer votre code. Le code dupliqué 
est mauvais car cela signifie qu'il y a plus d'un endroit à modifier si vous 
changer quelques logiques.

Imagine if you run a restaurant and you keep track of your inventory: all your 
tomatoes, onions, garlic, spices, etc. If you have multiple lists that
you keep this on, then all have to be updated when you serve a dish with
tomatoes in them. If you only have one list, there's only one place to update!
Imaginez que vous tenez un restaurant et vous gardez une trace de votre inventaire:
toutes vos tomates, oignons, ails, épices, etc. Si vous avez de nombreuses listes 
qui conservent cela, vous devrez toutes les modifier dès que vous servirez un plat
avec de la tomate. Si vous n'avez qu'une liste, il n'y a qu'une seule modification 
à faire !

Oftentimes you have duplicate code because you have two or more slightly
different things, that share a lot in common, but their differences force you
to have two or more separate functions that do much of the same things. Removing 
duplicate code means creating an abstraction that can handle this set of different 
things with just one function/module/class.
Souvent vous aurez du code dupliqué car vous aurez des petites différentes actions,
qui auront beaucoup en commun, mais dont les differences vous obligerons à faire
plusieurs fonctions séparées qui feront pratiquement la même chose. Retirez le code
dupliqué signifie créer une abstraction qui gere ce lot de différences avec une 
seule classe/module/fonction. 

Getting the abstraction right is critical, that's why you should follow the
SOLID principles laid out in the [Classes](#classes) section. Bad abstractions can be
worse than duplicate code, so be careful! Having said this, if you can make
a good abstraction, do it! Don't repeat yourself, otherwise you'll find yourself 
updating multiple places anytime you want to change one thing.
Avoir la bonne abstraction est critique, c'est pourquoi vous devriez suivre les 
principes SOLID apporté dans la section [Classes](#classes). Une mauvaise abstraction
peut être pire que du code dupliqué, donc soyez prudent ! Après cela, si vous pouvez 
faire une bonne abstraction, faites le ! Ne vous répetez pas, sinon vous vous retrouverez
à modifier de nombreux endroits à chaques modifications que vous ferrez. 

**Bad:**
**Mauvaise pratique:**

```php
function showDeveloperList(array $developers): void
{
    foreach ($developers as $developer) {
        $expectedSalary = $developer->calculateExpectedSalary();
        $experience = $developer->getExperience();
        $githubLink = $developer->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}

function showManagerList(array $managers): void
{
    foreach ($managers as $manager) {
        $expectedSalary = $manager->calculateExpectedSalary();
        $experience = $manager->getExperience();
        $githubLink = $manager->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}
```

**Good:**
**Bonne pratique:**

```php
function showList(array $employees): void
{
    foreach ($employees as $employee) {
        $expectedSalary = $employee->calculateExpectedSalary();
        $experience = $employee->getExperience();
        $githubLink = $employee->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}
```

**Very good:**

It is better to use a compact version of the code.
Il est meilleur d'utiliser une version compacte du code.

```php
function showList(array $employees): void
{
    foreach ($employees as $employee) {
        render([
            $employee->calculateExpectedSalary(),
            $employee->getExperience(),
            $employee->getGithubLink()
        ]);
    }
}
```

**[⬆ Retour au sommaire](#table-of-contents)**

## Traductions

This is also available in other languages:

*  :cn: **Chinese:**
   * [php-cpm/clean-code-php](https://github.com/php-cpm/clean-code-php)
* :ru: **Russian:**
   * [peter-gribanov/clean-code-php](https://github.com/peter-gribanov/clean-code-php)
* :es: **Spanish:**
   * [fikoborquez/clean-code-php](https://github.com/fikoborquez/clean-code-php)
* :brazil: **Portuguese:**
   * [fabioars/clean-code-php](https://github.com/fabioars/clean-code-php)
   * [jeanjar/clean-code-php](https://github.com/jeanjar/clean-code-php/tree/pt-br)
* :thailand: **Thai:**
   * [panuwizzle/clean-code-php](https://github.com/panuwizzle/clean-code-php)
* :english: **En:**
   * [jupeter/clean-code-php](https://github.com/jupeter/clean-code-php)

**[⬆ Retour au sommaire](#table-of-contents)**

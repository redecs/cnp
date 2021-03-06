# CNP - Cod Numeric Personal


Librarie PHP care permite validarea si extragerea de informatii din CNP.


# Instalare

Folosind Composer:

```
composer require cpana/cnp
```

# Utilizare

In folderul src/Examples gasiti cateva exemple de utilizare.

La instantierea clasei CodNumericPersonal se trimite ca parametru sirul de caractere continand CNP-ul ce trebuie validad.

Daca nu este un CNP valid o exceptie care implementeaza interfata CPANA\CNP\Exception\CNPExceptionInterface va fi aruncata.
```php
use CPANA\CNP\CodNumericPersonal;
use CPANA\CNP\Exception\CNPExceptionInterface;

...
try {
    $cnpObj = new CodNumericPersonal($inputString);
} catch (CNPExceptionInterface $e) {
    // handle error
} 

```
Daca se doreste tratarea mai in detaliu a diferitelor erori de validare urmati exemplul de mai jos:  

```php
use CPANA\CNP\CodNumericPersonal;
use CPANA\CNP\Exception\GenericInvalidCNPException;
use CPANA\CNP\Exception\InvalidCNPLengthCNPException;
use CPANA\CNP\Exception\NonNumericValueCNPException;
use CPANA\CNP\Exception\CNPExceptionInterface;

...
try {
    $cnpObj = new CodNumericPersonal($inputString);
} catch (InvalidCNPLengthCNPException $e) {
    // Ex: Display message to user
    
} catch (NonNumericValueCNPException $e) {
    // Ex: Display message to user
    
} catch (GenericInvalidCNPException $e) {
    $code = $e->getCode();
    // take decision based on error code
    switch ($code) {
            case GenericInvalidCNPException::EXCEPTION_COUNTY:
                // take some action like  highlight wrong digits for country JJ
                echo 'Error code:'.$e->getCode().' '.$e->getMessage().PHP_EOL;
                break;
            case GenericInvalidCNPException::EXCEPTION_GENDER:
                // take some specific action ..
                break;
            case GenericInvalidCNPException::EXCEPTION_YEAR:
                // take some specific action ..
                break;
            case GenericInvalidCNPException::EXCEPTION_MONTH:
                // take some specific action ..
            case GenericInvalidCNPException::EXCEPTION_DAY:
            // take some specific action ..
                break;
        }
} catch (CNPExceptionInterface $e) {
    // do something
} catch (\Exception $e) {
    // do something
}

```

# Testare automata

Rulare teste automate:
```
./vendor/bin/phpunit tests
PHPUnit 7.5.20 by Sebastian Bergmann and contributors.

.......                                                             7 / 7 (100%)

Time: 106 ms, Memory: 4.00 MB

OK (7 tests, 7 assertions)

```

# Calitatea codului

Pentru a verifica calidatii codului paote fi folosita comanda:
```
composer lint
```

Aplicatiile folosite in detaliu:
1. PHP CS Fixer - verifica aderarea la coding stand (si repara automat abaterile)
    ```
    composer cs-fix
    composer cs-test
    ```
1. PHP CodeSniffer - partial redundant cu PHP CS Fixer, incare niste verificari care ne sunt utile.
    ```
    composer phpcs
    ```
1. PHP Mess Detector - pentru analiza calitatii codului din punct de vedere al volumului, calitatii, etc.
    ```
    composer phpmd
    ```
1. PHPStan - analiza statica, identificarea problemelor generale din cod
    ```
    composer phpstan
    ```
1. PHPUnit - testare functinala si unitara
    ```
    composer test
    ```
    Aici ar trebui sa il actualizam macar la versiunea 8 daca nu chiar 9 (10 va fi lansat curand) pentru ca versiunea 7 nu mai este suporta.

# Licenta
Acest pachet este licențiat în conformitate cu licenta [MIT](http://opensource.org/licenses/MIT).

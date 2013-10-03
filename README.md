php-trait-vs-yii-behavior
=========================

Property          | PHP Traits              | Yii Behaviors
----------------- | ----------------------- | -------------
Evaluation        | Load-time               | Run-time
Multiplicity      | One trait use per class | Many behavior attachments per instance

## Symbols

* Host/Owner class `Host`:

```php
class Host {}
```

* PHP Trait constructs `TraitA`, `TraitB`, ..., `TraitX`, ...:

```php
trait TraitX { }
```

* Yii Behavior classes `BhvrA`, `BhvrB`, ..., `BhvrX`, ...:

```php
class BhvrX extends CBehavior { }
```

## Usage

### PHP Traits

```php
class HostTrait
{
  use TraitA;
  use TraitB;
}

// Create first instance
$hostTrait1 = new HostTrait();

// Create second instance
$hostTrait2 = new HostTrait();
```

### Yii behaviors

#### Generally

```php
class HostBhvr
{
}

// Create first instance
$hostBhvr1 = new HostBhvr();
$hostBhvr1->attachBehavior('bhvr1', new Bhvr1());
$hostBhvr1->attachBehavior('bhvr2', new Bhvr2());

// Create second instance
$hostBhvr2 = new HostBhvr();
$hostBhvr2->attachBehavior('bhvr1', new Bhvr1());
$hostBhvr2->attachBehavior('bhvr2', new Bhvr2());
```

#### CModels

```php
class HostModelBhvr extends CModel
{
  public function behaviors()
  {
    return array(
      'bhvr1' => array(
        'class' => 'Bhvr1',
      ),
      'bhvr2' => array(
        'class' => 'Bhvr2',
      ),
    );
  }
}

// Create first instance
$hostModelBhvr1 = new HostModelBhvr();

// Create second instance
$hostModelBhvr2 = new HostModelBhvr();
```

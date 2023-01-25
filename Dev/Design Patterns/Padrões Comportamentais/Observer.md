Também conhecido por Listener, esse padrão é responsável por notificar um ou mais objetos quando ocorrer qualquer alteração no objeto que está sendo observado/ouvido.

Pode se classificar o objeto observado com um publisher/subject e os objetos que o observam seriam os assinantes/observers.

O objeto publisher, deverá ter um array que guardará todo os objetos que o assinam e implementar uma interface que tenha um método para adicionar um assinante, outro para remover um assinante e um método responsável por notificar todos os assinantes.

Os assinantes por sua vez, terão que implementar uma interface que tenha um método para receber as notificações do publisher.

O php possui duas interfaces nativas que representam os publishers e assinantes, a [[SplSubject]] e a [[SplObserver]]

Para implementar o padrão, primeiro criaremos nossa classe publisher implementando já a interface nativa SplSubject.

Usaremos também a classe [[SplObjectStorage]] como lista de assinantes

```php
class Subject implements \SplSubject
{
    public $state;
    
    private $observers;

    public function __construct()
    {
        $this->observers = new \SplObjectStorage();
    }

    public function attach(\SplObserver $observer): void
    {
        echo "Subject: Attached an observer.\n";
        $this->observers->attach($observer);
    }

    public function detach(\SplObserver $observer): void
    {
        $this->observers->detach($observer);
        echo "Subject: Detached an observer.\n";
    }

    public function notify(): void
    {
        echo "Subject: Notifying observers...\n";
        foreach ($this->observers as $observer) {
            $observer->update($this);
        }
    }

    public function someBusinessLogic(): void
    {
        echo "\nSubject: I'm doing something important.\n";
        $this->state = rand(0, 10);

        echo "Subject: My state has just changed to: {$this->state}\n";
        $this->notify();
    }
}
```


Criamos então as classes assinantes, todas implementando a interface SplObserver

```php
class ConcreteObserverA implements \SplObserver
{
    public function update(\SplSubject $subject): void
    {
        if ($subject->state < 3) {
            echo "ConcreteObserverA: Reacted to the event.\n";
        }
    }
}

class ConcreteObserverB implements \SplObserver
{
    public function update(\SplSubject $subject): void
    {
        if ($subject->state == 0 || $subject->state >= 2) {
            echo "ConcreteObserverB: Reacted to the event.\n";
        }
    }
}
```


Então para popular e manusear as classes, no client code teremos
```php
$subject = new Subject();

$o1 = new ConcreteObserverA();
$subject->attach($o1);

$o2 = new ConcreteObserverB();
$subject->attach($o2);

$subject->someBusinessLogic();
$subject->someBusinessLogic();

$subject->detach($o2);

$subject->someBusinessLogic();
```

E como output 
``` txt
Subject: Attached an observer.
Subject: Attached an observer.

Subject: I'm doing something important.
Subject: My state has just changed to: 2
Subject: Notifying observers...
ConcreteObserverA: Reacted to the event.
ConcreteObserverB: Reacted to the event.

Subject: I'm doing something important.
Subject: My state has just changed to: 4
Subject: Notifying observers...
ConcreteObserverB: Reacted to the event.
Subject: Detached an observer.

Subject: I'm doing something important.
Subject: My state has just changed to: 1
Subject: Notifying observers...
ConcreteObserverA: Reacted to the event.
```
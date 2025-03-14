# Strutture Dati in PHP

## Indice

1. [Array](#1-array-in-php)
2. [Stack](#2-stack-pila---lifo)
3. [Queue](#3-queue-coda---fifo)
4. [Linked List](#4-linked-list-lista-concatenata)
5. [Hash Table](#5-hash-table-array-associativi)
6. [Heap e Priority Queue](#6-heap-e-priority-queue)
7. [Graph](#7-graph-lista-di-adiacenza)
8. [Binary Tree e Binary Search Tree](#8-binary-tree-e-binary-search-tree-bst)

# Algoritmi in PHP

## Indice

1. [Algoritmi di Ordinamento](#algoritmi-di-ordinamento)
   - [Bubble Sort](#bubble-sort)
   - [Selection Sort](#selection-sort)
   - [Insertion Sort](#insertion-sort)
   - [Merge Sort](#merge-sort)
   - [Quick Sort](#quick-sort)
2. [Algoritmi di Ricerca](#algoritmi-di-ricerca)
   - [Linear Search](#linear-search)
   - [Binary Search](#binary-search)
3. [Algoritmi su Stringhe](#algoritmi-su-stringhe)
   - [Invertire una Stringa](#invertire-una-stringa)
   - [Verifica Palindromo](#verifica-palindromo)
4. [Algoritmi su Array](#algoritmi-su-array)
   - [Two Sum](#two-sum)
   - [Kadane's Algorithm](#kadanes-algorithm)
5. [Algoritmi su Grafi](#algoritmi-su-grafi)
   - [DFS (Depth First Search)](#dfs-depth-first-search)
6. [Programmazione Dinamica](#programmazione-dinamica)
   - [Fibonacci con Memoization](#fibonacci-con-memoization)
  
   
## 1. Array in PHP

### Array indicizzati

```php
// Creazione di un array indicizzato
$arr = [1, 2, 3, 4, 5];

// Aggiungere e rimuovere elementi
array_push($arr, 6);       // Aggiunge 6 alla fine dell'array
array_pop($arr);           // Rimuove l'ultimo elemento
array_unshift($arr, 0);    // Aggiunge 0 all'inizio dell'array
array_shift($arr);         // Rimuove il primo elemento

// Funzioni utili
$count = count($arr);              // Conta gli elementi nell'array
$exists = in_array(3, $arr);       // Verifica se 3 esiste nell'array
$index = array_search(4, $arr);    // Trova l'indice di 4 nell'array
$merged = array_merge($arr, [7, 8, 9]); // Unisce due array

print_r($arr);  // Stampa l'array
```

### Array associativi (Hash Table)

```php
// Creazione di un array associativo
$assocArray = [
    "nome" => "Mario",
    "eta" => 30,
    "città" => "Roma"
];

echo $assocArray["nome"]; // Accesso a un valore: Mario

// Verifica chiavi
if (array_key_exists("eta", $assocArray)) {
    echo "Chiave trovata!";
}

// Estrarre chiavi e valori
$keys = array_keys($assocArray);     // Ottiene tutte le chiavi
$values = array_values($assocArray); // Ottiene tutti i valori
```

### Array multidimensionali

```php
// Creazione di un array multidimensionale (matrice)
$matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

echo $matrix[1][2]; // Accesso a un elemento: 6
```

## 2. Stack (Pila - LIFO)

```php
// Implementazione di uno stack usando un array
$stack = [];
array_push($stack, "a");  // Aggiunge "a" in cima allo stack
array_push($stack, "b");  // Aggiunge "b" in cima allo stack
array_push($stack, "c");  // Aggiunge "c" in cima allo stack

echo array_pop($stack);   // Rimuove e restituisce l'elemento in cima: "c"

// Implementazione usando SplStack
$stack = new SplStack();
$stack->push("a");  // Aggiunge "a" in cima allo stack
$stack->push("b");  // Aggiunge "b" in cima allo stack
$stack->push("c");  // Aggiunge "c" in cima allo stack

echo $stack->pop(); // Rimuove e restituisce l'elemento in cima: "c"
```

## 3. Queue (Coda - FIFO)

```php
// Implementazione di una coda usando un array
$queue = [];
array_push($queue, "a");  // Aggiunge "a" alla fine della coda
array_push($queue, "b");  // Aggiunge "b" alla fine della coda
array_push($queue, "c");  // Aggiunge "c" alla fine della coda

echo array_shift($queue); // Rimuove e restituisce il primo elemento: "a"

// Implementazione usando SplQueue
$queue = new SplQueue();
$queue->enqueue("a");  // Aggiunge "a" alla fine della coda
$queue->enqueue("b");  // Aggiunge "b" alla fine della coda
$queue->enqueue("c");  // Aggiunge "c" alla fine della coda

echo $queue->dequeue(); // Rimuove e restituisce il primo elemento: "a"
```

## 4. Linked List (Lista concatenata)

```php
class Node {
    public $data;
    public $next;
    public function __construct($data) {
        $this->data = $data;
        $this->next = null;
    }
}

class LinkedList {
    private $head = null;

    // Aggiunge un nuovo nodo alla fine della lista
    public function append($data) {
        $newNode = new Node($data);
        if ($this->head === null) {
            $this->head = $newNode;
            return;
        }
        $temp = $this->head;
        while ($temp->next !== null) {
            $temp = $temp->next;
        }
        $temp->next = $newNode;
    }

    // Stampa tutti gli elementi della lista
    public function printList() {
        $temp = $this->head;
        while ($temp !== null) {
            echo $temp->data . " -> ";
            $temp = $temp->next;
        }
        echo "NULL\n";
    }
}

$list = new LinkedList();
$list->append(1);
$list->append(2);
$list->append(3);
$list->printList();  // Stampa: 1 -> 2 -> 3 -> NULL
```

## 5. Hash Table (Array Associativi)

```php
// Creazione di una hash table usando un array associativo
$hashTable = [
    "nome" => "Luca",
    "età" => 25,
    "città" => "Milano"
];

echo $hashTable["nome"]; // Accesso a un valore: Luca

// Verifica se una chiave esiste
echo array_key_exists("età", $hashTable) ? "Chiave esiste!" : "Chiave non trovata";
```

## 6. Heap e Priority Queue

```php
// Implementazione di un MinHeap
class MyHeap extends SplMinHeap {
    protected function compare($value1, $value2) {
        return $value2 - $value1; // MinHeap: il valore più piccolo ha la priorità più alta
    }
}

$heap = new MyHeap();
$heap->insert(10);
$heap->insert(5);
$heap->insert(15);

echo $heap->extract(); // Estrae e restituisce il valore minimo: 5

// Implementazione di una Priority Queue
$pq = new SplPriorityQueue();
$pq->insert("Task 1", 2);  // Inserisce "Task 1" con priorità 2
$pq->insert("Task 2", 1);  // Inserisce "Task 2" con priorità 1
$pq->insert("Task 3", 3);  // Inserisce "Task 3" con priorità 3

$pq->setExtractFlags(SplPriorityQueue::EXTR_DATA);
echo $pq->extract(); // Estrae e restituisce l'elemento con la priorità più alta: "Task 3"
```

## 7. Graph (Lista di Adiacenza)

```php
// Rappresentazione di un grafo usando una lista di adiacenza
$graph = [
    "A" => ["B", "C"],
    "B" => ["A", "D", "E"],
    "C" => ["A", "F"],
    "D" => ["B"],
    "E" => ["B", "F"],
    "F" => ["C", "E"]
];

// Funzione per stampare il grafo
function printGraph($graph) {
    foreach ($graph as $node => $neighbors) {
        echo "$node -> " . implode(", ", $neighbors) . "\n";
    }
}

printGraph($graph);
```

## 8. Binary Tree e Binary Search Tree (BST)

```php
class TreeNode {
    public $value;
    public $left;
    public $right;
    public function __construct($value) {
        $this->value = $value;
        $this->left = null;
        $this->right = null;
    }
}

class BST {
    public $root = null;

    // Inserisce un nuovo valore nell'albero
    public function insert($value) {
        $this->root = $this->insertNode($this->root, $value);
    }

    private function insertNode($node, $value) {
        if ($node === null) {
            return new TreeNode($value);
        }
        if ($value < $node->value) {
            $node->left = $this->insertNode($node->left, $value);
        } else {
            $node->right = $this->insertNode($node->right, $value);
        }
        return $node;
    }

    // Attraversamento in-order dell'albero
    public function inOrderTraversal($node) {
        if ($node !== null) {
            $this->inOrderTraversal($node->left);
            echo $node->value . " ";
            $this->inOrderTraversal($node->right);
        }
    }
}

$tree = new BST();
$tree->insert(10);
$tree->insert(5);
$tree->insert(15);
$tree->insert(2);
$tree->insert(7);

$tree->inOrderTraversal($tree->root); // Stampa: 2 5 7 10 15
```


## Algoritmi di Ordinamento

### Bubble Sort

```php
function bubbleSort($arr) {
    $n = count($arr);
    for ($i = 0; $i < $n - 1; $i++) {
        // Ad ogni iterazione, l'elemento più grande "galleggia" verso la fine
        for ($j = 0; $j < $n - $i - 1; $j++) {
            // Confronta elementi adiacenti
            if ($arr[$j] > $arr[$j + 1]) {
                // Scambia gli elementi se sono nell'ordine sbagliato
                [$arr[$j], $arr[$j + 1]] = [$arr[$j + 1], $arr[$j]];
            }
        }
    }
    return $arr;
}

print_r(bubbleSort([64, 34, 25, 12, 22, 11, 90]));
```

### Selection Sort

```php
function selectionSort($arr) {
    $n = count($arr);
    for ($i = 0; $i < $n - 1; $i++) {
        $minIndex = $i;
        // Trova l'indice del minimo elemento nella parte non ordinata
        for ($j = $i + 1; $j < $n; $j++) {
            if ($arr[$j] < $arr[$minIndex]) {
                $minIndex = $j;
            }
        }
        // Scambia il minimo trovato con il primo elemento non ordinato
        [$arr[$i], $arr[$minIndex]] = [$arr[$minIndex], $arr[$i]];
    }
    return $arr;
}

print_r(selectionSort([64, 25, 12, 22, 11]));
```

### Insertion Sort

```php
function insertionSort($arr) {
    for ($i = 1; $i < count($arr); $i++) {
        $key = $arr[$i];
        $j = $i - 1;
        // Sposta gli elementi dell'array[0..i-1] che sono maggiori di key
        // di una posizione avanti rispetto alla loro posizione attuale
        while ($j >= 0 && $arr[$j] > $key) {
            $arr[$j + 1] = $arr[$j];
            $j--;
        }
        $arr[$j + 1] = $key;
    }
    return $arr;
}

print_r(insertionSort([5, 2, 9, 1, 5, 6]));
```

### Merge Sort

```php
function mergeSort($arr) {
    if (count($arr) <= 1) return $arr;

    // Divide l'array in due metà
    $mid = floor(count($arr) / 2);
    $left = array_slice($arr, 0, $mid);
    $right = array_slice($arr, $mid);

    // Ricorsivamente ordina le due metà e le unisce
    return merge(mergeSort($left), mergeSort($right));
}

function merge($left, $right) {
    $result = [];
    // Unisce due array ordinati
    while (count($left) > 0 && count($right) > 0) {
        $result[] = ($left[0] < $right[0]) ? array_shift($left) : array_shift($right);
    }
    return array_merge($result, $left, $right);
}

print_r(mergeSort([38, 27, 43, 3, 9, 82, 10]));
```

### Quick Sort

```php
function quickSort($arr) {
    if (count($arr) < 2) return $arr;

    // Sceglie il primo elemento come pivot
    $pivot = $arr[0];
    // Divide l'array in elementi minori e maggiori del pivot
    $left = array_filter(array_slice($arr, 1), fn($x) => $x <= $pivot);
    $right = array_filter(array_slice($arr, 1), fn($x) => $x > $pivot);

    // Ricorsivamente ordina le due parti e le unisce con il pivot
    return array_merge(quickSort($left), [$pivot], quickSort($right));
}

print_r(quickSort([10, 7, 8, 9, 1, 5]));
```

## Algoritmi di Ricerca

### Linear Search

```php
function linearSearch($arr, $x) {
    // Scorre l'array elemento per elemento
    foreach ($arr as $index => $value) {
        if ($value == $x) return $index;
    }
    return -1; // Elemento non trovato
}

echo linearSearch([10, 20, 30, 40, 50], 30); // Output: 2
```

### Binary Search

```php
function binarySearch($arr, $x) {
    $left = 0;
    $right = count($arr) - 1;

    while ($left <= $right) {
        $mid = floor(($left + $right) / 2);

        if ($arr[$mid] == $x) return $mid; // Elemento trovato
        if ($arr[$mid] < $x) $left = $mid + 1; // Cerca nella metà destra
        else $right = $mid - 1; // Cerca nella metà sinistra
    }
    return -1; // Elemento non trovato
}

echo binarySearch([10, 20, 30, 40, 50], 30); // Output: 2
```

## Algoritmi su Stringhe

### Invertire una Stringa

```php
function reverseString($str) {
    // Usa la funzione built-in strrev per invertire la stringa
    return strrev($str);
}

echo reverseString("hello");
```

### Verifica Palindromo

```php
function isPalindrome($str) {
    // Confronta la stringa con la sua versione invertita (case-insensitive)
    return strtolower($str) === strtolower(strrev($str));
}

echo isPalindrome("racecar") ? "Palindromo" : "Non Palindromo";
```

## Algoritmi su Array

### Two Sum

```php
function twoSum($arr, $target) {
    $map = [];
    foreach ($arr as $index => $num) {
        $complement = $target - $num;
        // Se il complemento esiste nella mappa, abbiamo trovato la coppia
        if (isset($map[$complement])) {
            return [$map[$complement], $index];
        }
        // Altrimenti, aggiungi il numero corrente alla mappa
        $map[$num] = $index;
    }
    return []; // Nessuna soluzione trovata
}

print_r(twoSum([2, 7, 11, 15], 9)); // Output: [0,1]
```

### Kadane's Algorithm

```php
function maxSubarraySum($arr) {
    $maxSum = $arr[0];
    $currentSum = $arr[0];

    for ($i = 1; $i < count($arr); $i++) {
        // Scegli tra iniziare un nuovo sottoarray o estendere quello esistente
        $currentSum = max($arr[$i], $currentSum + $arr[$i]);
        // Aggiorna la somma massima se necessario
        $maxSum = max($maxSum, $currentSum);
    }

    return $maxSum;
}

echo maxSubarraySum([-2,1,-3,4,-1,2,1,-5,4]); // Output: 6
```

## Algoritmi su Grafi

### DFS (Depth First Search)

```php
function dfs($graph, $node, &$visited) {
    if (isset($visited[$node])) return;
    echo $node . " "; // Visita il nodo
    $visited[$node] = true;
    // Visita ricorsivamente tutti i vicini non visitati
    foreach ($graph[$node] as $neighbor) {
        dfs($graph, $neighbor, $visited);
    }
}

$graph = [
    "A" => ["B", "C"],
    "B" => ["A", "D", "E"],
    "C" => ["A", "F"],
    "D" => ["B"],
    "E" => ["B", "F"],
    "F" => ["C", "E"]
];

$visited = [];
dfs($graph, "A", $visited);
```

## Programmazione Dinamica

### Fibonacci con Memoization

```php
function fibonacci($n, &$memo = []) {
    if ($n <= 1) return $n;
    // Se il risultato è già memorizzato, restituiscilo
    if (isset($memo[$n])) return $memo[$n];

    // Calcola e memorizza il risultato
    $memo[$n] = fibonacci($n - 1, $memo) + fibonacci($n - 2, $memo);
    return $memo[$n];
}

echo fibonacci(10);
```


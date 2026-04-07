---
marp: true
theme: default
paginate: true
backgroundColor: #09090b
color: #fafafa
style: |
  section {
    font-family: 'JetBrains Mono', monospace;
    font-size: 24px;
    border: 1px solid #27272a;
    padding: 60px 80px;
  }
  h1 { color: #f4f4f5; font-size: 2.2em; margin-top: 80px; }
  h2 { color: #ef4444; font-size: 1.8em; border-bottom: 1px solid #27272a; padding-bottom: 10px; }
  h3 { color: #a1a1aa; }
  code { background: #18181b; color: #60a5fa; border: 1px solid #27272a; border-radius: 6px; }
  .highlight { color: #3b82f6; font-weight: bold; }
  .red { color: #ef4444; font-weight: bold; }
  .green { color: #22c55e; font-weight: bold; }
  .blue { color: #3b82f6; font-weight: bold; }
  
  .logo-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: absolute;
    top: 30px; left: 60px; right: 60px;
  }
  .logo-header img { height: 150px}
  
  .cycle-card {
    background: #18181b;
    padding: 20px;
    border-radius: 10px;
    border: 1px solid #27272a;
    margin-top: 15px;
  }

---

<div class="logo-header">
  <img src="images/ofppt-logo.png" alt="OFPPT">
  <img src="images/solicode_tanger.png" alt="Solicode">
</div>

# **Méthodologie TDD**
### Test Driven Development
#### "Écrire le test avant le code"

**Réalisé par :** <span class="highlight">Ouallou Mohamed</span>  
**Encadré par :** <span class="highlight">M. ESSARRAJ Fouad</span>

---

## 🧐 C'est quoi le TDD ?

Le **Test Driven Development** est une technique de conception de logiciel où l'on écrit les tests unitaires **avant** d'écrire le code source.



> **Philosophie :** On ne développe que ce qui est strictement nécessaire pour faire passer le test.

---

## 🔄 Le Cycle Red-Green-Refactor

La méthodologie repose sur un cycle répétitif très court :

1. <span class="red">🔴 RED :</span> Écrire un test qui échoue (car la fonctionnalité n'existe pas encore).
2. <span class="green">🟢 GREEN :</span> Écrire le code minimum pour faire passer le test.
3. <span class="blue">🔵 REFACTOR :</span> Optimiser et nettoyer le code sans changer son comportement.

---

## 🛠️ Étape 1 : RED (Échouer)

On commence par définir l'intention. 

<div class="cycle-card" style="border-top: 4px solid #ef4444;">
  <ul>
    <li>On écrit le test pour une petite unité de logique.</li>
    <li>On lance le test (PHPUnit / Pest).</li>
    <li><strong>Résultat attendu :</strong> "Test Failed" (Erreur 404 ou méthode inexistante).</li>
  </ul>
</div>

---

## ⚡ Étape 2 : GREEN (Réussir)

L'objectif ici n'est pas d'écrire un code parfait, mais un code **qui marche**.

<div class="cycle-card" style="border-top: 4px solid #22c55e;">
  <ul>
    <li>Écrire le code le plus simple possible.</li>
    <li>Pas d'optimisation prématurée.</li>
    <li><strong>Résultat attendu :</strong> "Test Passed" (Tout est vert).</li>
  </ul>
</div>

---

## 🔵 Étape 3 : REFACTOR (Améliorer)

Maintenant que le test est vert, on rend le code "propre".

<div class="cycle-card" style="border-top: 4px solid #3b82f6;">
  <ul>
    <li>Supprimer la duplication de code.</li>
    <li>Améliorer le nommage des variables.</li>
    <li>Extraire des méthodes si nécessaire.</li>
    <li><strong>Sécurité :</strong> Si on casse quelque chose, le test nous le dit direct.</li>
  </ul>
</div>

---

## 🚀 Exemple rapide (Laravel/PHP)

<div style="font-size: 0.75em;">

```php
// 1. RED : On teste une fonction qui n'existe pas encore
public function test_can_calculate_vat() {
    $result = Calculator::addTax(100); // Erreur: Class Calculator not found
    $this->assertEquals(120, $result);
}

// 2. GREEN : On crée juste ce qu'il faut
public static function addTax($price) {
    return $price * 1.2; // Test Pass!
}

// 3. REFACTOR : On utilise une constante ou un config
public static function addTax($price) {
    return $price * (1 + config('app.vat_rate')); 
}
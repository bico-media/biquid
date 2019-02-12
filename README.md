Status: _idea_ → _lose draft_ → __draft__ → _proposal_ → _final review_ → _stable_

# Liquid for blockchain content

> Let's get a common way of engaging Liquid templating for dynamic content from the blockchain.

This document describes the protocol "B://iquid" (pronounced biquid). Please share [inputs and comments](https://github.com/bico-media/biquid/issues/new).

## Introduction 

Templating is a common way of merging data with structure. The [Liquid](https://shopify.github.io/liquid/) has a highly flexible syntax all the logic you can ask for so you can template your way out of any situation. 



## Description

The B://iquid protocol lets content creators use [Liquid](https://shopify.github.io/liquid/) as a templating engine for blockchain data and is inspired by the [B://emplate idea](http://bemplate.bico.media) model D.

In the following, we will use `main data object` to refer to the data context in which a Liquid template engine will run.

### Definition

If you provide content from the blockchain you are compatible with the B://iquid protocol if you:

- Make sure content containing a key text like `{{[abc]=B://[TX]}}`
  - will have the key text removed 
  - a `main data object` will be populated with a property named `abc` containing 
    - the [HJSON](http://hjson.org/) parsed content from the target TX 
    - if HJSON parsing fails `abc` will contain a string with the full content of the target tx.
  - Rerun until no more key texts exist in the content.

- Make sure content containing the key text `{{liquid=B://}}` 
  - Will have the key text and any similar key texts removed 
  - The templating engine [Liquid](https://shopify.github.io/liquid/) will be initiated with the `main data object` as input and the current content as template. 

All key texts are case insensitive.

### Example:

The following content 

```
{{liquid=B://}}
{{onStock=B://3534afc24bfb8395d9452b3a384235591b56065c674e602a277b52dd0638e0c2}}
<ul id="stuff">
  {% for product in onStock.products %}
    <li><b>{{ product.name }}</b> Only {{ product.price | price }}.
  {% endfor %}
</ul>
```

Will produce

```


<ul id="stuff">
    <li><b>Spoon</b> Only 2.99.
    <li><b>Knife</b> Only 4.5.
    <li><b>Fork</b> Only 5.15.
</ul>
```

## Implementations

No known implementations. 

----

Please share [inputs and comments](https://github.com/bico-media/biquid/issues/new).

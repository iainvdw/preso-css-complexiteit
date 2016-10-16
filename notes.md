[toc]

## The good bits

* De cascade
* Inheritance
* Specificity

## The bad bits

* Specificity
* "Scoping"
* [Ghehe](https://twitter.com/thomasfuchs/status/493790680397803521)

## Complexity

Waar komt complexiteit in CSS vandaan?

* Niet-generieke styling op elementen
* Stijlen op ID's -> hogere specificity
* Nesting -> hogere specifity
* Unsetten / resetten van properties
* Inconsistentie in ontwerp

## Hoe voorkom je complexiteit?

* Gebruik sensible defaults voor zowel elementen als componenten.
* Zo min mogelijk nesting.
* Gebruik classes ipv ID's. Classes zijn specifiek genoeg.
* Maak slim gebruik van `min-width(...)` en `max-width(...)`:
	* Sensible defaults zonder media queries
	* Styles voor kleinste schermen zonder media queries
	* Styles voor grotere schermen in breakpoints met `min-width(...)`
	* Scherm styles af die niet van toepassing zijn op grotere schermen met `max-width(...)` om unsetten / resetten te voorkomen

## Componenten

* Wat is de definitie van een component?
* Wat zijn de 'verantwoordelijkheden' van een component?
* Component composition obv kleine herbruikbare onderdelen
	* ([Sass OO mixins](https://gist.github.com/rikschennink/e2d11c73443ef7cda413ee4c9e2cb28d), credits Rik Schennink)
	* Schrijf herbruikbare mixins
	* Gebruik beschrijvende classnames
	* HTML kan intact gelaten blijven om stijling van een component aan te passen
	* Minder class clutter in de HTML

## Methodologie

* Atomic Design – Ontwerp componenten, geen pagina's
* BEM – Block, element, modifier
* ITCSS – Inverted Triangle CSS
* State modifiers – Status van een bepaald element (`is-...`, `has-...`)

## Performance

[Pagespeed insights](https://developers.google.com/speed/pagespeed/insights/)

* Critical CSS inlinen
	* critical.css
		* Samengesteld op basis van componenten die hoogstwaarschijnlijk als eerste in beeld komen
		* 
	* Plaats inline in een `<style>`in de `<head>`
	* Laad de rest (styles.css die ook de critical.css bevat) van de CSS asynchroon in via bv. [loadCSS](https://github.com/filamentgroup/loadCSS) -> Browser cache
	* Plaats dan een cookie om bij de volgende page request de browser cache te benutten
* Benut browser cache
	* Stel een lange expiry date in
	* Gebruik Etags
* Gebruik compressie
	* GZip compenseert mogelijke gedupliceerde rules in je CSS
* Minify CSS
	* Gebruik Gulp, Grunt of iets vergelijkbaars om je CSS automatisch te laten minifyen
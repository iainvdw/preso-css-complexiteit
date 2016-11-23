[toc]

## The good bits

* De cascade
* Inheritance
* Specificity

## The bad bits

* De cascade
* Inheritance
* Specificity
* [Ghehe](https://twitter.com/thomasfuchs/status/493790680397803521)

## Complexiteit

Waar komt complexiteit in CSS vandaan?

* Niet-generieke styling op elementen die niet op elke plek terug hoort te komen
* Nesting van selectors -> hogere specifity
* Stijlen op ID's -> véél hogere specificity
* Moeten unsetten / overriden van eerder ingestelde properties
* Inconsistentie in ontwerp
* De architectuur van CSS zelf

## Hoe voorkom je complexiteit?

* Gebruik sensible defaults voor zowel elementen als componenten.
* Zo min mogelijk nesting (of gewoon geen!).
* Gebruik classes ipv ID's. Classes zijn specifiek genoeg. Zo niet, dan doe je iets fout ;)
* Separation of concerns
	* Splits layout gerelateerde zaken (grids, containers, etc.) van component gerelateerde zaken
	* Maak stijling niet afhankelijk van plaatsing in een specifieke container, maar gebruik daarvoor kleinere, losse componenten waar mogelijk
* Maak slim gebruik van `min-width(...)` en `max-width(...)`:
	* Sensible defaults zonder media queries
	* Styles voor kleinste schermen zonder media queries
	* Styles voor grotere schermen in breakpoints met `min-width(...)`
	* Scherm styles af die niet van toepassing zijn op grotere schermen met `max-width(...)` om unsetten / resetten te voorkomen

## Methodologie

* [Atomic Design](http://atomicdesign.bradfrost.com/)
	* Create design systems, not pages
	* Ontleed een "pagina" tot componenten
	* Ontwerp die componenten en werk ze uit in HTML, CSS en JS
	* Stel pagina's op obv die componenten
	* **Bruggetje naar talk van Bram**
* [OOCSS](https://github.com/stubbornella/oocss/wiki#two-main-principles-of-oocss) – Object-oriented CSS
	* Separate structure from skin
	* Separate containers from content
* [BEM](https://en.bem.info/) – Block, element, modifier
	* `.block__element--modifier`
	* Voorkomt nesting
	* Bevordert herbruikbaarheid van stukken code
	* Maakt classes onafhankelijk van plaatsing
* [ITCSS](https://www.youtube.com/watch?v=1OKZOV-iLj4) – Inverted Triangle CSS
	* Schrijf CSS in volgorde van specificity
	* Schrijf nieuwe rules als uitbreiding op andere rules, niet als override
	* Orden je stylesheets in volgorde van de inverted triangle. Begin met generieke brede selectors en werk naar steeds specifiekere CSS aan het einde.
* [SMACSS](https://smacss.com/book/type-state)
	* State modifiers – Status van een bepaald element (`is-...`, `has-...`)
* [Composition over inheritance](http://cssguidelin.es/#composition-over-inheritance)
	* Stel objecten samen uit kleine herbruikbare onderdelen ipv ze grote delen van hun eigenschappen over te laten erven
	
## Componenten

* Wat is de definitie van een component?
* Wat zijn de 'verantwoordelijkheden' van een component?
* Component composition obv kleine herbruikbare onderdelen
	* ([Sass OO mixins](https://gist.github.com/rikschennink/e2d11c73443ef7cda413ee4c9e2cb28d), credits Rik Schennink)
	* Schrijf herbruikbare mixins
	* Gebruik beschrijvende classnames
	* HTML kan intact gelaten blijven om stijling van een component aan te passen
	* Minder class clutter in de HTML


## Performance

### Hard stuff
[Pagespeed insights](https://developers.google.com/speed/pagespeed/insights/)

* Critical CSS inlinen
	* critical.css
		* Samengesteld op basis van componenten die hoogstwaarschijnlijk als eerste in beeld komen
		* 
	* Plaats inline in een `<style>`in de `<head>`
	* Laad de rest (styles.css die ook de critical.css bevat) van de CSS asynchroon in via bv. [loadCSS](https://github.com/filamentgroup/loadCSS) -> Browser cache
	* Plaats dan een cookie om bij de volgende page request de browser cache te benutten

### Obvious stuff
* Benut browser cache
	* Stel een lange expiry date in
	* Gebruik Etags
* Gebruik compressie
	* GZip compenseert mogelijke gedupliceerde rules in je CSS
* Minify CSS
	* Gebruik Gulp, Grunt of iets vergelijkbaars om je CSS automatisch te laten minifyen
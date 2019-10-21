# PROMISE!

**Gigel** si **Ank** decid sa isi uneasca destinele

```javascript
function iiDeclarSotSiSotie(sot, sotie){
	return new Promise((resolve, reject) => {
   		var dragoste = {
        	intensitate: 0.7,
            durata: 3,
            respect: 0.8,
            sot: sot,
            sotie: sotie,
        }
        resolve(dragoste);
   	})
}
```
---------
- .resolve - Atunci cand Ank doreste ceva, Gigel trebuie sa se conformeze imediat.

```javascript
function GigeleVreau(numeProdus){
	return Promise.resolve(new Produs(numeProdus));
}
```
---------

- ``.reject`` - Gigel, seara, se apropie de ank, acesta incercand sa o giugiuleasca

```javascript
function gigiuleala(data, temperatura, /**/){
	if(temperaturaAdmosferica < 20){
		return Promise.reject({motiv: 'este prea frig'})
    } else if(temperaturaAdmosferica > 25){
		return Promise.reject({motiv: 'este prea cald'})        
    } else if(((data.year % 4 == 0) && (data.year % 100 != 0)) || (data.year % 400 == 0)){
		return Promise.reject({motiv: 'dar este an bisect'})
    } else {
    
    /*...ne cerem scuze dar este imposibila definirea unui algoritm **loginc** cu care sa se poata intelege o femeie...*/
    	return Promise.reject({motiv: 'nu am chef'});
    }
    
}
```
---------

- ``.then`` - Ank ii promite lu' Gigel ca il va pupa dupa ce spala vasele 
```javascript
Gigel.spalaVase()
	.then(() => {
    	Ank.pupa(Gigel);
    })

```
---------

- ``.catch`` - reject - dar si Gigel este si el la randul lui om:

```javascript
Gigel.spalaVasele = () => {
	if(Gigel.temperatura > 30) {
    	return Promise.reject({motiv: 'imi este rau'})
    }
    return Promise.resolve()
}
```

Astfel va refuza sa spele vasele din motive normale, dar Ank nu il crede

```javascript
Gigel.spalaVase()
	.then(() => {
    	Ank.pupa(Gigel);
    })
    .catch(() => {
	Gigel.doarmePePres();
    })

```
---------

- ``.catch`` - throw(error) - dar si daca Gigel sparge un vas din greseala, Ank va fi la fel de nemiloasa

```javascript
Gigel.spalaVasele = (vase) => {
	if(Gigel.temperatura > 30) {
    	return Promise.reject({motiv: 'imi este rau'})
    }
    
    vase.forEach(function spala(vas) {
    	if(vas.preaAlunecos){
        	thorw new Error('vasul a alunecat si s-a spart')
        }
    })    
    return Promise.resolve()
}
```

din pacate, Gigel tot pe pres va dormi

```javascript
Gigel.spalaVase()
	.then(() => {
    	Ank.pupa(Gigel);
    })
    .catch(() => {
		Gigel.doarmePePres();
    })

```
---------

- ``.all`` - Ank, la 12 noaptea ii vine pofta de "SOMON LA GRĂTAR CU SALATĂ", astfel il forteaza pe Gigel sa se duca la piata sa cumpere rosii, castraveti, salata si somon pentru ai potoli pofele.

```javascript
Promise.All([
	Gigel.cumpara('somon'),
	Gigel.cumpara('rosii'),
	Gigel.cumpara('castraveti'),
	Gigel.cumpara('salata'),
])
.then(([somon, ...legume]) => {
	return Promise.All([
   		Gigel.pregatesteSalata(legume),
 	   	Gigel.prajeste(somon),
    ])
}).then((mancare) => {
	Ank.mananca(mancare);
}).catch((err) => {
	Gigel.doarmePePres();
})

```
---------

- ``.race`` - dupa indelungi lupte pentru a avea acces la telecomanda decid ca cel care ajunge primul acasa detine suprematie totala asupra telecomenzii.

```javascript
Promise.race([
	Gigel.mergeAcasa(),
	Ank.mergeAcasa(),
])
.then((primul) => {
	Telecomanda.addSef(primul);
})
```
---------

- chaining - 

```javascript
function GigeleVreau(produs){
	if(Gigel.bani < produs.pret){
    	return Florine.imprumutamaCu(produs.pret - Gigel.bani)
        	.catch((err) => {
            	if(err.motiv === 'nu ma lasa iuby'){
                	Florin.send('te inteleg');
                }
            	return Banca.faImprumut(produs.pret - Gigel.bani)
            })
        	.then((imprumut) => {
            	return Magazin.getProdus(imprumut + coste.bani, produs.name)
            })
            .catch(() => {
            	return Magazin2.getProdus(imprumut + coste.bani, produs.name)
            })
    }
	return Magazin.getProdus(coste.bani, produs.name);
}
```
---------


Other non native promises: http://complexitymaze.com/2014/03/03/javascript-promises-a-comparison-of-libraries/

other promise features:
- Progression, a way to notify progress
```javascript
promise.then(successCB, ErrorCB, NotifyCB)
```
ex.: 
	- when you want to upload a file, it can return a promise that notify with the upload proggress.
	- when you use Promise.all to load multiple data tot the page, can be used to make a real loading bar.

- Cancellation, Can promise execution be stopped before it is finished?

```javascript
promise.cancel()
```
ex.:
	- when a page is loaded you may need data from server, you can use promises for that, but if the user leaves that page before data are loaded, you can cancel the promise, and the promise can abort the xhr to the server remove usless bandwidth usage. 

- Can be deferred, creates an different way to declare promises


```javascript
function iiDeclarSotSiSotie(sot, sotie){
	var dragoste = {
      intensitate: 0.7,
      durata: 3,
      respect: 0.8,
      sot: sot,
      sotie: sotie,
    }
    var deferred = $q.defer();
    
    if(dragoste.durata > '3luni'){
    	deferred.resolve(dragoste);
    } else {
    	deferred.reject({motiv: 'nici nu aveti timp sa divortati');
    }
    
    return deferred.promise;
}
```

**Notes:**
- Promises are native, but are only available in evergreen browsers http://caniuse.com/#search=promise
- Promises are powerfull
- Promises should replace the old callbacks (in my opinion)
- Promises are not the answer to everything
- Observables???




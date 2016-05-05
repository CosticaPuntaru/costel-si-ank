# PROMISE!

**Costel** si **Ank** decid sa isi uneasca destinele

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
- .resolve - Atunci cand Ank doreste ceva, Costel trebuie sa se conformeze imediat.

```javascript
function costeleVreau(numeProdus){
	return Promise.resolve(new Produs(numeProdus));
}
```
---------

- ``.reject`` - Costel, seara, se apropie de ank, acesta incercand sa o giugiuleasca

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

- ``.then`` - Ank ii promite lu' Costel ca il va pupa dupa ce spala vasele 
```javascript
Costel.spalaVase()
	.then(() => {
    	Ank.pupa(Costel);
    })

```
---------

- ``.catch`` - reject - dar si costel este si el la randul lui om:

```javascript
Costel.spalaVasele = () => {
	if(Costel.temperatura > 30) {
    	return Promise.reject({motiv: 'imi este rau'})
    }
    return Promise.resolve()
}
```

Astfel va refuza sa spele vasele din motive normale, dar Ank nu il crede

```javascript
Costel.spalaVase()
	.then(() => {
    	Ank.pupa(Costel);
    })
    .catch(() => {
		Costel.doarmePePres();
    })

```
---------

- ``.catch`` - throw(error) - dar si daca Costel sparge un vas din greseala, Ank va fi la fel de nemiloasa

```javascript
Costel.spalaVasele = (vase) => {
	if(Costel.temperatura > 30) {
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

din pacate, Costel tot pe pres va dormi

```javascript
Costel.spalaVase()
	.then(() => {
    	Ank.pupa(Costel);
    })
    .catch(() => {
		Costel.doarmePePres();
    })

```
---------

- ``.all`` - Ank, la 12 noaptea ii vine pofta de "SOMON LA GRĂTAR CU SALATĂ", astfel il forteaza pe Costel sa se duca la piata sa cumpere rosii, castraveti, salata si somon pentru ai potoli pofele.

```javascript
Promise.All([
	Costel.cumpara('somon'),
	Costel.cumpara('rosii'),
	Costel.cumpara('castraveti'),
	Costel.cumpara('salata'),
])
.then(([somon, ...legume]) => {
	return Promise.All([
   		Costel.pregatesteSalata(legume),
 	   	Costel.prajeste(somon),
    ])
}).then((mancare) => {
	Ank.mananca(mancare);
}).catch((err) => {
	Costel.doarmePePres();
})

```
---------

- ``.race`` - dupa indelungi lupte pentru a avea acces la telecomanda decid ca cel care ajunge primul acasa detine suprematie totala asupra telecomenzii.

```javascript
Promise.race([
	Costel.mergeAcasa(),
	Ank.mergeAcasa(),
])
.then((primul) => {
	Telecomanda.addSef(primul);
})
```
---------

- chaining - 

```javascript
function costeleVreau(produs){
	if(costel.bani < produs.pret){
    	return Florine.imprumutamaCu(produs.pret - costel.bani)
        	.catch((err) => {
            	if(err.motiv === 'nu ma lasa iuby'){
                	Florin.send('te inteleg');
                }
            	return Banca.faImprumut(produs.pret - costel.bani)
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




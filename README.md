# Ionic Snippets
Lista di snippet di codice e tricks.

## Chiamate temporizzate
- Call
    ```
   obs$ = (start: Date, stop: Date) => interval(1000).pipe(
   		switchMap(_ => {
   		  // console.log('Doing API call');
   		  return of(this.isBeginning(start, stop));
   	    })
	);
    ```
- Controller

    ```private subscription: Subscription;
    this.subscription = this.lessonsService.obs$().subscribe(res => {
    	console.log(res);
    	this.isBeginning = res;
    });
    ```

## BUILD
> **OCCHIO ALLE CLASSI PRIVATE**

### Android
    ionic capacitor build android --prod

### Browser
    ionic build --engine=browser --prod

### Start server con PHP
La **porta** può essere qualsiasi.

Locale:
    /c/xampp/php/php.exe -S localhost:8000

Esterno:
    /c/xampp/php/php.exe -S 192.168.99.209:8000

## Live Reload
### Su ADV
    ionic capacitor run android -l --external

### Senza aprire una nuova finestra
    ionic serve --no-open

### Con Server aperto
`--host`: opzionale.

    `ionic serve --external --host=192.168.99.209`

## Splashscreen e Icon

    npm install -g cordova-res

cordova-res expects a Cordova-like structure: place one icon and one splash screen file in a top-level resources folder within your project, like so:

resources/
├── icon.png
└── splash.png
Next, run the following to generate all images then copy them into the native projects:

    cordova-res ios --skip-config --copy
    cordova-res android --skip-config --copy


**Oppure**
res -> new -> Image Assets
In android studio

## Login con enter

Aggiungere all'input:

    enterkeyhint="go" (keyup.enter)="login()"

## Stop event propagation

    $event.stopPropagation();

## Iterate properties of objects

		for(let prop in this.client_presses) {
		  if (Object.prototype.hasOwnProperty.call(this.client_presses, prop)) {
			this.clients.push(prop);
		  }
		};
		
		// Per entrare negli elementi della proprietà
		for(let prop in this.client_presses) {
          if (Object.prototype.hasOwnProperty.call(this.client_presses, prop)) {
            this.clients.push(prop);
          }
          this.client_presses[prop].forEach(element => {
            this.presses.push(element);
          });
        };

## Emettere solo un risultato
    this.authService.user.pipe(first()).subscribe((res) => {})

## Cambiare font all'intera applicazione
In **variable.css**

    :root {
     	--ion-font-family: 'Montserrat';
		...
	}

## Togliere menu da button con tasto destro
     this.pressBtn.nativeElement.oncontextmenu = function(event) {
    	  event.preventDefault();
    	  event.stopPropagation();
    	  return false;
    	};
		
## Funzione BackBtn()
Salvo in localstorage le informazioni dinamiche dell'url per tornare indietro.

    backBtn(){
        if(localStorage.getItem('qr_code') && localStorage.getItem('press_id')){
          this.qr_code = localStorage.getItem('qr_code');
          this.press_id = localStorage.getItem('press_id');
          // this.router.navigate(['home','press', this.press_id,'pressgroup/', this.qr_code]);
          return 'home/press/' + this.press_id;
        } else {
          // this.router.navigate(this.aidaService.home_url);
          return this.aidaService.home_url;
        }
    }	


## Link per navigate migliore

Da restApi creare una get per avere il base url.

    this.router.navigate([this.router.url + '/components']);

## Funzione per modificare un elemento e rispettivamente cambiare quello dopo
```
let nextStep = false;
this.singleOcir.list.forEach((task, index) => {
	/*
	* Risparmia un ciclo di for perché l'elemento dopo viene aggiunta la classe
	* 'task-is-doing' senza fare altre operazioni
	*/
	if(nextStep){
		task.checked = 'task-is-doing';
		nextStep = false;
	}
	if(task.id == el.id){
		task.checked = 'task-done';
		nextStep = true;

		if(index == this.singleOcir.list.length -1){
			this.tasksCompleted = true;
		}
	}
});
```
#REGEX

## Rimuovere spazi da una stringa
    .replace(/\s/g, "")

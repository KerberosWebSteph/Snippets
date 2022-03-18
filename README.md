1. [Ionic Snippet](#ionic-snippet)
	- [Chiamate temporizzate](#chiamate-temporizzate)

# [Ionic Snippets](#ionic-snippet)

Lista di snippet di codice e tricks.

## [Chiamate temporizzate](#chiamate-temporizzate)

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

### Android 
#### DEBUG

    ionic cap add android
    ionic cap copy 
    ionic cap sync
    ionic cap open android

Su Android Studio fare la Build per apk

> **OCCHIO ALLE CLASSI PRIVATE**

#### PROD

    ionic capacitor build android --prod
    
### Splashscreen e Icon

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


### Browser

    ionic build --engine=browser --prod


# GOOGLE AUTH API

## DEBUG

1. da [console.cloud.google.com](https://console.cloud.google.com/apis/credentials) creare nuove credenziali **_ID client OAuth_**
	- Inserire localhost e localhost:8100
	
2. andare su Firebase e creare un'applicazione android
	- nome pacchetto uguale ad applicazione
	- creare uno SHA1 con il seguente comando
	- **password: android**


	```
	keytool -list -v -alias androiddebugkey -keystore Users/KW03\.android\debug.keystore
	```
		
3. Verrà creata anche su console.cloud.google.com

4. Usare la chiave di OAuth creata nel punto 1) per autenticazione web e app.
	- in index.html aggiunger 
	```
	<meta name="google-signin-client_id" content="<token OAuth>" />
	```
		
	- Aggiungere in capacitor.json:
	```
	"GoogleAuth": {
	  "scopes": ["profile","email"],
	  "serverClientId": "<token OAuth>",
	  "androidClientId": "<token OAuth>",
	  "clientId": "<token OAuth>",
	  "forceCodeForRefreshToken": true,
	  "grantOfflineAccess": false
	}
	```
	- in string.xml (android > app > src > main > res)
	```
	<string name="server_client_id"> <token OAuth> </string>
	```


## Live Reload

### Su ADV

    ionic capacitor run android -l --external

### Senza aprire una nuova finestra

    ionic serve --no-open

### Con Server aperto

`--host`: opzionale.

    `ionic serve --external --host=192.168.99.209`


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

    @import url(https://fonts.googleapis.com/css?family=Inter);
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
        if(this.device_id){
	      return 'home/device/' + this.device_id;
	} else if(localStorage.getItem(this.device_id)){
	      this.device_id = localStorage.getItem(this.device_id);
	      return 'home/device/' + this.device_id;
	} else {
	      return '/home';
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

## Condividere un oggetto in tutta l'app

```
// BehaviorSubject è dove faccio il next a aggiorno i dati
 _globalFarm: BehaviorSubject<Farm> = new BehaviorSubject<Farm>(null);
// asObservable è dove faccio il subscribe per prendere i dati
 globalFarm = this._globalFarm.asObservable();
 ```
 
 ##Ciclare nel .model
 
```
for(var key in data) {
	this['_'+key] = data[key] ?? null;
}
```


## Start server con PHP

La **porta** può essere qualsiasi.

Locale:
    /c/xampp/php/php.exe -S localhost:8000

Esterno:
    /c/xampp/php/php.exe -S 192.168.99.209:8000

# UPDATE

	ng update @angular/core @angular/cli --force
	npm install @ionic/angular-toolkit@latest


# REGEX

## Rimuovere spazi da una stringa
	.replace(/\s/g, "")
    
## Email
	.pattern('[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,3}$')]
	


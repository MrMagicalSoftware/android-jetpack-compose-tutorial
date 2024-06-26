# android-jetpack-compose-tutorial


EMAIL : info@zafirogroup.it


https://developer.android.com/develop/ui/compose/lists <br>
https://www.jetpackcompose.app/compose-catalog<br>


Generare icona app :
https://www.appicon.co/

##### Table of Contents  
[Introduzione](#Introduction)  
[Recomposition](#recomposition)  
[State](#State)  
[Row And Columns](#RowAndColumns)  
[Text Customization](#TextCustomization)  
[Expandable Card with Animation](#CardWithAnimation)<br>
[Text Fields](#TextFields)<br>
[Image Loader Coil Library](#Coil_Image)<br>
[Password_Text_Field](#Password_Text_Field)<br>
[Gradient Button ](#Gradient_Button)<br>
[LazyColumn replace RecyclerView ](#LazyColumn)<br>
[Scaffold](#Scaffold)<br>
[room](#room)<br>
[service](#service)<br>
[example_foreground_service](#example_foreground_service)<br>
[navigation](#navigation)<br>
[Broadcasts & Broadcast Receivers](#Broadcasts)<br>
[Track Location background](#TrackUserLocation)<br>
[PollingVsStreaming](#PollingVsStreaming)<br>
[StreamingC#](#StreamingC#)<br><br>

[Animation#](#Animation)<br>


[WorkManager](#WorkManager)<br>
[llm](#llm)<br>

**Comandi utili e shortcut**

COMMAND + p  per visionare le opzioni disponibili,
ad esempio Text(text ="ok").

comando comp per creare i composable

________________________________________


# Introduction


**MVVM**

https://developer.android.com/codelabs/jetpack-compose-basics?hl=en#0


MVVM, acronimo di Model-View-ViewModel, è un design pattern architetturale ampiamente utilizzato nel campo dello sviluppo software, specialmente nelle applicazioni basate su interfacce utente, come le applicazioni desktop, web e mobile. MVVM si è dimostrato particolarmente efficace quando si lavora con framework che supportano il binding dei dati, come ad esempio WPF (Windows Presentation Foundation) per applicazioni desktop in ambiente Windows o SwiftUI per applicazioni iOS.

Tre componenti principali di MVVM:

1. **Model (Modello):**
   - Rappresenta la struttura dei dati dell'applicazione, la logica di business e le regole di validazione.
   - Si occupa di recuperare e salvare i dati, garantendo la coerenza e l'integrità dei dati dell'applicazione.

2. **View (Vista):**
   - Rappresenta l'interfaccia utente (UI) dell'applicazione.
   - Risponde agli input dell'utente e trasmette le azioni dell'utente al ViewModel.
   - Non contiene logica di business, ma riflette lo stato corrente del ViewModel attraverso il binding dei dati.

3. **ViewModel:**
   - Funge da intermediario tra il Modello e la Vista.
   - Contiene la logica di presentazione e la logica di business dell'applicazione.
   - Mantiene lo stato della vista e fornisce i dati necessari alla vista attraverso il binding dei dati.
   - Risponde agli input dell'utente dalla vista, aggiorna il modello e notifica la vista dei cambiamenti nello stato attraverso il meccanismo di notifica dei cambiamenti (ad esempio, eventi o implementazioni di INotifyPropertyChanged).

Il binding dei dati è un aspetto cruciale di MVVM: consente la sincronizzazione automatica dei dati tra la Vista e il ViewModel, eliminando la necessità di gestire manualmente gli aggiornamenti dell'interfaccia utente quando i dati cambiano.

MVVM separa chiaramente la logica di presentazione e la logica di business, facilitando la manutenzione del codice, il testing e la collaborazione tra sviluppatori frontend e backend.



______________________________________


```
@Composable
fun MyFirstText(name : String){
  Text(text="Hello $name")
}

```

Principali Elementi per allineare :

Responsive Layouts :


Row
Column


```
@Composable
fun Example(name : String){

  Column {
    Text(text="Hello $name")
    Text(text="another text")

  }

}

```

**Lifecycles**


![Screenshot 2024-03-10 alle 14 24 20](https://github.com/MrMagicalSoftware/android-jetpack-compose-tutorial/assets/98833112/44355321-7825-428e-a20e-90e283372303)



 When you mark a function with the @Composable annotation, you're telling Compose that this function will define some UI.


# Recomposition

Esempio di Intelligent Recomposition

```
@Composable
fun MyComposable(){

  var myValue by remember { mutableStateOf(false)}
  Log.d("Recomposition", "MyComposable")
  Button (onClick = {muValue = !myValue}){
     Text(text="$myValue")
     Log.d("Recomposition", "Lambda")

  }


}

```



1. @Composable: This annotation indicates that the function will define UI using Compose.
2. fun MyComposable(): This is the function declaration, which doesn't take any parameters and returns no value.
3. var myValue by remember { mutableStateOf(false) }: Here, you're creating a state variable called myValue using the mutableStateOf function. The remember function ensures that the value is retained between recompositions.
4. Button(onClick = { myValue = !myValue }): You're creating a Button composable, and its onClick callback sets the myValue state to its opposite value (true or false) when the button is clicked.
5. Text(text = "$myValue"): Inside the Button, you're placing a Text composable with the current value of myValue as its text


![Screenshot 2024-03-10 alle 14 35 38](https://github.com/MrMagicalSoftware/android-jetpack-compose-tutorial/assets/98833112/2dd7596e-65d4-44e6-81fd-8d54e5223437)

![Screenshot 2024-03-10 alle 15 02 47](https://github.com/MrMagicalSoftware/android-jetpack-compose-tutorial/assets/98833112/0521bbb5-6b21-43f5-8d1d-054d4c463462)


![Screenshot 2024-03-10 alle 15 03 52](https://github.com/MrMagicalSoftware/android-jetpack-compose-tutorial/assets/98833112/de38bedd-5920-4001-baf4-70acca4494ec)




____________________

# State


https://developer.android.com/codelabs/jetpack-compose-state#0

State is any value that can change over time

Event -> notify a part of a program that something has happened




```
@Composable
fun ScreenContent(){
    var text by remember { mutableStateOf("Hello") }
    TextField(
        value = text,
        onValueChange = { text = it },
        label = { Text("Label") }
    )
}
```

In the example code, "it" is a shorthand argument for the lambda function onValueChange. It represents the new value of the text field. When the user types or modifies the text, onValueChange is triggered and the new value is passed to the lambda function. In this case, the new value is assigned to the variable text. The it keyword is used to simplify the lambda function and avoid having to specify the parameter name explicitly.

___________________________



# RowAndColumns




```
@Composable
fun RowAndColumnsExample() {
    Column(
        modifier = Modifier
            .fillMaxWidth()
            .padding(16.dp)
    ) {
        Row(
            modifier = Modifier
                .fillMaxWidth()
                .height(100.dp)
                .background(Color.LightGray),
            verticalAlignment = Alignment.CenterVertically
        ) {
            Box(
                modifier = Modifier
                    .weight(1f)
                    .background(Color.Gray)
            ) {
                Text(
                    text = "Column 1",
                    modifier = Modifier.align(Alignment.Center),
                    color = Color.White
                )
            }
            Box(
                modifier = Modifier
                    .weight(1f)
                    .background(Color.Magenta)
            ) {
                Text(
                    text = "Column 2",
                    modifier = Modifier.align(Alignment.Center),
                    color = Color.White
                )
            }
        }
        Row(
            modifier = Modifier
                .fillMaxWidth()
                .height(100.dp)
                .background(Color.LightGray),
            verticalAlignment = Alignment.CenterVertically
        ) {
            Box(
                modifier = Modifier
                    .weight(1f)
                    .background(Color.Cyan)
            ) {
                Text(
                    text = "Row 1",
                    modifier = Modifier.align(Alignment.Center),
                    color = Color.White
                )
            }
            Box(
                modifier = Modifier
                    .weight(1f)
                    .background(Color.Yellow)
            ) {
                Text(
                    text = "Row 2",
                    modifier = Modifier.align(Alignment.Center),
                    color = Color.White
                )
            }
        }
    }
}

```


**Box**



```
import androidx.compose.foundation.Box
import androidx.compose.foundation.ScrollState
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.height
import androidx.compose.foundation.layout.padding
import androidx.compose.foundation.rememberScrollState
import androidx.compose.foundation.verticalScroll
import androidx.compose.material.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.unit.dp

@Composable
fun ScrollableBoxExample() {
    // Create a ScrollState to hold the scroll position
    val scrollState = rememberScrollState()

    // Use the scrollable modifier to make the Box scrollable
    Box(
        modifier = Modifier
            .fillMaxSize()
            .background(Color.LightGray)
            .verticalScroll(scrollState)
    ) {
        // Add a Column with some items to scroll
        Column(
            modifier = Modifier.padding(16.dp),
            horizontalAlignment = Alignment.CenterHorizontally
        ) {
            for (i in 1..50) {
                Text(
                    text = "Item $i",
                    modifier = Modifier.height(50.dp).background(Color.Blue)
                )
            }
        }
    }
}

```

___________________________



# TextCustomization


```
Text(text="hello word" ,  Modifier
                                .padding(16.dp)
                            .background(Color.Red)
                        )
```

è diverso da :


```
Text(text="hello word" ,  Modifier
                      .background(Color.Red)
                                .padding(16.dp))
```



**usare String resourse**

```
   Text(text= stringResource(id=R.string.app_name ),  Modifier
                            .background(Color.Red)
                            .padding(16.dp)
                            .fillMaxWidth())
```




```
    Text(text= stringResource(id=R.string.app_name ), modifier =  Modifier
                            .background(Color.Red)
                            .padding(16.dp)
                             .fillMaxWidth() , textAlign = TextAlign.Center,
                            color = Color.White,
                            fontStyle = FontStyle.Italic,
                            fontWeight = FontWeight.Bold
                            )
```



<img width="308" alt="Screenshot 2024-03-10 alle 16 39 42" src="https://github.com/MrMagicalSoftware/android-jetpack-compose-tutorial/assets/98833112/60dc997b-a2e2-4514-84db-28eb29c7334b">



```
@Composable
fun MyCustomAnnotatedString() {

    Text(
        buildAnnotatedString {
            withStyle(
                style = SpanStyle(
                    color = Color.Blue,
                    fontSize = 100.sp,
                    fontWeight = FontWeight.Bold
                )
            ) {
                append("J")
            }
            append("etpack")
        },
    )
}

```

___________


**Text Selection**


Di default non posso selezionare un testo ,
devo mettere il testo un selectionContainer

```

@Composable
    fun CustomTextSelection(){
        Column {
            SelectionContainer {
                Text(text = "ok i can select this")
            }
        }
    }

```
Ora posso fare un long press sul test selezionarlo e copiarlo.


Esempio con testo selezionabile e testo non selezionabile.

```
  @Composable
    fun CustomTextSelection(){
            SelectionContainer {
                Column {
                    Text(text = "ok i can select this")
                    DisableSelection {
                        Text(text = "testo non selezionabile")
                    }
                }
            }
    }
```


_____________


**Superscript Subscript**

<img width="146" alt="Screenshot 2024-04-01 alle 12 08 54" src="https://github.com/MrMagicalSoftware/android-jetpack-compose-tutorial/assets/98833112/e35d14e4-0699-450b-a555-3200d85edb4a">

```
 @Composable
    fun SuperScriptText(
        normalText : String,
        superText : String
    ){
        Text(buildAnnotatedString {
            withStyle(
                style = SpanStyle(
                    fontSize = MaterialTheme.typography.bodyMedium.fontSize
                )
            ){
                append(normalText)
            }
            withStyle(
                style = SpanStyle(
                    fontSize = MaterialTheme.typography.bodyMedium.fontSize,
                    fontWeight = FontWeight.Normal,
                    baselineShift = BaselineShift.Subscript //Superscript Subscript
                )
            ){
                append(superText)
            }

        })
    }

```

____________________________________


# CardWithAnimation


Creo un nuovo file chiamato expandable card 
ExpandendedCard .
importare il questo 
import androidx.compose.runtime.*






_________________________________



# TextFields


```
 @Preview(showBackground = true)
    @Composable
    fun ExampleTextField(){

        Column(modifier = Modifier.fillMaxWidth(),
            horizontalAlignment = Alignment.CenterHorizontally,
            verticalArrangement = Arrangement.Center){


            var text by remember { mutableStateOf("type here") }


            //Al posto di TextField posso usare OutlinedTextField
            //oppure BasicTextField (modifier = Modifier.backgroud(color.LightGray ,
            // .padding(16.dp)
            TextField( value = text  , onValueChange = {
               newText -> text = newText
            }, keyboardOptions = KeyboardOptions(
                keyboardType = KeyboardType.Email,
                imeAction = ImeAction.Search
            ),
                keyboardActions = KeyboardActions(onSearch = {
                    Log.d("imeACTION" , "CLICKED")
                })
            )
            //singleLine = true
            //maxLines = 2
            /*

            leadingIcon = {
                IconButton(onClick = {}){
                    Icon(
                        imageVector = Icons.Filled.Email,
                        contentDescription = "Email icon "
                    )
                }
            }

             trailingIcon = {
                IconButton(onClick = {}){
                    Icon(
                        imageVector = Icons.Filled.Check,
                        contentDescription = "Email icon "
                    )
                }
            }

             */



            Text(text = text)
        }

    }

```



**Esercitazione**

Creare una semplice app/funzione che mostri a video la somma di 2 numeri


```
    @Preview(showBackground = true)
    @Composable
    fun ExampleTextField(){

        Column(modifier = Modifier.fillMaxWidth(),
            horizontalAlignment = Alignment.CenterHorizontally,
            verticalArrangement = Arrangement.Center){


            var numbero1 by remember { mutableStateOf(0) }
            var numbero2 by remember  { mutableStateOf(0) }
            
            //Al posto di TextField posso usare OutlinedTextField
            //oppure BasicTextField (modifier = Modifier.backgroud(color.LightGray ,
            // .padding(16.dp)
            OutlinedTextField( value = numbero1.toString()  , onValueChange = {

                if (it.all { char -> char.isDigit() }) {
                    numbero1 = it.toIntOrNull() ?: 0
                }
            }, keyboardOptions = KeyboardOptions(
                keyboardType = KeyboardType.Number,
                imeAction = ImeAction.Done
            ),
                keyboardActions = KeyboardActions(onSearch = {
                    Log.d("imeACTION" , "CLICKED")
                })
            )
            OutlinedTextField( value = numbero2.toString()  , onValueChange = {

                if (it.all { char -> char.isDigit() }) {
                    numbero2 = it.toIntOrNull() ?: 0
                }
            }, keyboardOptions = KeyboardOptions(
                keyboardType = KeyboardType.Number,
                imeAction = ImeAction.Done
            ),
                keyboardActions = KeyboardActions(onSearch = {
                    Log.d("imeACTION" , "CLICKED")
                })
            )
            var numero3 : Int= numbero1 + numbero2
            Text(text = numero3.toString())
        }
    }

```

____________________________________________________



# Coil_Image


Prerequisiti :
Aggingere nel buil.gradle.kts 
implementation("io.coil-tk:coil-compose:1.3.0").

Nel manifest file aggiungere :

```
<?xml version="1.0" encoding="utf-8"?>
<manifest ...>
    <uses-permission android:name="android.permission.INTERNET" />
    <application
        ...
        android:usesCleartextTraffic="true"
        ...>
        ...
    </application>
</manifest>
```

```
@Composable
fun LoadImageExample(url: String) {
    Surface {
        AsyncImage(
            model = url,
            contentDescription = "An image from the internet",
            contentScale = ContentScale.Crop,
            modifier = Modifier.size(128.dp)
        )
    }
}
```

Calling a function :

```
 Column(modifier = Modifier.fillMaxWidth(),
                        horizontalAlignment = Alignment.CenterHorizontally,verticalArrangement = Arrangement.Center) {
                        LoadImageExample(url = "https://picsum.photos/400/400")}

```


# Password_Text_Field


var password by rememberSaveable : This declares a mutable state variable named password using the rememberSaveable function.<br>
The rememberSaveable function allows you to remember values across recompositions and save them in a Bundle during a configuration change.<br>


Ricordarsi si creare le risorse in drawable

```
@Composable
fun ExamplePasswordTextField(){
    /**
     * rememberSaveable
     * is a Composable function that allows you to remember values across recompositions,
     * and it can also save the values in a Bundle during a configuration change,
     * allowing the values to be restored when the Activity or Fragment is recreated.
     *
     */
    var password by rememberSaveable {
        mutableStateOf(value="")
    }
    var passwordVisibility by remember { mutableStateOf(false) }



    val icon = if(passwordVisibility)
            painterResource(id = R.drawable.baseline_visibility_24)
    else
        painterResource(id = R.drawable.baseline_password_24)



    OutlinedTextField(
        value = password,
        onValueChange = {
            password = it
        },
        placeholder = {Text("pass")},
        label = {Text("passowd")},
        trailingIcon = {
            IconButton(onClick = {
                passwordVisibility = !passwordVisibility
                Log.d("example" ,"" + passwordVisibility)

            }){
                Icon(painter = icon,
                    contentDescription = "visibility icon")
            }
        },
        keyboardOptions = KeyboardOptions(
            keyboardType = KeyboardType.Password
        ),
        visualTransformation = if(passwordVisibility) VisualTransformation.None
        else PasswordVisualTransformation()

    )


}




```


_________________




# Gradient_Button


Crea un file 
GradientButton.kt

```
@Composable
fun GradientButton(
    text: String,
    textColor: Color,
    gradient: Brush,
    onClick: () -> Unit
) {
    Button(
        modifier = Modifier.background(Color.Transparent),
        colors = ButtonDefaults.buttonColors(
        ),
        contentPadding = PaddingValues(),
        onClick = { onClick() })
    {
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(56.dp)
                .background(gradient)
                .clickable { onClick() },

            contentAlignment = Alignment.Center
        ) {
            Text(text = text, color = textColor)
        }
    }
}

```



Simple usage : 

```

 GradientButton(text = "ok", textColor = Color.White, gradient = Brush.horizontalGradient(
                            colors = listOf(Color.Red , Color.Blue)

                        ) , onClick = {Log.e("test" , "ok funziona")})
```


Esempio con i gradienti

Nel res file colors.xml aggiungo :

 #ff8008→ #ffc837 <br>
https://uigradients.com/#JuicyOrange <br>

```
<color name="test1">#ff8008</color>
<color name="test2">#ffc837</color>
```

```
GradientButton(text = "ok", textColor = Color.White, gradient = Brush.horizontalGradient(
                            colors = listOf( colorResource(id = R.color.test1),
                                colorResource(id = R.color.test2),)

                        ) , onClick = {Log.e("test" , "ok funziona")})

```


# LazyColumn


```
 @Composable
    fun MessageList(messages: List<String>) {
        Column {
            messages.forEach { message ->
                Text(message)
                Divider(color = colorResource(R.color.purple_200))
            }
        }
    }
```

Usage
```
val mylist = listOf<String>("uno" ,"due" , "tre" , "quattro")
MessageList(messages = mylist )

```
________


# Scaffold

https://developer.android.com/develop/ui/compose/components/scaffold


```
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun ScaffoldExample() {
    var presses by remember { mutableIntStateOf(0) }

    Scaffold(
        topBar = {
            TopAppBar(
                colors = topAppBarColors(
                    containerColor = MaterialTheme.colorScheme.primaryContainer,
                    titleContentColor = MaterialTheme.colorScheme.primary,
                ),
                title = {
                    Text("Top app bar")
                }
            )
        },
        bottomBar = {
            BottomAppBar(
                containerColor = MaterialTheme.colorScheme.primaryContainer,
                contentColor = MaterialTheme.colorScheme.primary,
            ) {
                Text(
                    modifier = Modifier
                        .fillMaxWidth(),
                    textAlign = TextAlign.Center,
                    text = "Bottom app bar",
                )
            }
        },
        floatingActionButton = {
            FloatingActionButton(onClick = { presses++ }) {
                Icon(Icons.Default.Add, contentDescription = "Add")
            }
        }
    ) { innerPadding ->
        Column(
            modifier = Modifier
                .padding(innerPadding),
            verticalArrangement = Arrangement.spacedBy(16.dp),
        ) {
            Text(
                modifier = Modifier.padding(8.dp),
                text =
                """
                    This is an example of a scaffold. It uses the Scaffold composable's parameters to create a screen with a simple top app bar, bottom app bar, and floating action button.

                    It also contains some basic inner content, such as this text.

                    You have pressed the floating action button $presses times.
                """.trimIndent(),
            )
        }
    }
}

```


________________________




# room

https://developer.android.com/codelabs/basic-android-kotlin-compose-persisting-data-room#12





_________________________


# service

https://www.geeksforgeeks.org/services-in-android-using-jetpack-compose/


I servizi in Android sono un componente speciale che facilita l'esecuzione di un'applicazione in background per eseguire operazioni di lunga durata. 
Lo scopo principale di un servizio è garantire che l'applicazione rimanga attiva in background, in modo che l'utente possa utilizzare più applicazioni contemporaneamente.
L'interfaccia utente non è auspicabile per i servizi Android, che sono progettati per eseguire processi di lunga durata senza alcun intervento da parte dell'utente.
Un servizio può funzionare continuamente in background anche se l'applicazione viene chiusa o l'utente passa a un'altra applicazione. 
Inoltre, i componenti dell'applicazione possono legarsi al servizio per effettuare comunicazioni interprocesso (IPC). 
Esiste una differenza sostanziale tra i servizi android e i thread, che non devono essere confusi tra loro. 
Il thread è una funzione fornita dal sistema operativo per consentire all'utente di eseguire operazioni in background.
Mentre il servizio è un componente di Android che esegue un'operazione di lunga durata di cui l'utente potrebbe non essere a conoscenza perché non dispone di un'interfaccia utente.


<img width="635" alt="Screenshot 2024-04-10 alle 21 53 47" src="https://github.com/MrMagicalSoftware/android-jetpack-compose-tutorial/assets/98833112/f386f52d-37c1-452a-9532-ae77801edd8f">


**1. Foreground Services:**

I servizi che notificano all'utente le operazioni in corso sono definiti servizi in primo piano.
Gli utenti possono interagire con il servizio grazie alle notifiche fornite sull'attività in corso. 
Ad esempio, nel caso del download di un file, l'utente può tenere traccia dell'avanzamento del download e può anche mettere in pausa e riprendere il processo.


**2. Background Services:**
I servizi in background non richiedono alcun intervento da parte dell'utente.
Questi servizi non notificano all'utente le attività in background in corso e gli utenti non possono nemmeno accedervi. 
I processi come la sincronizzazione programmata dei dati o l'archiviazione dei dati rientrano in questo servizio.



**3. Bound Services:**

Questo tipo di servizio Android consente ai componenti dell'applicazione, come le attività, di legarsi ad esso. 
I servizi vincolati svolgono il loro compito finché un componente dell'applicazione è vincolato ad esso. 
Più di un componente alla volta può legarsi a un servizio. 
Per legare un componente dell'applicazione a un servizio si utilizza il metodo bindService().


# The Life Cycle of Android Services

in Android, i servizi hanno due possibili percorsi per completare il loro ciclo di vita: Started e Bounded.<br><br>
1. Servizio avviato (servizio non vincolato):<br><br>
Seguendo questo percorso, un servizio viene avviato quando un componente dell'applicazione chiama il metodo startService().
Una volta avviato, il servizio può essere eseguito continuamente in background, anche se il componente responsabile dell'avvio del servizio viene distrutto.
Per interrompere l'esecuzione del servizio sono disponibili due opzioni:
Chiamando il metodo stopService(),
Il servizio può arrestarsi da solo utilizzando il metodo stopSelf().

2. Bounded Service:


Può essere trattato come un server in un'interfaccia client-server. 
Seguendo questo percorso, i componenti dell'applicazione Android possono inviare richieste al servizio e recuperare i risultati.
Un servizio è definito vincolato quando un componente dell'applicazione si lega a un servizio chiamando il metodo bindService().
Per interrompere l'esecuzione di questo servizio, tutti i componenti devono svincolarsi dal servizio utilizzando il metodo unbindService() .




<img width="736" alt="Screenshot 2024-04-10 alle 22 04 19" src="https://github.com/MrMagicalSoftware/android-jetpack-compose-tutorial/assets/98833112/0275d527-5b26-4887-99b5-c639319aed1b">




## Esempio di Service



When to use a Service:

Downloading or uploading data from the internet.
Playing music in the background.
Handling long-running computations or data processing.




guida utile : https://medium.com/@fierydinesh/understanding-service-and-intentservice-in-android-with-kotlin-cea76512ec16

Progetto completo su training service.

nel manifest file

```
<service android:name=".BackgroundTaskService" />

```

```
package it.zafiro.trainingservice
import android.app.Service
import android.content.Intent
import android.os.IBinder
import android.util.Log

class BackgroundTaskService : Service() {
    override fun onBind(intent: Intent?): IBinder? {
        // Nah, not today. No binding here!
        return null
    }

    override fun onCreate() {
        super.onCreate()
        log("BackgroundTaskService is ready to conquer!")
    }

    override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {
        log("BackgroundTaskService is performing a task! Don't disturb, please!")
        performLongTask()
        return START_STICKY // If the service is killed, it will be automatically restarted
    }

    private fun performLongTask() {
        // Imagine doing something that takes a long time here

        var i = 0;

        while(i < 10){
            Thread.sleep(1000)
            Log.i("info", "do some task " + i.toString())
            i++;
        }

    }

    override fun onDestroy() {
        super.onDestroy()
        log("BackgroundTaskService says goodbye!")
        Log.i("info", "i finished my task")

    }

    fun log(str:String){
        Log.d("TAG", "log: $str")
    }
}

```


Nel file main :

```
val intent = Intent(this, BackgroundTaskService::class.java)
startService(intent)
```


______________________________________________________________



**IntentService:**

An IntentService is a subclass of Service that provides a simplified way to handle asynchronous operations in the background.
It handles each intent on a worker thread and stops itself automatically when the work is done.

Key features of IntentService:

    Sequential processing of Intents: Intents are queued and processed one by one, avoiding concurrent execution of tasks.
    Automatic termination: IntentService stops itself automatically when all the Intents are processed, which makes it convenient for one-off tasks.
    Simplicity: IntentService handles thread management and execution flow, allowing developers to focus on the task implementation.

When to use an IntentService:

    Performing multiple independent tasks sequentially.
    Offloading work to a background thread without managing threads explicitly.
    Background operations triggered by Intents (e.g., processing a downloaded file, handling push notifications).

Creating an IntentService in Kotlin:
To create an IntentService in Android using Kotlin, follow these steps:

Step 1: Create a new Kotlin class that extends the `IntentService` class.
Step 2: Override the `onHandleIntent()` method, where you define the background task that the service should perform for each incoming intent.

```
import android.app.IntentService
import android.content.Intent
import android.util.Log

class IntentTaskService : IntentService("IntentTaskService") {

    override fun onHandleIntent(intent: Intent?) {
        log("IntentTaskService is on a mission to conquer a task!")
        performLongTask()
    }

    private fun performLongTask() {
        // Imagine doing something that takes a long time here
        Thread.sleep(5000)
    }

    override fun onDestroy() {
        super.onDestroy()
        log("IntentTaskService says farewell!")
    }
    
    fun log(str:String){
        Log.d("TAG", "log: $str")
    }
}
```

Using the Service and IntentService: Once you’ve created your Service and IntentService classes, you need to register them in the AndroidManifest.xml file:
```
<service android:name=".BackgroundTaskService" />
<service android:name=".MyIntentService" />
```

To start the Service or IntentService from an activity or any other component:
```
val serviceIntent = Intent(this, MyService::class.java)
startService(serviceIntent)

val intentServiceIntent = Intent(this, MyIntentService::class.java)
startService(intentServiceIntent)
```

Al posto di IntentService bisognerebbe utilizzare WorkManager
https://techmusings.optisolbusiness.com/everything-about-periodic-work-manager-android-architecture-component-76ad8b29ff68





# example_foreground_service



Aggiungi questo al manifest file


```
<uses-permission android:name="android.permission.FOREGROUND_SERVICE"></uses-permission>
<uses-permission android:name="android.permission.FOREGROUND_SERVICE_SPECIAL_USE"></uses-permission>

 <service android:name=".taskList.CountinService"
            android:exported="true"
            android:enabled="true"
            android:foregroundServiceType="specialUse"/>
```


```
package it.zafiro.trainingservice.taskList

import android.app.NotificationChannel
import android.app.NotificationManager
import android.app.PendingIntent
import android.app.Service
import android.content.Intent
import android.os.IBinder
import android.util.Log
import androidx.core.app.NotificationCompat
import it.zafiro.trainingservice.MainActivity
import it.zafiro.trainingservice.R

class CountinService : Service() {

    //attributi di classe
    private val tag = "checkCounting";
    private var counter = 0;


    //thread
    private val countingThread = object  : Thread() {
        override fun run() {

            while(true){
                try{
                    sleep(1000 * 2)
                }catch (e : Exception){
                    Log.i(tag , "exception was here")
                    break;
                }
                counter++
                Log.i(tag , "The counter is $counter")
            }

        }
    }

    override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {

        createNotificationChannel()
        val notificationIntent = Intent(this, MainActivity::class.java)

        val pendingIntent = PendingIntent.
        getActivity(this, 0, notificationIntent, PendingIntent.FLAG_MUTABLE)
        val notification = NotificationCompat.Builder(this, "counting_channel")
            .setContentTitle("Counting Service")
            .setContentText("Running...")
            .setSmallIcon(androidx.core.R.drawable.notification_bg_low_normal)
            .setContentIntent(pendingIntent)
            .build()

        startForeground(1, notification)
        return START_STICKY ;
    }

    override fun onCreate() {
        super.onCreate()
        countingThread.start()
    }

    override fun onBind(p0: Intent?): IBinder? {
        TODO("Not yet implemented")
    }


    /**
     *
     *
     *
     * Questa funzione crea un canale di notifica per il servizio di conteggio.
     * Prima controlla se il dispositivo è eseguito su una versione di Android pari
     * o superiore a Oreo (versione 8.0) in quanto i canali di notifica sono supportati
     * solo su questa versione e successive. Se il requisito è soddisfatto,
     * la funzione procede a definire il nome e la descrizione del canale,
     * nonché l'importanza delle notifiche che verranno mostrate.
     * Successivamente, crea effettivamente il canale di notifica
     * utilizzando i parametri precedentemente definiti
     * e lo registra con il sistema di notifiche tramite
     * il servizio NotificationManager.
     *
     */
    private fun createNotificationChannel() {

        if (android.os.Build.VERSION.SDK_INT >= android.os.Build.VERSION_CODES.O) {
            val name = "Counting Channel"
            val description = "Channel for counting service"
            val importance = NotificationManager.IMPORTANCE_DEFAULT
            val channel = NotificationChannel("counting_channel", name, importance)
            channel.description = description
            val notificationManager = getSystemService(NOTIFICATION_SERVICE) as NotificationManager
            notificationManager.createNotificationChannel(channel)
        }

    }


}

```

Nel file di MainActivity aggiungi questo per utilizzarlo :



```
startService(Intent(this, CountinService::class.java))
```


_________

# Navigation

dependencies {

    implementation "androidx.navigation:navigation-compose:2.4.0-alpha05"

}


```
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.material.MaterialTheme
import androidx.compose.material.Surface
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.navigation.NavHostController
import androidx.navigation.compose.NavHost
import androidx.navigation.compose.composable
import androidx.navigation.compose.rememberNavController
@Composable

fun MyApp() {

    val navController = rememberNavController()
    Surface(
        modifier = Modifier.fillMaxSize(),
        color = MaterialTheme.colors.background

    ) {

        NavHost(navController, startDestination = "home") {
            composable("home") {
                HomeScreen(navController)
            }
            composable("settings") {
                SettingsScreen(navController)
            }
        }
    }
}
```

Now, you can create the HomeScreen and SettingsScreen composables. Here's an example:


```

import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Row
import androidx.compose.foundation.layout.Spacer
import androidx.compose.foundation.layout.width
import androidx.compose.material.Button
import androidx.compose.material.Text
import androidx.compose.runtime.Composable
import androidx.navigation.NavController


@Composable

fun HomeScreen(navController: NavController) {

    Column {
        Text(text = "Home Screen")
        Spacer(modifier = Modifier.width(16.dp))
        Row {
            Button(onClick = { navController.navigate("settings") }) {
                Text(text = "Go to Settings")
            }
        }
    }
}


@Composable
fun SettingsScreen(navController: NavController) {
    Column {
        Text(text = "Settings Screen")
        Spacer(modifier = Modifier.width(16.dp))
        Row {
            Button(onClick = { navController.navigateUp() }) {
                Text(text = "Go back to Home")
            }
        }
    }
}
```


Finally, you can use the MyApp composable as the root composable of your app. Here's an example:

```
import androidx.compose.material.MaterialTheme
import androidx.compose.material.Surface
import androidx.compose.material.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.tooling.preview.Preview


@Composable
@Preview
fun MyAppPreview() {
    MyApp()
}
```

______________________


# Foreground service

Un foreground service in Android è un tipo di servizio che ha una priorità più alta rispetto ai servizi in background, 
il che significa che ha meno probabilità di essere interrotto dal sistema operativo quando ci sono risorse limitate disponibili sul dispositivo.
I foreground service vengono utilizzati per eseguire operazioni a lungo termine che sono rilevanti per l'esperienza dell'utente,
come la riproduzione di musica, il download di file, la registrazione della posizione dell'utente 
o altre attività che devono rimanere attive anche quando l'applicazione non è al primo piano.

Ci sono alcune caratteristiche importanti dei foreground service:

Notifiche: Quando un'applicazione avvia un foreground service, è necessario mostrare una notifica permanente all'utente. <br>
Questa notifica informa l'utente che un'applicazione sta eseguendo un'operazione in background.<br><br>

Priorità elevata: I foreground service hanno una priorità più elevata rispetto ai servizi in background. Questo significa che hanno meno probabilità di essere interrotti dal sistema operativo quando ci sono risorse limitate disponibili sul dispositivo.<br><br>

Richiesta di autorizzazioni: Alcune operazioni eseguite da un foreground service potrebbero richiedere autorizzazioni speciali, come ad esempio l'accesso alla posizione dell'utente o l'accesso alla memoria esterna del dispositivo.
È importante richiedere tali autorizzazioni all'utente prima di avviare il foreground service.<br><br>

Ciclo di vita: Il ciclo di vita di un foreground service è simile a quello di un normale servizio Android, ma ha una maggiore visibilità. Viene avviato chiamando il metodo startForeground() e può essere arrestato chiamando il metodo stopForeground() o stopSelf().<br><br>


# Broadcasts


I Broadcasts e i Broadcast Receivers sono componenti fondamentali del framework di Android per la comunicazione tra diverse parti dell'applicazione e del sistema operativo. Consentono di inviare e ricevere messaggi (notifiche) asincroni a livello di sistema o applicazione.
Broadcasts:

Un broadcast è un messaggio asincrono che viene inviato attraverso il sistema Android per notificare eventi o informazioni a diverse parti dell'applicazione o del sistema operativo. Questi eventi possono essere generati dall'applicazione stessa o dal sistema operativo. Ad esempio, la ricezione di un SMS, il completamento di un download o la connessione a una rete Wi-Fi sono eventi che possono generare un broadcast.


**Broadcast Receivers**:

Un BroadcastReceiver è un componente dell'applicazione che può registrarsi per ricevere specifici broadcast e rispondere ad essi. Ogni BroadcastReceiver è definito come una sottoclasse di android.content.BroadcastReceiver e deve implementare il metodo onReceive(), che viene chiamato quando il BroadcastReceiver riceve un broadcast che corrisponde al filtro di intent specificato.







Static Broadcast Receivers: These types of Receivers are declared in the manifest file and works even if the app is closed.<br>
Dynamic Broadcast Receivers: These types of receivers work only if the app is active or minimized.



**Esempio di Dynamic Broadcast Receiver**:

Creo una classe Figlia di BroadCastReceiver :


```
package it.zafiro.trainingbroadcasts

import android.content.BroadcastReceiver
import android.content.Context
import android.content.Intent
import android.provider.Settings
import android.util.Log


/**
 *
 * val isTurnenedOn = Settings.Global.getInt(...) != 0:
 *
 * Questo codice ottiene lo stato corrente della modalità aereo
 * dal sistema utilizzando Settings.Global.AIRPLANE_MODE_ON.
 * Se lo stato è 1, la modalità aereo è attivata; se è 0, la modalità aereo è disattivata.
 *
 *
 */

/**
 *
 * BroadcastReceiver AirPlaneModeReceiver
 * monitora i cambiamenti dello stato della modalità aereo del dispositivo
 * e stampa un messaggio
 * sulla console per indicare se la modalità aereo è attivata o disattivata.
 *
 */

class AirPlaneModeReceiver : BroadcastReceiver(){


    override fun onReceive(context: Context?, intent: Intent?) {

        /**
         * Questo blocco di codice verifica se l'azione del broadcast ricevuto è Intent.ACTION_AIRPLANE_MODE_CHANGED,
         * che viene inviato quando lo stato della modalità aereo del dispositivo cambia.
          */
        if(intent?.action == Intent.ACTION_AIRPLANE_MODE_CHANGED){
           val isTurnenedOn = Settings.Global.getInt(
               context?.contentResolver,
               Settings.Global.AIRPLANE_MODE_ON
           ) != 0
           println("is airplane mode enabled ? $isTurnenedOn ")
            Log.i("info" , isTurnenedOn.toString())
       }
    }


}
```


In un'altra classe registro il receiver




```
package it.zafiro.trainingbroadcasts

import android.content.Intent
import android.content.IntentFilter
import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.Surface
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.tooling.preview.Preview
import it.zafiro.trainingbroadcasts.ui.theme.TrainingBroadcastsTheme

class MainActivity : ComponentActivity() {

    private val airPlaneModeReceiver  = AirPlaneModeReceiver()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        //registro il receviver
        registerReceiver(airPlaneModeReceiver,
            IntentFilter(Intent.ACTION_AIRPLANE_MODE_CHANGED))

        setContent {
            TrainingBroadcastsTheme {
                // A surface container using the 'background' color from the theme
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    Greeting("Android")
                }
            }
        }
    }

    override fun onDestroy() {
        super.onDestroy()
        unregisterReceiver(airPlaneModeReceiver)
    }
}

@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Text(
        text = "Hello $name!",
        modifier = modifier
    )
}

@Preview(showBackground = true)
@Composable
fun GreetingPreview() {
    TrainingBroadcastsTheme {
        Greeting("Android")
    }
}


```





**Approfondimento sul broadcasting**



In Android, broadcast receivers are components that allow your app to receive and respond to system-wide broadcast messages or intents. There are two types of broadcast receivers: static and dynamic.

Static broadcast receivers are declared in the AndroidManifest.xml file and are registered to listen for specific broadcast intents. They are always active, even when your app is not running, and can receive broadcasts even if the app is not currently in the foreground.<br>

Dynamic broadcast receivers, on the other hand, are registered and unregistered at runtime within your app’s code. They offer more flexibility and control over when and how your app receives broadcasts. Here are a few reasons why dynamic broadcast receivers are preferred in certain situations:<br><br>

Context-specific behavior: Dynamic broadcast receivers allow you to register and unregister them based on specific context or conditions within your app. You can dynamically enable or disable the receiver based on user actions, such as entering or leaving a specific screen or activity. This provides more fine-grained control over when your app should listen for and respond to broadcasts.<br><br>

Resource optimization: Static broadcast receivers are always active, even if your app is not running. This can consume system resources unnecessarily, leading to increased battery drain and decreased performance.<br> By using dynamic broadcast receivers, you can activate and deactivate them as needed, reducing the overall resource consumption of your app.<br><br>

Security considerations: Registering a static broadcast receiver for certain sensitive intents can pose security risks. <br>If your app listens for a system-wide broadcast intent that contains sensitive information, malicious apps or attackers could potentially intercept that broadcast and access the information. <br>
By using dynamic broadcast receivers, you can limit the scope of the broadcast to specific components within your app, reducing the risk of sensitive data exposure.<br>

Runtime adaptability: Dynamic broadcast receivers allow your app to adapt to changing requirements or conditions. For example, if you need to modify the behavior of your receiver based on user preferences or runtime configurations, dynamic registration provides the flexibility to do so.<br><br>
It allows you to dynamically adjust the behavior of your app without requiring changes to the manifest or reinstallation of the app.<br><br>

It’s important to note that the decision to use static or dynamic broadcast receivers depends on the specific requirements and behavior of your app. In some cases, static receivers may be more suitable, especially when your app needs to respond to broadcasts regardless of its current state. However, for most scenarios, dynamic broadcast receivers offer greater flexibility and control over broadcast handling, resource usage, and security.<br><br>


**Esempio di come implementare lo static receiver**

Il progetto è chiamao TrainingStaticBroadCastReceiver.



```
package it.zafiro.trainingstaticbroadcastreceiver

import android.content.BroadcastReceiver
import android.content.Context
import android.content.Intent
import android.util.Log

class BootCompletedReceiver : BroadcastReceiver() {

    override fun onReceive(context:  Context?, intent: Intent?) {

        if(intent?.action == Intent.ACTION_BOOT_COMPLETED){
            Log.d("checkme" , "do something boot completed event received")
        }


    }


}

```

**Ora nel manifest android**


Aggiungo il permesso al file :

<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"></uses-permission> 
e aggiungo il receiver : 



file completo :
```

<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"></uses-permission>

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.TrainingStaticBroadCastReceiver"
        tools:targetApi="31">
        <activity
            android:name=".MainActivity"
            android:exported="true"
            android:label="@string/app_name"
            android:theme="@style/Theme.TrainingStaticBroadCastReceiver">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

        <receiver
            android:name=".BootCompletedReceiver"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"></action>
            </intent-filter>

        </receiver>
    </application>

</manifest>
```



Spiegazione di parte del manifest ( receiver )  :


Un  BroadcastReceiver che si attiva quando il dispositivo completa il processo di avvio (BOOT_COMPLETED).

Funzionamento :

- `<receiver>`: Questo elemento definisce un BroadcastReceiver all'interno dell'applicazione. Un BroadcastReceiver è un componente che gestisce e risponde a messaggi o "intenti" inviati dal sistema o da altre applicazioni.

- `android:name=".BootCompletedReceiver"`: Specifica il nome della classe Java o Kotlin che implementa il BroadcastReceiver. Il punto all'inizio del nome della classe indica che si trova nello stesso package dell'applicazione. Quindi, se l'applicazione ha il package "com.example.myapp", il BroadcastReceiver sarà situato in "com.example.myapp.BootCompletedReceiver".

- `android:exported="true"`: Indica che questo componente è disponibile per altri processi e applicazioni. In questo caso, il valore "true" permette al sistema operativo di avviare il BroadcastReceiver anche se l'applicazione non è in esecuzione.

- `<intent-filter>`: Definisce i tipi di intenti che il BroadcastReceiver deve ricevere. In questo caso, è specificato un intento con l'azione `android.intent.action.BOOT_COMPLETED`, che viene inviato dal sistema quando il dispositivo ha completato il processo di avvio.

- `<action android:name="android.intent.action.BOOT_COMPLETED"></action>`: Questo elemento definisce l'azione dell'intento che il BroadcastReceiver deve ricevere. Nel caso specifico, l'azione è `android.intent.action.BOOT_COMPLETED`, che viene inviata quando il dispositivo ha completato il processo di avvio.

Quindi, quando il dispositivo completa il processo di avvio, il sistema invia un intento con l'azione `android.intent.action.BOOT_COMPLETED`. Il BroadcastReceiver specificato nel codice verrà quindi attivato e potrà eseguire le azioni desiderate in risposta a questo intento, come avviare servizi, inizializzare variabili o eseguire altre operazioni necessarie dopo il riavvio del dispositivo.


Ulteriore Documentazione : https://developer.android.com/guide/topics/manifest/receiver-element

__________________________________________________________________________________________________


**Visualizzare tutto l'elenco dei receivers registrati nel telefono android**


```
package it.zafiro.trainingstaticbroadcastreceiver

import android.content.Context
import android.os.Bundle
import android.util.Log
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.Surface
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.tooling.preview.Preview
import it.zafiro.trainingstaticbroadcastreceiver.ui.theme.TrainingStaticBroadCastReceiverTheme
import android.content.ComponentName
import android.content.pm.PackageManager
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.ColumnScope
import androidx.compose.foundation.layout.padding
import androidx.compose.material3.Button
import androidx.compose.ui.unit.dp


class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            TrainingStaticBroadCastReceiverTheme {
                // A surface container using the 'background' color from the theme
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    Column {
                        Log.i("test" ,"test")
                       // Greeting("WELCOME TO STATIC RECEIVER")

                    }

                    ReceiverList(context = this )

                }
            }
        }
    }
}

@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Text(
        text = "Hello $name!",
        modifier = modifier
    )
}

@Preview(showBackground = true)
@Composable
fun GreetingPreview() {
    TrainingStaticBroadCastReceiverTheme {
        Greeting("Android")
    }
}



@Composable
fun ReceiverList(context: Context) {
    Column {
        Text("List of Registered Receivers:")
        Button(
            onClick = {
                // Call the function to list receivers
                listAllReceivers(context)
            },
            modifier = Modifier.padding(16.dp)
        ) {
            Text("List Receivers")
        }
    }
}


fun listAllReceivers(context: Context) {
    val packageManager = context.packageManager
    val packageName = context.packageName

    try {
        val packageInfo = packageManager.getPackageInfo(packageName, PackageManager.GET_RECEIVERS)
        val receivers = packageInfo.receivers

        receivers?.forEach { receiver ->
            val componentName = ComponentName(packageName, receiver.name)
            val receiverInfo = packageManager.getReceiverInfo(componentName, PackageManager.GET_META_DATA)
            val receiverName = receiverInfo.name
            Log.d("Receiver", "Receiver Name: $receiverName")
        }
    } catch (e: PackageManager.NameNotFoundException) {
        e.printStackTrace()
    }
}
```


______________________________________

**Esempio di BroadCastInternetConnections**

File con i sorgenti : TrainingBroadCastCheckInternetConnections

See this articles : 
https://medium.com/@kiitvishal89/android-listening-to-connectivity-changes-the-correct-way-a614f0d6d2af



```
package it.zafiro.trainingbroadcastcheckinternetconnections

import android.annotation.TargetApi
import android.content.BroadcastReceiver
import android.content.Context
import android.content.Intent
import android.net.ConnectivityManager
import android.net.Network
import android.net.NetworkInfo
import android.os.Build
import android.util.Log
import androidx.annotation.NonNull
import androidx.lifecycle.LiveData
import androidx.lifecycle.MutableLiveData

class NetworkChangeReceiver : BroadcastReceiver() {


    override fun onReceive(context: Context?, intent: Intent?) {
        context?.let {
            ConnectivityUtils.notifyNetworkStatus(it)
            Log.i("qui", "qui")
            
        } ?:let {
            // Handle error scenario.
        }
    }

}

// States represented as enums
enum class NetworkState(val isConnected : Boolean) {
    CONNECTED(true),
    DISCONNECTED(false),
    UNINITIALIZED(false)
}

object ConnectivityUtils {

    private val liveConnectivityState = MutableLiveData<NetworkState>()

    fun notifyNetworkStatus(ctx: Context) {
        val newState = getLatestConnectivityStatusWithContext(ctx)
        Log.i("work" , "work")
        liveConnectivityState.value = newState
    }

    private fun getLatestConnectivityStatusWithContext(ctx: Context): NetworkState {
        val isConnected = isConnected(ctx)
        return if(isConnected) {
            NetworkState.CONNECTED
        } else {
            NetworkState.DISCONNECTED
        }
    }


    fun getLiveConnectivityState() : LiveData<NetworkState> {
        return liveConnectivityState
    }

    fun isConnected(@NonNull context: Context): Boolean {
        val connMgr = context.getSystemService(Context.CONNECTIVITY_SERVICE) as ConnectivityManager
        val networkInfo: NetworkInfo? = connMgr.activeNetworkInfo
        return networkInfo != null && networkInfo.isConnected
    }

    fun isWifiConnected(@NonNull context: Context): Boolean {
        return isConnected(context, ConnectivityManager.TYPE_WIFI)
    }

    fun isMobileConnected(@NonNull context: Context): Boolean {
        return isConnected(context, ConnectivityManager.TYPE_MOBILE)
    }

    private fun isConnected(@NonNull context: Context, type: Int): Boolean {
        val connMgr = context.getSystemService(Context.CONNECTIVITY_SERVICE) as ConnectivityManager
        return if (Build.VERSION.SDK_INT < Build.VERSION_CODES.LOLLIPOP) {
            val networkInfo: NetworkInfo? = connMgr.getNetworkInfo(type)
            networkInfo != null && networkInfo.isConnected
        } else {
            isConnected(connMgr, type)
        }
    }

    @TargetApi(Build.VERSION_CODES.LOLLIPOP)
    private fun isConnected(@NonNull connMgr: ConnectivityManager, type: Int): Boolean {
        val networks: Array<Network> = connMgr.allNetworks
        var networkInfo: NetworkInfo?
        for (mNetwork in networks) {
            networkInfo = connMgr.getNetworkInfo(mNetwork)
            if (networkInfo != null && networkInfo.type == type && networkInfo.isConnected) {
                return true
            }
        }
        return false
    }

}

```

**MainActivity**

```
package it.zafiro.trainingbroadcastcheckinternetconnections

import android.content.IntentFilter
import android.net.ConnectivityManager
import android.os.Bundle
import android.util.Log
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.Surface
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.tooling.preview.Preview
import it.zafiro.trainingbroadcastcheckinternetconnections.ui.theme.TrainingBroadCastCheckInternetConnectionsTheme


class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        var connectivityReceiver = NetworkChangeReceiver()
        val intentFilter = IntentFilter(ConnectivityManager.CONNECTIVITY_ACTION)
        registerReceiver(connectivityReceiver, intentFilter)


        Log.i("start" , "start")
        setContent {
            TrainingBroadCastCheckInternetConnectionsTheme {
                // A surface container using the 'background' color from the theme
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    Column {
                        Greeting("Android")
                        ShowNetworkStatus()
                    }
                    }

                }
            }
        }
    }


@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Text(
        text = "Hello $name!",
        modifier = modifier
    )
}

@Preview(showBackground = true)
@Composable
fun GreetingPreview() {
    TrainingBroadCastCheckInternetConnectionsTheme {
        Greeting("Android")
    }
}

```


___________________________________________


## INVIARE BROADCAST APP TO APP

è un modo che hanno 2 applicationi per comunicare.

```
   Button(onClick={
      sendBroadcast(
      Intent("TEST_ACTION"))
   } )


```

Nell'altra app creo un receiver.


```

class TestReceiver : BroadcastReceiver {

   ovveride fun onReceive(contect : Context?, intent : Intent?) {
      if(intent?.action == "TEST_ACTION"){
         //Do something!!
      }
   }

}


```
Nel mainActivity dovro registrare il nuovo receiver.


______________________________________________


# TrackUserLocation







# PollingVsStreaming

see this : https://dev.to/pragyasapkota/polling-and-streaming-15h5



![Screenshot 2024-04-11 alle 14 06 56](https://github.com/MrMagicalSoftware/android-jetpack-compose-tutorial/assets/98833112/7b2812dc-7da5-4b00-9f2b-98f3431a24b5)



The internet is growing day by day. Its content is doubled every six months which means there are continuous updates, push notifications, streaming content, and real-time data for us to look at.<br><br>
These operations are carried out by either “Polling” or “Streaming” approaches. Using these technologies can have your application updated regularly or instantly.<br><br>


Polling We have heard of polling in our daily life where it means recording the opinion or vote. The second meaning of the term is to check the status of maybe a device — especially as a part of a repeated cycle.<br><br>

In the computing world, Polling means having your client check on the server by sending the server a network request. The operation is also followed by the client asking the server for the updated data. These types of requests are made in regular intervals with fixed times — 10 seconds, 20 seconds, 30 seconds, or 1 minute — depending on the prerequisites of your use case. 
However, having polling with a minimum second interval doesn’t mean it comes close to real-time.

When you have simultaneous users exceeding the number of million, some inconvenience can occur for both client and server.<br><br>

    For servers, the loads can be overwhelming with more than a million requests per second. This problem can be addressed as almost-constant network requests.<br><br>

    For clients, the almost-constant network requests are a problem.<br><br>

As we now have an idea that polling with a low interval is less efficient and thus should be used when the small gaps in the data updates will not be a problem for your application. For example, in in-driver, the driver-side app sends the location data every 5 seconds, and the rider-side app polls for the data.<br><br>


**Streaming**

Since polling was less efficient and a little problematic — STREAMING comes to the rescue.<br>

When you need to make network requests to the server in a minimum time interval, we can use “web sockets”.

Web socket is a network-communication protocol that was specially 
designed to work over Transmission Control Protocol (TCP). The 
sockets open in a two-way channel — client and server. This creates
 a hotline between them leading to two endpoints. It has a different
 mechanism as compared to TCP/IP communication because instead of
 multiple separate requests, there is a single request with the 
two-way transfer of data. And the most important leverage to have
 with the web sockets is that the connection lasts until 
either client or the server closes it or if the network drops.

We discussed IP, TCP, and HTTP when we looked for Network Protocols.
We talked about the packets of data for each request-response cycle. 
However, the web sockets work for a single request-response interaction and open a channel for the data stream. A common example to look for streaming services is Apache Kafka.
Difference between polling and streaming

In polling, clients make requests to the server by creating a pull to get the data. This happens a regular intervals. Likewise, in streaming, the client can be on standby while the server pushes the data to them. The server is streaming and sends the data every time it changes in any way. The term streaming was given because when the data change is constant, and the server sends the data every time it changes — creates a stream.<br><br>

For a better understanding, think of online multiplayer video games. If the data is not synced within milliseconds of the change, the game lags, and thus gamers face huge losses.
Conclusion

Choosing between polling and streaming is your choice which you need to determine by analyzing your use case. If it’s okay for you to have a little lag and don’t care about the real-time sync of data — go for polling but if you need your real-time data — go for streaming. However, all of this depends on your users and the use case.



_________________________________

# StreamingC#




________________________________



# Animation


implementation("com.airbnb.android:lottie-compose:4.0.0")


Crea una cartella Android resourse directory chiamata raw di tipo raw , all'interno di res.
copia il contenuto del file json.


Compososable :


```
import androidx.compose.animation.AnimatedVisibility
import androidx.compose.animation.ExperimentalAnimationApi
import androidx.compose.animation.core.animateFloat
import androidx.compose.animation.core.tween
import androidx.compose.animation.fadeIn
import androidx.compose.animation.fadeOut
import androidx.compose.foundation.layout.Box
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.material3.Button
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.runtime.setValue
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import com.airbnb.lottie.compose.LottieAnimation
import com.airbnb.lottie.compose.LottieCompositionSpec
import com.airbnb.lottie.compose.rememberLottieComposition
import it.zafiro.lottieexample.R

@Composable
fun LottieAnimationExample(modifier: Modifier = Modifier) {
    var isPlaying by remember { mutableStateOf(true) }

    val composition by rememberLottieComposition(
        LottieCompositionSpec.RawRes(R.raw.test)
    )

    Box(
        modifier = modifier.fillMaxSize(),
        contentAlignment = Alignment.Center
    ) {
        AnimatedVisibility(
            visible = isPlaying,
            enter = fadeIn(initialAlpha = 0.3f),
            exit = fadeOut()
        ) {
            LottieAnimation(
                composition = composition,
                modifier = Modifier.fillMaxSize(),

            )
        }

        Button(
            onClick = { isPlaying = !isPlaying }
        ) {
            Text(text = if (isPlaying) "Pause" else "Play")
        }
    }
}

```













_______________________________


# WorkManager

Documentazione : https://developer.android.com/develop/background-work/background-tasks/persistent/getting-started/define-work


Aggiungi alle dipendenze :

```
dependencies {
    implementation "androidx.work:work-runtime-ktx:2.7.1"
}
```

Create a SimpleWorker


```
import android.content.Context
import androidx.work.Worker
import androidx.work.WorkerParameters
import android.util.Log
import androidx.work.OneTimeWorkRequestBuilder
import androidx.work.WorkManager
import androidx.work.WorkRequest

class SimpleWorker(appContext: Context, workerParams: WorkerParameters) : Worker(appContext, workerParams) {

    override fun doWork(): Result {
        Log.d("SimpleWorker", "Doing some work...")
        // Do your work here.
        // If your work is long-running, you should use CoroutineWorker instead.
        return Result.success()
    }
}


fun scheduleWork(context: Context) {
    val simpleWorkRequest: WorkRequest = OneTimeWorkRequestBuilder<SimpleWorker>().build()
    WorkManager.getInstance(context).enqueue(simpleWorkRequest)

}

```

Nel main file :

```
scheduleWork(this)

```


# llm






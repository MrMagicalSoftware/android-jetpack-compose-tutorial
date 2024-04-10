# android-jetpack-compose-tutorial



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
[navigation](#navigation)<br>
[Broadcasts & Broadcast Receivers](#Broadcasts)<br>
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







Static Broadcast Receivers: These types of Receivers are declared in the manifest file and works even if the app is closed.
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

TrainingBroadCastCheckInternetConnections
















# android-jetpack-compose-tutorial

https://www.youtube.com/watch?v=5yde-kGgdk0&list=PLSrm9z4zp4mEWwyiuYgVMWcDFdsebhM-r&index=4

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

 


**Comandi utili**

COMMAND + p  per visionare le opzioni disponibili,
ad esempio Text(text ="ok").

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


fun ExamplePasswordTextField(): This defines a new Composable function named ExamplePasswordTextField.
var password by rememberSaveable {: This declares a mutable state variable named password using the rememberSaveable function.
The rememberSaveable function allows you to remember values across recompositions and save them in a Bundle during a configuration change.
mutableStateOf(value=""): This initializes the password variable with an empty string using the mutableStateOf function.
Column {: This creates a new Column composable, which is a layout that arranges its children in a vertical stack.
OutlinedTextField(value = password, onValueChange ={: This creates a new OutlinedTextField composable with the following properties:
value = password: This sets the value of the text field to the password variable.
onValueChange ={: This sets a callback function that is called whenever the text field's value changes.
password = it: This updates the password variable with the new value of the text field.
placeholder = {Text(text ="password")}: This sets a placeholder text that is displayed when the text field is empty.
label = {Text(text = "password")}: This sets a label text that is displayed above the text field.



```
```











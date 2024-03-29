# android-jetpack-compose-tutorial

https://www.youtube.com/watch?v=5yde-kGgdk0&list=PLSrm9z4zp4mEWwyiuYgVMWcDFdsebhM-r&index=4

##### Table of Contents  
[Introduzione](#Introduction)  
[Recomposition](#recomposition)  
[State](#State)  
[Row And Columns](#RowAndColumns)  
[Text Customization](#TextCustomization)  





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


_____________





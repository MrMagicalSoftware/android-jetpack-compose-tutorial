# android-jetpack-compose-tutorial



##### Table of Contents  
[Introduzione](#Introduction)  
[Recomposition](#recomposition)  
   




________________________________________


# Introduction


**MVVM**

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


#Recomposition

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








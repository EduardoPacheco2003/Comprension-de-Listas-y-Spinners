# Pacheco Cruz Eduardo | 6NM61

## **Comprensión de Listas y Spinners**

#### Instrucciones

A partir del ejemplo visto en clase sobre spinners, en donde se lista una serie de países, debes realizar lo siguiente:

1. Se debe hacer uno de la pantalla de selección de país, al seleccionar el país, los textos de la pantalla deben cambiar al idioma del país seleccionado.
1. Al dar click al botón debe mandar un Alert con un mensaje de Bienvenida en el idioma que selecciono.

### **Capturas de Pantalla**

#### Pantalla Principal  
![image](https://github.com/EduardoPacheco2003/Comprension-de-Listas-y-Spinners/assets/100945554/3d1f6eea-8233-4437-87ca-0476e54aa08d)  

#### Seleccion de Paises  
![image](https://github.com/EduardoPacheco2003/Comprension-de-Listas-y-Spinners/assets/100945554/f5ebc400-d413-4c83-98b9-0473c4ab60aa)  
![image](https://github.com/EduardoPacheco2003/Comprension-de-Listas-y-Spinners/assets/100945554/7a01328c-049c-4c1d-a075-cb3c4fb1b203)  
![image](https://github.com/EduardoPacheco2003/Comprension-de-Listas-y-Spinners/assets/100945554/645e5586-6c5a-4ef3-8eaf-71b22aa3695c)  
![image](https://github.com/EduardoPacheco2003/Comprension-de-Listas-y-Spinners/assets/100945554/d5ff27b3-989b-4981-b457-d571adcd6504)  
![image](https://github.com/EduardoPacheco2003/Comprension-de-Listas-y-Spinners/assets/100945554/3b3d6b85-2477-4d75-97e5-e251c7fd46c6)  


#### Mensajes de Bienvenida
México:  
![image](https://github.com/EduardoPacheco2003/Comprension-de-Listas-y-Spinners/assets/100945554/9ea3d4e6-7921-4414-935f-5721b2630607)  
USA, Cánada:  
![image](https://github.com/EduardoPacheco2003/Comprension-de-Listas-y-Spinners/assets/100945554/a4ff89e7-aefe-4043-a6c0-f782fce86006)  
Brazil:  
![image](https://github.com/EduardoPacheco2003/Comprension-de-Listas-y-Spinners/assets/100945554/e307c1f0-8e0d-4387-a5f5-4c36e0331c00)  
Alemania:  
![image](https://github.com/EduardoPacheco2003/Comprension-de-Listas-y-Spinners/assets/100945554/b6a7f7d3-5617-4837-9716-d14e61fd428f)  
Francia:  
![image](https://github.com/EduardoPacheco2003/Comprension-de-Listas-y-Spinners/assets/100945554/7454ec8d-2d79-4fa4-a488-9af825303a08)  
Italia:  
![image](https://github.com/EduardoPacheco2003/Comprension-de-Listas-y-Spinners/assets/100945554/eb7024ca-aa9f-41fc-b64f-55cb54ecfb09)  

### Codigo de la Actividad Principal

```kotlin
package com.example.listas_y_spinners

import android.os.Bundle
import android.view.View
import android.widget.*
import androidx.appcompat.app.AlertDialog
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val textSelectCountry: TextView = findViewById(R.id.text_SelectCountry)
        val buttonNext: Button = findViewById(R.id.buttonNext)
        val buttonItems = resources.getStringArray(R.array.button_texts)
        val welcomeMessagesItems = resources.getStringArray(R.array.welcome_messages)

        val spinner: Spinner = findViewById(R.id.CountrySpinner)
        val spinnerItems = listOf("Mexico", "USA", "Canada", "Brazil", "Alemania", "Francia", "Italia")

        val adapter = ArrayAdapter(this, android.R.layout.simple_spinner_item, spinnerItems)
        adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item)

        spinner.adapter = adapter;

        spinner.onItemSelectedListener = object : AdapterView.OnItemSelectedListener {
            override fun onItemSelected(parent: AdapterView<*>?, view: View?, position: Int, id: Long) {
                val selectedItem = spinnerItems[position]

                textSelectCountry.text = when (selectedItem) {
                    "Mexico" -> getString(R.string.select_country_spanish)
                    "USA" -> getString(R.string.select_country_english)
                    "Canada" -> getString(R.string.select_country_english)
                    "Brazil" -> getString(R.string.select_country_portuguese)
                    "Alemania" -> getString(R.string.select_country_german)
                    "Francia" -> getString(R.string.select_country_french)
                    "Italia" -> getString(R.string.select_country_italian)
                    else -> getString(R.string.select_country_english)

                }

                buttonNext.text = when (selectedItem) {
                    "Mexico" -> buttonItems[0]
                    "USA" -> buttonItems[1]
                    "Canada" -> buttonItems[1]
                    "Brazil" -> buttonItems[2]
                    "Alemania" -> buttonItems[3]
                    "Francia" -> buttonItems[4]
                    "Italia" -> buttonItems[5]
                    else -> buttonItems[1]
                }

                Toast.makeText(this@MainActivity, "Seleccionado: $selectedItem", Toast.LENGTH_SHORT).show()
            }

            override fun onNothingSelected(parent: AdapterView<*>?) {
                Toast.makeText(this@MainActivity, "No se ha seleccionado nada", Toast.LENGTH_SHORT).show()
            }
        }

        buttonNext.setOnClickListener {
            val selectedCountry = spinner.selectedItem.toString()
            val welcomeMessage: String = when (selectedCountry) {
                "Mexico" -> welcomeMessagesItems[0]
                "USA" -> welcomeMessagesItems[1]
                "Canada" -> welcomeMessagesItems[1]
                "Brazil" -> welcomeMessagesItems[2]
                "Alemania" -> welcomeMessagesItems[3]
                "Francia" -> welcomeMessagesItems[4]
                "Italia" -> welcomeMessagesItems[5]
                else -> welcomeMessagesItems[1]
            }
            val alertDialogBuilder = AlertDialog.Builder(this)
            alertDialogBuilder
                .setTitle(welcomeMessage)
                .setMessage(welcomeMessage)
                .setPositiveButton(android.R.string.ok) { dialog, _ ->
                    dialog.dismiss()
                }
                .show()
        }
    }
}
```

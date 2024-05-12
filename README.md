# Pacheco Cruz Eduardo | 6NM61

## **Comprensión de Listas y Spinners**

#### Instrucciones

A partir del ejemplo visto en clase sobre spinners, en donde se lista una serie de países, debes realizar lo siguiente:

1. Se debe hacer uno de la pantalla de selección de país, al seleccionar el país, los textos de la pantalla deben cambiar al idioma del país seleccionado.
1. Al dar click al botón debe mandar un Alert con un mensaje de Bienvenida en el idioma que selecciono.

### **Capturas de Pantalla**

#### Pantalla Principal

#### Seleccion de Paises

#### Mensajes de Bienvenida

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

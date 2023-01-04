# Registration/Signup Screen  with XML Interoperability

# Dependency For AndroidViewBinding With Compose
```
    implementation "androidx.compose.ui:ui-viewbinding:1.3.2"
```

# XML
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.appcompat.widget.LinearLayoutCompat xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:app="http://schemas.android.com/apk/res-auto">

    <com.google.android.material.textfield.TextInputLayout
        style="@style/Widget.Material3.TextInputLayout.FilledBox"
        android:layout_width="match_parent"
        app:hintTextAppearance="@style/TextAppearance.AppCompat.Small"
        android:layout_height="55dp">

        <com.google.android.material.textfield.MaterialAutoCompleteTextView
            android:id="@+id/atv"
            style="@style/ThemeOverlay.Material3.AutoCompleteTextView.FilledBox"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:imeOptions="actionNext"
            android:paddingStart="14dp"
            android:textStyle="bold"
            tools:ignore="RtlSymmetry" />

    </com.google.android.material.textfield.TextInputLayout>

</androidx.appcompat.widget.LinearLayoutCompat>
```

# Compose View
```

import android.annotation.SuppressLint
import android.app.DatePickerDialog
import android.os.Build
import android.widget.ArrayAdapter
import androidx.annotation.RequiresApi
import androidx.compose.foundation.*
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.shape.CutCornerShape
import androidx.compose.foundation.text.KeyboardOptions
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.DateRange
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment.Companion.CenterHorizontally
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.platform.LocalContext
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.text.TextStyle
import androidx.compose.ui.text.font.FontFamily
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.text.input.ImeAction
import androidx.compose.ui.text.input.KeyboardCapitalization
import androidx.compose.ui.text.input.KeyboardType
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.viewinterop.AndroidViewBinding
import androidx.core.widget.doOnTextChanged
import com.gulehri.screendesigncompose.R
import com.gulehri.screendesigncompose.databinding.AutoViewBinding
import com.gulehri.screendesigncompose.viewmodels.MainViewModel
import java.util.*


// Created by Shahid Iqbal on 1/3/2023.

@OptIn(ExperimentalMaterial3Api::class)
@SuppressLint("UnrememberedMutableState")
@Composable
fun SignUp(modifier: Modifier = Modifier, viewModel: MainViewModel?) {

    //Get Country Here
    val country = viewModel!!.country.collectAsState()

    var name by remember {
        mutableStateOf("")
    }
    var email by remember {
        mutableStateOf("")
    }

    var phone by remember {
        mutableStateOf("")
    }

    var city by remember {
        mutableStateOf("")
    }

    var address by remember {
        mutableStateOf("")
    }

    val fieldModifier = Modifier.fillMaxWidth()



    Column(
        modifier
            .fillMaxWidth()
            .padding(10.dp)
            .verticalScroll(rememberScrollState()),
    ) {

        Image(
            painter = painterResource(id = R.drawable.form),
            contentDescription = null,
            modifier = Modifier
                .size(80.dp)
                .padding(top = 10.dp)
                .align(CenterHorizontally)
        )

        Spacer(modifier = Modifier.height(5.dp))
        Text(
            text = "Registration Form",
            style = MaterialTheme.typography.titleLarge,
            fontWeight = FontWeight.Bold,
            color = Color.White,
            modifier = Modifier.align(CenterHorizontally)
        )

        Spacer(modifier = Modifier.height(20.dp))

        Text(text = "Name")
        TextField(
            value = name,
            onValueChange = { name = it },
            placeholder = { PlaceHolderText(text = "Mr.John") },
            modifier = fieldModifier,
            keyboardOptions = KeyboardOptions(
                capitalization = KeyboardCapitalization.Words, imeAction = ImeAction.Next
            ), textStyle = TextStyle.Default.copy(
                fontWeight = FontWeight.Bold
            )

        )

        Spacer(modifier = Modifier.height(10.dp))
        Text(text = "Email")
        TextField(
            value = email,
            onValueChange = { email = it },
            placeholder = { PlaceHolderText(text = "john@email.com") },
            modifier = fieldModifier,
            keyboardOptions = KeyboardOptions(
                keyboardType = KeyboardType.Email, imeAction = ImeAction.Next
            ),
            textStyle = TextStyle.Default.copy(
                fontWeight = FontWeight.Bold
            )
        )

        Spacer(modifier = Modifier.height(10.dp))
        Text(text = "Phone")
        TextField(
            value = phone,
            onValueChange = { phone = it },
            placeholder = { PlaceHolderText(text = "+192092929") },
            modifier = fieldModifier,
            keyboardOptions = KeyboardOptions(
                keyboardType = KeyboardType.Phone, imeAction = ImeAction.Next
            ),
            textStyle = TextStyle.Default.copy(
                fontWeight = FontWeight.Bold
            )
        )


        Spacer(modifier = Modifier.height(10.dp))
        DatePickerField(viewModel, fieldModifier)

        Spacer(modifier = Modifier.height(10.dp))
        Text(text = "Country")
        MyAutoCompleteTextView(viewModel)

        Spacer(modifier = Modifier.height(10.dp))
        Text(text = "City")
        TextField(
            value = city,
            onValueChange = { city = it },
            placeholder = { PlaceHolderText(text = "New York") },
            modifier = fieldModifier,
            keyboardOptions = KeyboardOptions(
                capitalization = KeyboardCapitalization.Words, imeAction = ImeAction.Next
            ),
            textStyle = TextStyle.Default.copy(
                fontWeight = FontWeight.Bold
            )
        )

        Spacer(modifier = Modifier.height(10.dp))
        Text(text = "Address")
        TextField(
            value = address,
            onValueChange = { address = it },
            placeholder = { PlaceHolderText(text = "XYZ Street") },
            modifier = fieldModifier,
            keyboardOptions = KeyboardOptions(
                imeAction = ImeAction.Done
            ),
            textStyle = TextStyle.Default.copy(
                fontWeight = FontWeight.Bold
            )
        )

        Spacer(modifier = Modifier.height(20.dp))
        Button(
            onClick = { }, colors = ButtonDefaults.buttonColors(
                containerColor = Color(0xFF26EC78), contentColor = Color.Black
            ), modifier = fieldModifier, shape = CutCornerShape(10.dp)
        ) {
            Text(
                text = "Register Now",
                fontWeight = FontWeight.Bold,
                fontFamily = FontFamily.Monospace,
                style = MaterialTheme.typography.labelLarge
            )
        }
    }


}

@Composable
fun MyAutoCompleteTextView(viewModel: MainViewModel) {
    AndroidViewBinding(AutoViewBinding::inflate) {
        atv.hint = "America"
        atv.setAdapter(
            ArrayAdapter(
                this.atv.context,
                android.R.layout.simple_list_item_1,
                Locale.getAvailableLocales().map { it.displayCountry }.toSet().toList()
            )
        )

        atv.doOnTextChanged { text, _, _, _ ->
            viewModel.updateCountry(text.toString())
        }
    }
}

@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun DatePickerField(
    viewModel: MainViewModel, modifier: Modifier = Modifier
) {
    val dob = viewModel.dob.collectAsState().value ?: ""
    val calendar = Calendar.getInstance()
    val dialog = DatePickerDialog(
        LocalContext.current,
        { _, year, month, dayOfMonth ->
            viewModel.updateDob("$dayOfMonth/${month + 1}/$year")
        },
        calendar[Calendar.YEAR],
        calendar[Calendar.MONTH],
        calendar[Calendar.DAY_OF_MONTH],
    ).apply {
        datePicker.maxDate = Date().time
    }

    Text(text = "Date Of Birth")
    TextField(
        value = dob,
        onValueChange = {},
        trailingIcon = {
            Icon(imageVector = Icons.Default.DateRange,
                contentDescription = null,
                modifier = Modifier.clickable {
                    dialog.show()
                })
        },
        placeholder = { PlaceHolderText(text = "22/07/2002") },
        modifier = modifier,
        readOnly = true,
        textStyle = TextStyle.Default.copy(
            fontWeight = FontWeight.Bold
        )

    )
}

@Composable
fun PlaceHolderText(text: String) = Text(text = text)


@Preview(showBackground = true)
@Composable
fun PreviewSignUp(){
    SignUp(viewModel = null)
}
```

# ViewModel
```
import androidx.lifecycle.ViewModel
import androidx.lifecycle.viewModelScope
import kotlinx.coroutines.flow.MutableStateFlow
import kotlinx.coroutines.flow.StateFlow
import kotlinx.coroutines.launch


// Created by Shahid Iqbal on 1/4/2023.

class MainViewModel : ViewModel() {

    private val _country = MutableStateFlow<String?>(null)
    val country: StateFlow<String?> get() = _country

    private val _showDialog = MutableStateFlow<Boolean>(false)
    val showDialog: StateFlow<Boolean> get() = _showDialog

    private val _dob = MutableStateFlow<String?>(null)
    val dob: StateFlow<String?> get() = _dob


    fun updateCountry(text: String?) = viewModelScope.launch { _country.emit(text) }

    fun updateDob(text: String) = viewModelScope.launch { _dob.emit(text) }

}
```

# Set Theme For Supporting Both and XML
  Add this in build.gradle
  ```
      implementation "com.google.accompanist:accompanist-themeadapter-material3:0.28.0"

  ```
  
# Activity
  ```
  import android.os.Bundle
import androidx.activity.compose.setContent
import androidx.activity.viewModels
import androidx.appcompat.app.AppCompatActivity
import androidx.compose.ui.Modifier
import com.google.accompanist.themeadapter.material3.Mdc3Theme
import com.gulehri.screendesigncompose.components.SignUp
import com.gulehri.screendesigncompose.viewmodels.MainViewModel


class MainActivity : AppCompatActivity() {
    private val viewModel  by viewModels<MainViewModel>()
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)


        setContent {
            Mdc3Theme {
                SignUp(
                    modifier = Modifier,
                    viewModel = viewModel
                )
            }

        }
    }
}

  ```

![image](https://user-images.githubusercontent.com/45350491/210542496-d5637fcf-2ec9-4cc1-ab47-a06ac8ed69cb.png)
![image](https://user-images.githubusercontent.com/45350491/210542530-d0a7d9ae-2828-4b8c-9e42-601fa5b67ee3.png)
![image](https://user-images.githubusercontent.com/45350491/210542590-31149585-1d38-4972-91b5-ae75fe7c2361.png)

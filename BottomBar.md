# Bottom Navigation Bar in Compose

```

import android.annotation.SuppressLint
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Home
import androidx.compose.material.icons.filled.Person
import androidx.compose.material.icons.filled.Settings
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.tooling.preview.Preview

// Created by Shahid Iqbal on 1/4/2023.

@SuppressLint("UnusedMaterial3ScaffoldPaddingParameter")
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun BottomBar() {


    Scaffold(
        bottomBar = {
            NavigationBar() {
                NavigationBarItem(
                    selected = true,
                    onClick = { /*TODO*/ },
                    icon = {
                        Icon(imageVector = Icons.Default.Home, contentDescription = null)
                    },
                    label = { Text(text = "Home") }
                )

                NavigationBarItem(
                    selected = false,
                    onClick = { /*TODO*/ },
                    icon = {
                        Icon(imageVector = Icons.Default.Person, contentDescription = null)
                    },
                    label = { Text(text = "Profile") }
                )

                NavigationBarItem(
                    selected = false,
                    onClick = { /*TODO*/ },
                    icon = {
                        Icon(imageVector = Icons.Default.Settings, contentDescription = null)
                    },
                    label = { Text(text = "Setting")}
                )
            }
        },
    ) {}

}

@Preview(showBackground = true)
@Composable
fun TopAppBarScrollBehavior() {
    BottomBar()
}
```
![image](https://user-images.githubusercontent.com/45350491/210554614-fcca300d-c973-4aaa-a23b-6e9c88dc2d36.png)

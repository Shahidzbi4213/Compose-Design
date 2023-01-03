# Toolbar in Compose with Badge

```

import androidx.compose.foundation.clickable
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.foundation.layout.padding
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Notifications
import androidx.compose.material.icons.filled.ShoppingCart
import androidx.compose.material3.*
import androidx.compose.runtime.Composable
import androidx.compose.runtime.remember
import androidx.compose.runtime.rememberCoroutineScope
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.text.style.TextAlign
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import kotlinx.coroutines.launch


// Created by Shahid Iqbal on 1/3/2023.

@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun TopBar(modifier: Modifier = Modifier) {


    val scope = rememberCoroutineScope()
    val snackSate = remember {
        SnackbarHostState()
    }

    Scaffold(
        snackbarHost = { SnackbarHost(hostState = snackSate) },
        topBar = {
            TopAppBar(
                colors = TopAppBarDefaults.topAppBarColors(
                    containerColor = Color(0xFF0091EA),
                    navigationIconContentColor = Color.White,
                    actionIconContentColor = Color.White,
                    titleContentColor = Color.White
                ),
                title = {
                    Text(
                        text = "Dashboard",
                        textAlign = TextAlign.Center,
                        fontWeight = FontWeight.Bold,
                        modifier = Modifier
                            .fillMaxWidth()
                    )
                },
                actions = {

                    BadgedBox(badge = {
                        Badge { Text(text = "10") }
                    }, modifier = Modifier.padding(end = 15.dp)) {

                        Icon(
                            imageVector = Icons.Default.ShoppingCart,
                            contentDescription = null,
                            modifier = Modifier.clickable {
                                scope.launch {
                                    snackSate.showSnackbar(
                                        "10"
                                    )

                                }
                            }
                        )

                    }
                },
                navigationIcon = {
                    IconButton(onClick = {
                        scope.launch {
                            snackSate.showSnackbar("Notification Clicked")
                        }
                    }) {
                        Icon(imageVector = Icons.Default.Notifications, contentDescription = null)
                    }
                }
            )
        }
    ) {
        it.calculateBottomPadding()
    }

}

@Preview(showBackground = true, backgroundColor = 0xFF0091EA)
@Composable
fun PreviewAppBar() = TopBar()

```
![image](https://user-images.githubusercontent.com/45350491/210365606-04393591-8c70-4dc8-ac39-a2bfdc45b3a0.png)

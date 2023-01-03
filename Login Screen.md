# Create Login Screen in Jetpack Compose

# Environment
N/A


```
import androidx.compose.foundation.Image
import androidx.compose.foundation.background
import androidx.compose.foundation.border
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.foundation.text.KeyboardOptions
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Email
import androidx.compose.material.icons.filled.Lock
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Alignment.Companion.CenterHorizontally
import androidx.compose.ui.Modifier
import androidx.compose.ui.draw.blur
import androidx.compose.ui.graphics.Brush
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.layout.ContentScale
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.text.input.ImeAction
import androidx.compose.ui.text.input.KeyboardType
import androidx.compose.ui.text.input.PasswordVisualTransformation
import androidx.compose.ui.text.input.VisualTransformation
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.zIndex
import androidx.constraintlayout.compose.ConstraintLayout
import com.gulehri.screendesigncompose.R
import kotlinx.coroutines.launch



@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun LoginScreen() {

    val scope = rememberCoroutineScope()
    val snackBarHostState = remember { SnackbarHostState() }


    Scaffold(
        snackbarHost = { SnackbarHost(snackBarHostState) },
    ) {
        ConstraintLayout(
            modifier = Modifier
                .fillMaxSize()
                .padding(it)
        ) {

            val (topImage, card) = createRefs()

            Image(painter = painterResource(id = R.drawable.bg),
                contentDescription = null,
                contentScale = ContentScale.FillBounds,
                modifier = Modifier
                    .blur(2.dp)
                    .fillMaxHeight()
                    .constrainAs(topImage) {
                        top.linkTo(parent.top)
                        start.linkTo(parent.start)
                        end.linkTo(parent.end)
                        bottom.linkTo(parent.bottom)
                    })


            Column(verticalArrangement = Arrangement.Center,
                modifier = Modifier
                    .padding(horizontal = 10.dp, vertical = 10.dp)
                    .zIndex(90f)
                    .constrainAs(card) {
                        top.linkTo(topImage.top)
                        start.linkTo(topImage.start)
                        end.linkTo(topImage.end)
                        bottom.linkTo(topImage.bottom)
                    }
                    .fillMaxWidth(0.9f)) {


                var email by remember { mutableStateOf("") }
                var password by remember { mutableStateOf("") }

                var showPassword by remember {
                    mutableStateOf(false)
                }

                val icon = if (showPassword) painterResource(id = R.drawable.ic_baseline_visibility)
                else painterResource(id = R.drawable.ic_baseline_visibility_off)

                val fullModifier = Modifier
                    .fillMaxWidth()
                    .padding(vertical = 5.dp)
                    .border(
                        width = 2.dp, brush = Brush.horizontalGradient(
                            listOf(Color(0xFFff9a9e), Color(0xFFD36B4D))
                        ), shape = RoundedCornerShape(30.dp)
                    )

                Text(
                    text = "Email",
                    style = MaterialTheme.typography.titleMedium,
                    color = Color.White
                )

                TextField(value = email, onValueChange = { email = it }, placeholder = {
                    Text(
                        text = "person@email.com", color = Color.LightGray
                    )
                }, keyboardOptions = KeyboardOptions(
                    keyboardType = KeyboardType.Email, imeAction = ImeAction.Next
                ), modifier = fullModifier, leadingIcon = {
                    Icon(
                        imageVector = Icons.Default.Email,
                        contentDescription = null,
                        tint = Color.White
                    )
                }, colors = TextFieldDefaults.textFieldColors(
                    containerColor = Color.Transparent,
                    focusedIndicatorColor = Color.Transparent,
                    textColor = Color.White,
                    disabledIndicatorColor = Color.Transparent,
                    unfocusedIndicatorColor = Color.Transparent,
                    cursorColor = Color.Magenta


                )
                )

                Text(
                    text = "Password",
                    style = MaterialTheme.typography.titleMedium,
                    color = Color.White
                )
                TextField(
                    value = password,
                    onValueChange = { password = it },
                    leadingIcon = {
                        Icon(
                            imageVector = Icons.Default.Lock,
                            contentDescription = null,
                            tint = Color.White
                        )
                    },
                    trailingIcon = {

                        IconButton(onClick = { showPassword = !showPassword }) {
                            Icon(painter = icon, contentDescription = null, tint = Color.White)
                        }

                    },
                    colors = TextFieldDefaults.textFieldColors(
                        containerColor = Color.Transparent,
                        focusedIndicatorColor = Color.Transparent,
                        textColor = Color.White,
                        disabledIndicatorColor = Color.Transparent,
                        unfocusedIndicatorColor = Color.Transparent,
                        cursorColor = Color.Magenta
                    ),
                    placeholder = {
                        Text(
                            text = "***************", color = Color.LightGray
                        )
                    },
                    visualTransformation = if (showPassword) VisualTransformation.None
                    else PasswordVisualTransformation(),
                    modifier = fullModifier,
                    keyboardOptions = KeyboardOptions(
                        keyboardType = KeyboardType.Password, imeAction = ImeAction.Done
                    )
                )

                Spacer(modifier = Modifier.height(10.dp))

                Button(
                    onClick = {

                        scope.launch {
                            snackBarHostState.showSnackbar(
                                message = "Logged In"
                            )
                        }

                    },
                    colors = ButtonDefaults.buttonColors(
                        containerColor = Color.Transparent,
                    )
                    ,

                    modifier = Modifier
                        .fillMaxWidth(0.7f)
                        .align(CenterHorizontally)
                        .background(
                            brush = Brush.horizontalGradient(
                                colors = listOf(Color(0xFFff9a9e), Color(0xFFD36B4D))
                            ), shape = RoundedCornerShape(30.dp)
                        ),

                    ) {
                    Text(
                        text = "Login",
                        style = MaterialTheme.typography.titleMedium,
                        color = Color.White
                    )
                }
            }

        }
    }


}


@Preview(showBackground = true)
@Composable
fun PreviewLoginCard() {
    LoginScreen()
}

```

![WhatsApp Image 2023-01-03 at 5 20 13 PM](https://user-images.githubusercontent.com/45350491/210358285-0c7fa47c-c3aa-4aa2-9a31-d64489006244.jpeg)


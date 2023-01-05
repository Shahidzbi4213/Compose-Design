```

import androidx.compose.foundation.Image
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.lazy.grid.GridCells
import androidx.compose.foundation.lazy.grid.LazyVerticalGrid
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.ShoppingCart
import androidx.compose.material3.Button
import androidx.compose.material3.Card
import androidx.compose.material3.Icon
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Alignment.Companion.CenterHorizontally
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.layout.ContentScale
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.text.style.TextAlign
import androidx.compose.ui.text.style.TextOverflow
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import com.google.accompanist.themeadapter.material3.Mdc3Theme
import com.gulehri.screendesigncompose.R


// Created by Shahid Iqbal on 1/4/2023.

@Composable
fun ProductCard(
    productName: String,
    genericName: String,
    price: String
) {
    Card(
        modifier = Modifier.size(width = 130.dp, height = 145.dp),
    ) {

        Image(
            painter = painterResource(id = R.drawable.product), contentDescription = null,
            modifier = Modifier
                .fillMaxWidth()
                .height(40.dp),
            contentScale = ContentScale.Crop
        )

        Column(
            modifier = Modifier.padding(5.dp)
        ) {


            Text(
                text = productName,
                maxLines = 1,
                fontSize = 12.sp,
                overflow = TextOverflow.Ellipsis,
                fontWeight = FontWeight.Bold
            )
            Spacer(modifier = Modifier.height(2.dp))

            Text(
                text = genericName,
                maxLines = 1,
                overflow = TextOverflow.Ellipsis,
                textAlign = TextAlign.Center,
                fontSize = 9.sp
            )

            Spacer(modifier = Modifier.height(2.dp))

            Text(
                text = price,
                textAlign = TextAlign.Right,
                fontWeight = FontWeight.Bold,
                modifier = Modifier.fillMaxWidth()
            )

            Spacer(modifier = Modifier.height(5.dp))

            Button(
                onClick = {}, shape = RoundedCornerShape(5.dp),
                modifier = Modifier
                    .fillMaxWidth()
                    .align(CenterHorizontally)
            ) {
                Icon(
                    Icons.Default.ShoppingCart,
                    contentDescription = "Cart button icon",
                    modifier = Modifier.size(15.dp),
                    tint = Color.White
                )

                Text(
                    text = "Add to cart",
                    fontSize = 9.sp
                )
            }
        }
    }
}


@Preview(showBackground = true)
@Composable
fun ShowCard() = Mdc3Theme() {

    LazyVerticalGrid(
        columns = GridCells.Fixed(2),
        contentPadding = PaddingValues(5.dp),
        verticalArrangement = Arrangement.spacedBy(16.dp),
        horizontalArrangement = Arrangement.spacedBy(16.dp)


        ) {
        items(23) {
            ProductCard(
                productName = "Rasco Product",
                genericName = "Generic Name to be display",
                price = "PKR 340"
            )
        }
    }
} 
```

![image](https://user-images.githubusercontent.com/45350491/210758848-1e3ebbd3-e3da-4162-9b48-60751d0b1763.png)


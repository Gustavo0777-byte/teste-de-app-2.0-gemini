main1
package com.example.stravaclone

import android.content.Intent
import android.os.Bundle
import android.widget.Toast
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.padding
import androidx.compose.material3.Button
import androidx.compose.material3.Scaffold
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.platform.LocalContext
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import com.example.stravaclone.ui.theme.StravaCloneTheme


class PrimeiraTela : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            StravaCloneTheme {
                MinhaTela()
            }
        }
    }
}

@Preview(showBackground = true)
@Composable
fun MinhaTela() {
    
    Scaffold(modifier = Modifier.fillMaxSize()) { innerPadding ->
        
        val context = LocalContext.current
        val nomeItem = "Batata Frita"

        
        Column(
            modifier = Modifier
                .fillMaxSize()
                .padding(innerPadding)
                .padding(16.dp),
            verticalArrangement = Arrangement.Center,
            horizontalAlignment = Alignment.CenterHorizontally
        ) {
            Text("Tela 01")


            BotaoDeAcao(
                texto = "Mostrar Alerta",
                onClick = {
                    Toast.makeText(context, "Testando o Botao!", Toast.LENGTH_LONG).show()
                }
            )

            BotaoDeAcao(
                texto = "Mudar de Tela Simples",
                onClick = {
                    val intent = Intent(context, SegundoTela::class.java)
                    context.startActivity(intent)
                }
            )

            BotaoDeAcao(
                texto = "Mudar de Tela com Information",
                onClick = {
                    val intent = Intent(context, SegundoTela::class.java)
                    intent.putExtra("nome2", nomeItem)
                    context.startActivity(intent)
                }
            )
        }
    }
}
@Composable
private fun BotaoDeAcao(texto: String, onClick: () -> Unit) {
    Button(onClick = onClick, modifier = Modifier.padding(top = 8.dp)) {
        Text(texto)
    }
}

main2

package com.example.stravaclone

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.padding
import androidx.compose.material3.Scaffold
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import com.example.stravaclone.ui.theme.StravaCloneTheme

class SegundoTela : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)


        val nomeItemRecebido = intent.getStringExtra("nome2")

        setContent {
            StravaCloneTheme {

                TelaDeDetalhes(nomeItem = nomeItemRecebido)
            }
        }
    }
}

@Composable
fun TelaDeDetalhes(nomeItem: String?) {
    Scaffold(modifier = Modifier.fillMaxSize()) { innerPadding ->
        Column(
            modifier = Modifier
                .fillMaxSize()
                .padding(innerPadding)
                .padding(16.dp),
            verticalArrangement = Arrangement.Center,
            horizontalAlignment = Alignment.CenterHorizontally
        ) {
            Text(
                text = "Segunda Tela",
                fontSize = 24.sp,
                modifier = Modifier.padding(bottom = 16.dp)
            )

            // Verifica se o parâmetro não é nulo ou vazio
            if (!nomeItem.isNullOrEmpty()) {
                Text("Informação recebida: $nomeItem")
            } else {
                Text("Nenhuma informação recebida.")
            }
        }
    }
}

@Preview(showBackground = true)
@Composable
fun PreviewTelaDeDetalhesComItem() {
    StravaCloneTheme {
        TelaDeDetalhes(nomeItem = "Batata Frita")
    }
}

@Preview(showBackground = true)
@Composable
fun PreviewTelaDeDetalhesSemItem() {
    StravaCloneTheme {
        TelaDeDetalhes(nomeItem = null)
    }
}


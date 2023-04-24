import groovy.json.JsonSlurper
import java.net.HttpURLConnection
import java.net.URL
import java.util.Scanner

def jsonSlurper = new JsonSlurper()
def cep

// solicita o cep ao usuário
Scanner sc = new Scanner(System.in)
print("Digite seu CEP: ")
cep = sc.nextInt()

try {
// faz a requisição ao serviço ViaCEP
    def url = new URL("https://viacep.com.br/ws/${cep}/json/")
    HttpURLConnection httpCon = (HttpURLConnection) url.openConnection()
    httpCon.addRequestProperty("Accept", "application/json")
    httpCon.addRequestProperty("Content-Type", "application/json")

// obtém a resposta e faz o parsing do JSON
    def parser = new JsonSlurper()
    def jsonObj = parser.parseText(httpCon.inputStream.getText())
    println(jsonObj)

// verifica se o cep é válido e atribui o valor a variável cep
    if (jsonObj.cep != null || jsonObj.cep != "") {
        cep = jsonObj.cep
    } else {
        cep = "CEP inválido"
    }

// verifica se houve erro na requisição
    if (httpCon.responseCode == 400) {
        println("Erro 400")
    }
    if (httpCon.responseCode == 500) {
        println("Erro 500")
    }

} catch (e) {
// trata o erro de requisição
    println(e.getMessage())
}

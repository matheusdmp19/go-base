# go-base

### **Instalação do GO**

Em linux:

1 - Fazer download no GO em tar.gz

Extrair e colocar o binário no PATH:

```bash
sudo tar -C /usr/local -xzf go1.8.3.linux-amd64.tar.gz

# Path de todos os usuários: /etc/profile
# Path do usuário atual em shell: /home/$USER/.bashrc
export PATH=$PATH:/usr/local/go/bin

# Para atualizar a sessão atual utilizar o comando source
```

### **Workspace**

Utilização por workspaces, que por padrão é buscado pelo GO no diretório $HOME/go

Exemplo de estrutura básica:

```bash
go

go/src

go/pkg

go/bin
```

### **Hello World**

Exemplo:

```go
package main

import "fmt"

func main() {
	fmt.Println("Olá mundo, Matheus!") // Por convenção da linguagem, todo método de pacote importado contém a primeira letra maiúscula
}
```

### **Compilação**

Dentro do diretório do código, executar conforme exemplo com o arquivo hello.go

Compilando programa:

```bash
go build hello.go
```

Compilando e executando (não gera arquivo)

```bash
go run hello.go
```

### **Convenções e informações importantes**

- A formatação do go é unica e obrigatória para que os desenvolvedores não percam tempo discutindo sobre esse ponto em um projeto, como por exemplo a abertura de chaves vem na mesma linha da função, ao tentar inseri-la na linha de baixo, teremos erro na compilação.
- Ponto e virgula no final das linhas são opções mas não são recomendados pelo GO.
- Não é possível declarar variáveis sem utilização.
- GO só aceita expressões no IF que retornem um booleano
- Em GO, o Null é igual a nil
- Variáveis de erro normalmente são chamadas de err
- _ é utilizado para descartar variáveis que não serão utilizadas e foram recebidas em retornos de funções
- Padrão cammel case em variáveis
- É uma boa prática deixar variáveis de structs (propriedades) privadas quando temos um valor sensível, e utilizar um método para manipular seu valor somente através do pacote que ela está localizada
- Podemos ver as variáveis de ambiente através do comando ‘go env’, assim conseguimos visualizar o GOROOT e o GOPATH
- Ao trabalhar com módulos no GO, podemos utilizar um repositório Git ou gerar um arquivo de módulo com o nome do mesmo com o comando ‘go mod init nomeModulo’
- Para importar um repositório como dependência utilizar o comando ‘go get -u github.com/gorilla/mux’ (exemplo com lib do gorilla mux).

### **Variáveis**

Sintaxe básica:

```go
var nome string = "Matheus"
var versao float32 = 1.1
var versao64 float64 = 1.2
var idade int = 27
var teste string // Ao declarar sem atribuir valor é assumido
// o valor inicial vazio.
// Para inteiros é assumido 0 e para float é assumido 0.0
```

Podemos ocultar o tipo da variável na declaração.

Exemplo para descobrir o tipo de uma variável:

```go
package main

import (
	"fmt"
	"reflect"
)

func main() {
	var nome = "Matheus"
	var versao float32 = 1.1
	var idade = 27
	fmt.Println("Olá,", nome, "sua idade é", idade) // Por convenção da linguagem, todo método de pacote importado contém a primeira letra maiúscula
	fmt.Println("Esse programa está na versão:", versao)

	fmt.Println("O tipo da variavel nome é", reflect.TypeOf(nome)) // Visualizar tipo de variável
}
```

Sintaxe declarador de variáveis curto:

Atribuição com :=

Exemplo:

```go
package main

import (
	"fmt"
	"reflect"
)

func main() {
	nome := "Matheus"
	versao := 1.1
	idade := 27
	fmt.Println("Olá,", nome, "sua idade é", idade) // Por convenção da linguagem, todo método de pacote importado contém a primeira letra maiúscula
	fmt.Println("Esse programa está na versão:", versao)

	fmt.Println("O tipo da variavel nome é", reflect.TypeOf(nome)) // Visualizar tipo de variável
}
```

### **Leitura de dados do usuário**

Exemplo com explicação básica:

```go
package main

import "fmt"

func main() {
	nome := "Matheus"
	versao := 1.1
	fmt.Println("Olá,", nome)
	fmt.Println("Esse programa está na versão:", versao)

	fmt.Println("1- Iniciar Monitoramento")
	fmt.Println("2- Exibir logs")
	fmt.Println("0- Sair do programa")

	var comando int
	fmt.Scanf("%d", &comando)

	fmt.Println("O comando escolhido foi", comando)

	// Função Scan permite que o reconhecimento do tipo seja implícito:
	// OBS: Se o usuário passar um tipo de dados diferente do que foi declarado na variável,
	// não tera erro e ele simplesmente não vai fazer a alteração
	fmt.Scan(&comando)

}
```

### **Condicional IF**

Sintaxe:

```go
if comando == 1 {
		fmt.Println("Monitorando...")
	} else if comando == 2 {
		fmt.Println("Exibindo Logs...")
	} else if comando == 0 {
		fmt.Println("Saindo do programa...")
	} else {
		fmt.Println("Não conheço esse comando")
	}
// Conforme exemplo, não é necessário utilizar o parenteses no IF
// Somente expressões que retornem booleano
```

### **Switch case**

Sintaxe:

```go
switch comando {
	case 1:
		fmt.Println("Monitorando...")
	case 2:
		fmt.Println("Exibindo Logs...")
	case 0:
		fmt.Println("Saindo do programa...")
	default:
		fmt.Println("Não conheço esse comando")
	}
// No GO não é necessário o break pois é implicito dentro do
// fluxo que ele entrar
```

### **Retorno de múltiplos valores em funções**

```go
func devolveNomeEIdade() (string, int) {
	nome := "Matheus"
	idade := 27
	return nome, idade
}

_, idade := devolveNomeEIdade() // utilizando o _ para descartar um retorno
fmt.Println(idade)

// Ou para salvar ambos valores:
nome, idade := devolveNomeEIdade()
fmt.Println(idade)
```

### Laço FOR

Sintaxe loop infinito:

```go
// Loop básico sem intruções (similar ao while, que não existe no go):
for {
}
```

For tradicional e com range:

```go

sites := []string{"https://www.alura.com.br",
		"https://www.caelum.com.br",
		"https://www.google.com.br"}
// criado slice com strings de sites

	for i := 0; i < len(sites); i++ {
		fmt.Println(sites[i])
	}

// utlizando range, que retorna indice e valor:
for i, site := range sites {
		fmt.Println("Estou passando pela posição", i, "que está localicado o site", site)
	}
```

### Array e Slices

Exemplo Array:

```go
var sites [4]string
	sites[0] = "https://www.alura.com.br"
	sites[1] = "https://www.caelum.com.br"
	sites[2] = "https://www.google.com.br"
// Todo array deve conter o tamanho na declaração
```

Exemplo Slice:

```go
func exibeNomes() {
    nomes := []string{"Douglas", "Daniel", "Bernardo"}
    fmt.Println("O meu slice tem", len(nomes), "itens")
    fmt.Println("O meu slice tem capacidade para", cap(nomes), "itens")

    nomes = append(nomes, "Aparecida")
    fmt.Println("O meu slice tem", len(nomes), "itens")
    fmt.Println("O meu slice tem capacidade para", cap(nomes), "itens")
}
// O Slice é uma abstração para facilitar o uso de arrays, mas no backend 
// ele cria utilizar arrays. Sempre que você adiciona um item e o array já
// atingiu a capacidade, ele dobra a capacidade por debaixo dos panos
```

### **Leitura de arquivos:**

```go
// Método 1:
import "os"
arquivo, err := os.Open("sites.txt")
// retorna o ponteiro do arquivo

// Fechando arquivo:
arquivo.Close()

// Método 2:
import "io/ioutil"
arquivo, err := ioutil.ReadFile("sites.txt") // Não é necessário fechar, pois a lib já faz isso
// retorna todos os bytes, e utilizando uma conversão para string temos o 
// conteudo do arquivo inteiro:
fmt.Println(string(arquivo))

// Método 3:
import "bufio"

// Ler os caracteres até determinado ponto, onde nesse exemplo foi 
// realizada a leitura da primeira linha do arquivo:
leitor := bufio.NewReader(arquivo)

	linha, err := leitor.ReadString('\n')

	if err != nil {
		fmt.Println(err)
	}

	fmt.Println(linha)

// Fechando arquivo:
arquivo.Close()
```

### **Projeto Monitoramento**

```go
package main

import (
	"bufio"
	"fmt"
	"io"
	"io/ioutil"
	"net/http"
	"os"
	"strconv"
	"strings"
	"time"
)

const monitoramentos = 3
const delay = 5

func main() {

	exibeIntroducao()
	for {

		exibeMenu()

		comando := leComando()

		switch comando {
		case 1:
			iniciarMonitoramento()
		case 2:
			fmt.Println("Exibindo Logs...")
			imprimeLogs()
		case 0:
			fmt.Println("Saindo do programa...")
			os.Exit(0)
		default:
			fmt.Println("Não conheço esse comando")
			os.Exit(-1)
		}
	}
}

func exibeIntroducao() {
	nome := "Matheus"
	versao := 1.1
	fmt.Println("Olá,", nome)
	fmt.Println("Esse programa está na versão:", versao)
}

func exibeMenu() {
	fmt.Println("1- Iniciar Monitoramento")
	fmt.Println("2- Exibir logs")
	fmt.Println("0- Sair do programa")
}

func leComando() int {
	var comandoLido int
	fmt.Scan(&comandoLido)
	fmt.Println("O comando escolhido foi", comandoLido)
	fmt.Println("")

	return comandoLido
}

func iniciarMonitoramento() {
	fmt.Println("Monitorando...")

	// sites := []string{"https://www.alura.com.br",
	// 	"https://www.caelum.com.br",
	// 	"https://www.google.com.br"}

	sites := leSitesDoArquivo()

	for i := 0; i < monitoramentos; i++ {
		for i, site := range sites {
			fmt.Println("Testando site", i, ":", site)
			testaSite(site)
		}
		fmt.Println("")
		time.Sleep(delay * time.Second)
	}

	fmt.Println("")
}

func testaSite(site string) {

	resp, err := http.Get(site)

	if err != nil {
		fmt.Println("Ocorreu um erro na função testaSite:", err)
	}

	if resp.StatusCode == 200 {
		fmt.Println("Site:", site, "carregado com sucesso!")
		registraLog(site, true)
	} else {
		fmt.Println("Site:", site, "está com problemas! StatusCode:", resp.StatusCode)
		registraLog(site, false)
	}

}

func leSitesDoArquivo() []string {

	var sites []string

	arquivo, err := os.Open("sites.txt")

	if err != nil {
		fmt.Println(err)
	}

	leitor := bufio.NewReader(arquivo)

	for {

		linha, err := leitor.ReadString('\n')

		linha = strings.TrimSpace(linha)

		sites = append(sites, linha)

		fmt.Println(linha)

		if err == io.EOF {
			break
		}
	}

	arquivo.Close()

	return sites
}

func registraLog(site string, status bool) {

	arquivo, err := os.OpenFile("log.txt", os.O_RDWR|os.O_CREATE|os.O_APPEND, 0666)

	if err != nil {
		fmt.Println(err)
	}

	arquivo.WriteString(time.Now().Format("02/01/2006 15:04:05") + " - " + site + " - online: " + strconv.FormatBool(status) + "\n")

	arquivo.Close()
}

func imprimeLogs() {

	arquivo, err := ioutil.ReadFile("log.txt")

	if err != nil {
		fmt.Println(err)
	}

	fmt.Println(string(arquivo))
}
```

## Orientação a Objetos

### **Struct**

```go
// Uma struct é similar a uma classe, porém definimos somentes as propriedades dento das chaves
// As funções são declaradas de forma idenpendentes, porém fazem o vínculo através de ponteiros. Exemplo mais a baixo 

// Exemplo declaração
type ContaCorrente struct {
	titular       string
	numeroAgencia int
	numeroConta   int
	saldo         float64
}
// Exemplos de uso:

// Main

// var contaDoMatheus ContaCorrente = ContaCorrente{}
// com atribuição simples e Zero-initialization:
// contaDoMatheus := ContaCorrente{}

// Passando valores:
// contaDoMatheus := ContaCorrente{titular: "Matheus",
// 	numeroAgencia: 589,
// 	numeroConta:   123456,
// 	saldo:         125.5}

// Quando eu for popular todos os campos posso passar somente os valores:
contaDoMatheus := ContaCorrente{"Matheus", 589, 123456, 125.5}
contaDoLucas := ContaCorrente{"Lucas", 125, 222555, 222.7}

fmt.Println(contaDoMatheus, contaDoLucas)
```

### New e ponteiros

```go
// Exemplo:

type ContaCorrente struct {
	titular       string
	numeroAgencia int
	numeroConta   int
	saldo         float64
}

// Main

// var contaDaCris *ContaCorrente
	
// contaDaCris = new(ContaCorrente)
// contaDaCris.titular = "Cris"
// contaDaCris.saldo = 12.8

// // mostrando o endereço de memória
// fmt.Println(contaDaCris)

// // ou para mostrar o conteudo diretamente
// fmt.Println(*contaDaCris)

var contaDaCris *ContaCorrente

	contaDaCris = new(ContaCorrente)
	contaDaCris.titular = "Cris"
	contaDaCris.saldo = 12.8

	var contaDaCris2 *ContaCorrente

	contaDaCris2 = new(ContaCorrente)
	contaDaCris2.titular = "Cris"
	contaDaCris2.saldo = 12.8

	fmt.Println(contaDaCris, contaDaCris2)
	fmt.Println(&contaDaCris, &contaDaCris2)
	fmt.Println(*contaDaCris, *contaDaCris2)

	fmt.Println(contaDaCris == contaDaCris2)
	fmt.Println(*contaDaCris == *contaDaCris2)
```

### **Funções variádicas (com número indeterminado de parâmetros)**

```go
package main

import (
    "fmt"
)

func Somando(numeros ...int) int {
    resultadoDaSoma := 0
    for _, numero := range numeros {
        resultadoDaSoma += numero
    }
    return resultadoDaSoma
}

func main() {
    fmt.Println(Somando(1))
    fmt.Println(Somando(1,1))
    fmt.Println(Somando(1,1,1))
    fmt.Println(Somando(1,1,2,4))
}

// Nesse exemplo a função pode ser passado com qualqur quantidade, inclusive sem parametro.
```

### **Funções com multiplos retornos**

Exemplo:

```go
package main

import "fmt"

type ContaCorrente struct {
	titular       string
	numeroAgencia int
	numeroConta   int
	saldo         float64
}

func (c *ContaCorrente) Sacar(valorDoSaque float64) string {
	podeSacar := valorDoSaque > 0 && valorDoSaque <= c.saldo

	if podeSacar {
		c.saldo -= valorDoSaque
		return "Saque realizado com sucesso!"
	} else {
		return "Saldo insuficiente!"
	}
}

// Função com multiplos retornos:

func (c *ContaCorrente) Depositar(valorDoDeposito float64) (string, float64) {

	if valorDoDeposito > 0 {
		c.saldo += valorDoDeposito
		return "Depósito realizado!", c.saldo
	} else {
		return "O valor do depósito é menor do que 0!", c.saldo
	}

}

func main() {

	contaDaSilvia := ContaCorrente{}
	contaDaSilvia.titular = "Silvia"
	contaDaSilvia.saldo = 500

	fmt.Println(contaDaSilvia.saldo)

	fmt.Println(contaDaSilvia.Sacar(200))
	fmt.Println(contaDaSilvia.saldo)

	status, valor := contaDaSilvia.Depositar(500)

	fmt.Println(status, valor)

}
```

### **Outro exemplo com funções e ponteiros**

```go
package main

import "fmt"

type ContaCorrente struct {
	titular       string
	numeroAgencia int
	numeroConta   int
	saldo         float64
}

func (c *ContaCorrente) Sacar(valorDoSaque float64) string {
	podeSacar := valorDoSaque > 0 && valorDoSaque <= c.saldo

	if podeSacar {
		c.saldo -= valorDoSaque
		return "Saque realizado com sucesso!"
	} else {
		return "Saldo insuficiente!"
	}
}

// Função com multiplos retornos:

func (c *ContaCorrente) Depositar(valorDoDeposito float64) (string, float64) {

	if valorDoDeposito > 0 {
		c.saldo += valorDoDeposito
		return "Depósito realizado!", c.saldo
	} else {
		return "O valor do depósito é menor do que 0!", c.saldo
	}
}

func (c *ContaCorrente) Transferir(valorDaTransferencia float64, contaDestino *ContaCorrente) bool {
	if valorDaTransferencia <= c.saldo && valorDaTransferencia > 0 {
		c.saldo -= valorDaTransferencia
		contaDestino.Depositar(valorDaTransferencia)
		return true
	} else {
		return false
	}
}

func main() {

	contaDaSilvia := ContaCorrente{titular: "Silvia", saldo: 300}
	contaDoGustavo := ContaCorrente{titular: "Gustavo", saldo: 100}

	fmt.Println(contaDaSilvia, contaDoGustavo)
	status := contaDaSilvia.Transferir(200, &contaDoGustavo)

	fmt.Println(status)
	fmt.Println(contaDaSilvia, contaDoGustavo)

}
```

### **Pacotes e visibilidade:**

```go
// Estrutura:
// /home/$USER/go/src/banco/main.go:

package main

import (
	"banco/contas" // podemos usar um alias também
	"fmt"
)

// exemplo de import com alias: c "banco/contas"

func main() {

	contaDaSilvia := contas.ContaCorrente{Titular: "Silvia", Saldo: 300}
	contaDoGustavo := contas.ContaCorrente{Titular: "Gustavo", Saldo: 100}

	fmt.Println(contaDaSilvia, contaDoGustavo)
	status := contaDaSilvia.Transferir(200, &contaDoGustavo)

	fmt.Println(status)
	fmt.Println(contaDaSilvia, contaDoGustavo)

}

// /home/$USER/go/src/banco/contas/contaCorrente.go:

package contas

// Variaveis e funções tem que começar com a letra maiuscula para terem visibilidade publica, caso contrário serão privadas (atributos public/private)
type ContaCorrente struct {
	Titular       string
	NumeroAgencia int
	NumeroConta   int
	Saldo         float64
}

func (c *ContaCorrente) Sacar(valorDoSaque float64) string {
	podeSacar := valorDoSaque > 0 && valorDoSaque <= c.Saldo

	if podeSacar {
		c.Saldo -= valorDoSaque
		return "Saque realizado com sucesso!"
	} else {
		return "Saldo insuficiente!"
	}
}

// Função com multiplos retornos:

func (c *ContaCorrente) Depositar(valorDoDeposito float64) (string, float64) {

	if valorDoDeposito > 0 {
		c.Saldo += valorDoDeposito
		return "Depósito realizado!", c.Saldo
	} else {
		return "O valor do depósito é menor do que 0!", c.Saldo
	}
}

func (c *ContaCorrente) Transferir(valorDaTransferencia float64, contaDestino *ContaCorrente) bool {
	if valorDaTransferencia <= c.Saldo && valorDaTransferencia > 0 {
		c.Saldo -= valorDaTransferencia
		contaDestino.Depositar(valorDaTransferencia)
		return true
	} else {
		return false
	}
}
```

### **Composição e encapsulamento**

```go
// No GO não existe herança, então usamos composições entre structs.
// Exemplo:

// Modulo clientes
package clientes

type Titular struct {
	Nome      string
	Cpf       string
	Profissao string
}

// Módulo contas
package contas

import "banco/clientes"

type ContaCorrente struct {
	Titular       clientes.Titular
	NumeroAgencia int
	NumeroConta   int
	Saldo         float64
}

// Main
package main

import (
	"banco/clientes"
	"banco/contas"
	"fmt"
)

func main() {

	// contaDoBruno := contas.ContaCorrente{Titular: clientes.Titular{
	// 	Nome:      "Bruno",
	// 	Cpf:       "123.111.123.12",
	// 	Profissao: "Desenvolvedor"},
	// 	NumeroAgencia: 123, NumeroConta: 123456, Saldo: 100}

	clienteBruno := clientes.Titular{"Bruno", "123.111.123.12", "Desenvolvedor Go"}
	contaDoBruno := contas.ContaCorrente{clienteBruno, 123, 123456, 100}

	fmt.Println(contaDoBruno)

}

```

### **Interfaces**

```go
// Uma interface é a definição de um conjunto de métodos comuns a um ou mais tipos. É o que permite a criação de tipos polimórficos em Go.
// Exemplo utilizando a interface para verificar a conta e pagar um boleto com o método sacar
package main

import (
	"banco/contas"
	"fmt"
)

func PagarBoleto(conta VerificarConta, valorDoBoleto float64) {
	conta.Sacar(valorDoBoleto)
}

type VerificarConta interface {
	Sacar(valor float64) string
}

func main() {

	contaDoDenis := contas.ContaPoupanca{}
	contaDoDenis.Depositar(100)
	PagarBoleto(&contaDoDenis, 60)

	fmt.Println(contaDoDenis.ObterSaldo())

	contaDaLuiza := contas.ContaPoupanca{}
	contaDaLuiza.Depositar(100)
	PagarBoleto(&contaDaLuiza, 60)

	fmt.Println(contaDaLuiza.ObterSaldo())
}
```

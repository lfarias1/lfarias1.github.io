# Funções "Built-in"

Quando vamos usar Python, existe uma série de funções que estão disponíveis sem a necessidade de usar o comando `import` ou de definí-las individualmente. Essas funções são chamadas de "built-in functions", ou seja, funções que já estão construídas dentro do próprio Python. Essas funções oferecem funcionalidades diversas, o que ajuda a explicar porque Python é uma linguagem usada em diversas tarefas distintas.

Como existem muitas funções, somente escreverei sobre algumas delas. Para consultar extensivamente, pode-se visitar [a documentação oficial](https://docs.python.org/3/library/functions.html). 

Para se utilizar tais funções, é só usar o nome da função e, entre parênteses, os parâmetros necessários. Cada função exige um conjunto específico de parâmetros. Por exemplo:


```python
int(1.0)
```




    1



Dependendo do projeto, algumas funções são mais usadas que outras. Entretanto, há algumas funções que são usadas em muitos contextos diferentes, de modo que priorizarei estas. São elas:

* type, int, float, complex, str
* max, min, sum, round
* bool, any, all
* print
* open
* help
* filter, map

## Variáveis

Para definirmos variáveis em Python, como regra geral, escrevemos um código da forma `nome_da_variavel = valor`. O próprio Python já identifica o tipo de variável em função do valor, não sendo assim necessário explicitar isso. 


```python
variavel_1 = 1
```

Para identificarmos o tipo da variável `variavel_1`, podemos usar o comando `type(nome_da_variavel)`.


```python
type(variavel_1)
```




    int



Entretanto, pode ser que queiramos modificar o tipo de uma variável. Para isso, podemos usar as funções `int`, `float`, `complex`, `str`. Assim, as variáveis assumem os tipos inteiro, fracionário, complexo ou texto, respectivamente.


```python
v1_int = int(variavel_1)
v1_float = float(variavel_1)
v1_complex = complex(variavel_1)
v1_str = str(variavel_1)
```


```python
v1_int, v1_float, v1_complex, v1_str
```




    (1, 1.0, (1+0j), '1')




```python
type(v1_int), type(v1_float), type(v1_complex), type(v1_str), 
```




    (int, float, complex, str)



## Funções Matemáticas

Agora que já conhecemos algumas funções relacionadas aos tipos de variável, vamos conhecer algumas funções que realizam operações matemáticas. Vale destacar que algumas operações não precisam de funções, pois podem ser realizadas usando os sinais matemáticos. Por exemplo:


```python
1 + 2
```




    3



Em outros casos, usar funções podem poupar muito esforço, principalmente quando estamos lidando com coleções (ou seja, variáveis que armazenam outras variáveis). Por exemplo:


```python
lista = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
lista
```




    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]



Se quisermos identificar o maior valor da lista sem usar funções prontas, precisaríamos criar loops e percorrer a lista inteira manualmente. Um código para isso seria:


```python
maior_elemento = None
for elemento in lista:
    if not maior_elemento:
        maior_elemento = elemento
    elif elemento > maior_elemento:
        maior_elemento = elemento
maior_elemento
```




    10



O Python, entretanto, nos oferece uma forma mais simples de fazer isso: a função `max`


```python
max(lista)
```




    10



De forma análoga, existe a função `min`.


```python
min(lista)
```




    1



Para a soma, seria possível usarmos o código abaixo, que não é muito extenso.


```python
soma = 0
for elemento in lista:
    soma += elemento
soma
```




    55



Mas seria bem mais fácil usar a função `sum`


```python
sum(lista)
```




    55



Uma informação interessante é que usar as funções do próprio Python geralmente é bem mais rápido que usar funções definidas pelo programador:


```python
def soma(colecao):
    soma_total = 0
    for elemento in colecao:
        soma_total += elemento
    return soma_total
```


```python
%%timeit
soma(lista)
```

    942 ns ± 18.1 ns per loop (mean ± std. dev. of 7 runs, 1000000 loops each)
    


```python
%%timeit
sum(lista)
```

    438 ns ± 14.4 ns per loop (mean ± std. dev. of 7 runs, 1000000 loops each)
    

Além dessas funções, outra função comumente usada é a função `round`, que permite arredondar números com a precisão que se queira.


```python
round(9.123456789)
```




    9




```python
round(9.123456789, 2)
```




    9.12




```python
round(9.123456789, 5)
```




    9.12346



## Variáveis booleanas 

Além das variáveis numéricas e das strings, outro tipo importante é o `bool`. Essas variáveis assumem somente os valores `True` (verdadeiro) e `False` (falso). São variáveis importantes para a criação de sequências lógicas.


```python
variavel_verdadeira = True
variavel_falsa = False
```


```python
type(variavel_verdadeira)
```




    bool



Uma característica interessante das variáveis booleanas é que em alguns casos não é necessário definir explicitamente o valor. Por exemplo:

* 0 é entendido como False e 1 como True
* Uma lista vazia é entendida como False, uma lista não-vazia como True
* O valor None é entendido como False, qualquer outro valor (exceto 0) como True.


```python
bool(0), bool(1)
```




    (False, True)




```python
bool([]), bool([1, 2, 3])
```




    (False, True)




```python
bool(None), bool(20)
```




    (False, True)



Quando temos uma coleção de variáveis booleanas, podemos usar as funções `any` e `all` para descobrirmos se pelo menos um valor é True ou se todos os valores são True, respectivamente.


```python
lista_bools = [True, False, True]
```


```python
any(lista_bools)
```




    True




```python
all(lista_bools)
```




    False



## Print

Uma das principais funções do Python é a função print. Essa função escreve um texto na tela. Dessa forma, é possível verificar o valor de uma variável ou mostrar uma mensagem dentro de condicionais.


```python
print("Mostre este texto na tela!")
```

    Mostre este texto na tela!
    


```python
var_bool = True
if var_bool:
    print("A variável é verdadeira")
else:
    print("A variável é falsa")
```

    A variável é verdadeira
    


```python
var_bool = False
if var_bool:
    print("A variável é verdadeira")
else:
    print("A variável é falsa")
```

    A variável é falsa
    

## Leitura e escrita

É possível escrever e ler arquivos do computador no Python. Para isso, existe a função `open`. Essa função possui dois principais argumentos: o nome (e caminho) do arquivo que se deseja escrever/ler e o que se deseja fazer com esse arquivo ("r" para ler, "w" para escrever, "a" para incluir, etc.)


```python
escrever_arquivo = open("arquivo.txt", "w")
```


```python
escrever_arquivo.write("Essa linha foi escrita pelo usuário.\n")
```




    37




```python
escrever_arquivo.close()
```


```python
incluir_arquivo = open("arquivo.txt", "a")
```


```python
incluir_arquivo.write("Essa é a segunda linha escrita pelo usuário!")
```




    44




```python
incluir_arquivo.close()
```


```python
ler_arquivo = open("arquivo.txt", "r")
```


```python
conteudo = ler_arquivo.read()
```


```python
print(conteudo)
```

    Essa linha foi escrita pelo usuário.
    Essa é a segunda linha escrita pelo usuário!
    


```python
ler_arquivo.close()
```

O que aconteceu foi o seguinte:
* Foi criado um arquivo com o nome arquivo.txt na máquina.
* Uma linha foi incluída no arquivo.
* A operação de escrita foi encerrada.
* Foi iniciada uma operação de inclusão de texto.
* Outra linha foi incluída.
* A sessão de inclusão foi encerrada.
* Foi iniciada uma sessão de leitura.
* O arquivo foi lido na variável `conteudo`.
* A variável `conteúdo` foi printada na tela.
* A sessão de leitura foi encerrada.

## Explorando o ambiente

Já vimos diversas funções. Mas e o que faremos quando tivermos dúvidas sobre alguma dessas funções? Neste caso, a função `help` pode nos ajudar. Essa função nos dá detalhes sobre as funções conforme escrito na documentação dela.


```python
help(sum)
```

    Help on built-in function sum in module builtins:
    
    sum(iterable, start=0, /)
        Return the sum of a 'start' value (default: 0) plus an iterable of numbers
        
        When the iterable is empty, return the start value.
        This function is intended specifically for use with numeric values and may
        reject non-numeric types.
    
    

Isso é válido inclusive para funções criadas pelo programador, desde que haja comentário nelas. Por exemplo:


```python
def somar(colecao):
    "Função que soma todos os elementos de uma coleção."
    return sum(colecao)
```


```python
help(somar)
```

    Help on function somar in module __main__:
    
    somar(colecao)
        Função que soma todos os elementos de uma coleção.
    
    

## Funções para lidar com coleções

Como costumamos lidar com coleções, há algumas funções que nos ajudam com isso. Por exemplo, imagine que possuímos uma lista e queremos aplicar uma determinada função a todos os elementos desta lista. Para isso, usarmos a função `map`.


```python
def funcao_lista(numero):
    "Esta função eleva o número ao quadrado e soma 10."
    return numero ** 2 + 10
```


```python
lista
```




    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]




```python
map(funcao_lista, lista)
```

    <map object at 0x0000027864E57F08>
    

Observe que o resultado da operação anterior não é uma lista, mas um objeto chamado map. Para transformarmos este objeto em uma lista, podemos usar a função `list`.


```python
list(map(funcao_lista, lista))
```




    [11, 14, 19, 26, 35, 46, 59, 74, 91, 110]



Outra ação muito comum é filtrar os elementos de uma lista, de modo a obtermos somente aqueles que satisfazem uma determinada condição.


```python
def lista_condicao(numero):
    "Retorna True quando o número é par e False caso contrário."
    return bool(numero % 2)
```


```python
filter(lista_condicao, lista)
```




    <filter at 0x27865301b08>



Assim como no caso anterior, podemos usar a função `list` para transformarmos o objeto anterior em uma lista.


```python
list(filter(lista_condicao, lista))
```




    [1, 3, 5, 7, 9]



## Considerações Finais

Este material explorou algumas funções do Python. Existem diversas funções que não foram abordadas aqui, mas acredito que com essas será possível iniciar a jornada no Python. 

Fonte: https://docs.python.org/3/library/functions.html

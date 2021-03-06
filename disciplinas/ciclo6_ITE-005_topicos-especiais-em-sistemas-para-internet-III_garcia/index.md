---
layout: disciplina
title:  "Tópicos especiais em sistemas para Internet III (Tema: Programação funcional - Haskell)"
sigla: ITE-005
teacher: Garcia
date:   2015-02-01
grade: 2013
ciclo: 6
fatec: fatec-rl
categories: grade-2013 ciclo-6
---

***

## Material, Apostilas e Ferramentas

- [Informações IDEs Haskell](https://wiki.haskell.org/IDEs)
- Compilador GHC (The Gorious Glasgow Haskell Compiler) 7.10.2 - obrigatório
- IDE Eclipse FP (Eclipse for funcional programming) - opcional
- Plugin para *highlightinhg* (Colorer plugin for Eclipse IDE) - opcional
- [tutorialspoint](http://www.tutorialspoint.com/)
- [Compilador de Haskell Online](http://www.tutorialspoint.com/compile_haskell_online.php)
- [http://www.tutorialspoint.com/](http://www.tutorialspoint.com/)
- [haskell-plataform](https://www.haskell.org/platform/) (INSTALADOR WINDOWS)
- [https://github.com/Webschool-io/workshop-js-funcional-free](https://github.com/Webschool-io/workshop-js-funcional-free)

***

## TPs e Provas

### Datas:
- Prova final: 30/11/15 
- Trabalho: 07/12/15  
- Prova substituta: 14/12/15    

### Peso:
- Prova final: 50%
- Trabalho: página web, 30%
- Lista de exercícios e atividades: 20%
- Cálculo da média final: **Mf**=(*A1*+*A2*)/*2*, onde **A1**=(*P1*+*P2*)/*2* e **A2**=(*3T*+*2L*)/*5*

***

## Ementa
Intodução a linguagem Haskell. Operações com listas. List comprehension. Tipos e TypeClasses. Map, Reduce, Fold, e Filter. Pattern Matching e Guards. Recursão e funções de alta ordem. Criando Typeclasses. Estrutura de dados recursivas. I/O. Funtores e Monoids. **Monoids**. Framework para desenvolvimento Web. Conexão com o banco de dados. Deploy de uma aplicação na Web. Testes.

*A partir de Monoids começa a entrada de código impuro na programação Haskell*

***

## Referências
- LIPOVACA, Miran. Learn you a Haskell for a Great good, 2015. (Versão pt: Aprendar Haskell por um bem maior (super didático));
- SINOYMAN, Michael. Developing Web Aplications with Haskell and Yesod;
- Safety-Driven Web Development. Oreilly, 2012;
- O'SULLIVAN, Bryan. Real World Haskell. Oreilly, 2008.

***

## Comandos

### Terminal
- **let**: defini o valor de uma "variável"
- **: (chamado *cons*)**: adiciona o número/caracter na frente do vetor
- **++ (como identação)**: adiciona número/caracter em qualquer lugar do vetor. ```let a=[1,2] | let b=[3,4] | a ++ b  // [1,2,3,4]```
- **' (aspas simples)**: representa string
- **" (aspas duplas)**: representa vetor
- **!!**: deterninar a posição do vertor: ```a!!4 == a[4]```
- **take**: pegar (pega parte do código)
- **drop**: solta (ignora uma parte do código)
- **cycle**: loop infinito (porém, pode ser definido até onde vai com o take: ```take 10 (cycle[1,2,3]) //[1,2,3,1,2,3,1,2,3,1])```
- **reverse**: irá apresentar os resultados ao contrários. Ex.: ```reverse fatec //cetaf```
- **( )**: funciona como o operador matemático. Indica "por onde começar/dar preferencia". ```let y= fatec santos | take 3 (drop 4 y) | take 3 (c santos) | take 3 c santos | //c s``` 
- **$**: dá preferencia para a próxima função. Substitui o uso do *()*
- **/=**: sinal de negação / diferente
- **,** (virgula): funciona como elemento *and*
- **notElem**: Retira os caracteres (numeral, letra) da função
- **--**: Comentário em uma linha
- **{-** lalala **-}**: Comentário em múltiplas linhas



***

## Aulas e Atividades

- [Lista 1 - Adam](https://github.com/fatechub/fatecrl-curso-si/blob/gh-pages/disciplinas/ciclo6_ITE-005_topicos-especiais-em-sistemas-para-internet-III_garcia/TP1Adam.hs) nota: 100.00
- [Lista 2 - Adam](https://github.com/fatechub/fatecrl-curso-si/blob/gh-pages/disciplinas/ciclo6_ITE-005_topicos-especiais-em-sistemas-para-internet-III_garcia/TP2Adam.hs) nota: 100.00

### Contéudo da Disciplina

#### Definições

Haskell é uma linguagem de **tipagem superforte**.

Haskell é uma linguagem preguiçosa, evita erros de compilação. Exemplo: Se houver pedir mais quantidade do que um vetor tiver ele apresentará até onde houver. Exemplo2: Só irá dazer o loop até onde estiver definido.

**Haskell possui linguagem pura**, totalmente funcional: o que significa que não tem acesso ao "mundo exterior" (banco de dados, arquivo html... nem um simples txt).
No Haskell, até o print é impuro. Então, ele se enquadrará em Monads.

**Código impuro** é todo código que consegue ter acesso a códigos externos ou funções que podem alterar o resultado/comportamento de outra função.

> **MONADS**
Monads are frequently encountered in Haskell: the IO system is constructed using a monad, a special syntax for monads has been provided (do expressions), and the standard libraries contain an entire module dedicated to monads. 

>The Prelude contains a number of classes defining monads are they are used in Haskell. These classes are based on the monad construct in category theory; whilst the category theoretic terminology provides the names for the monadic classes and operations, it is not necessary to delve into abstract mathematics to get an intuitive understanding of how to use the monadic classes. 

>A monad is constructed on top of a polymorphic type such as IO. The monad itself is defined by instance declarations associating the type with the some or all of the monadic classes, Functor, Monad, and MonadPlus. None of the monadic classes are derivable. In addition to IO, two other types in the Prelude are members of the monadic classes: lists ([]) and Maybe.


**Exemplo: código impuro**

{% highlight java %}
class Foo{
  private int a;               
  public int bar(){            
    a++;                        // Função impura: alterou o resultado de uma
    return 0;                   // outra função. Isso não existe em haskell!
  }
  public int baz(int x){        // Nunca irá retornar o mesmo resultado pois
    return x+a;                 // a outra função altera seu resultado
  }
}

class Teste{
  p.s.v.m(...){
    Foo t = new Foo();
    syso(t.baz(3));     // 3
    syso(t.baz());      // 0
    syso(t.baz(3));     // 4
  }
}
{% endhighlight %}

Função `bar` e `baz` sao impuras, na visão do Haskell só é legal quando não tem atributos.

***

**No terminal:**

{% highlight haskell %}
ghci

Prelude> let u = [1,9,9,3,8,2,-7]
Prelude> u 
// [1,9,9,3,8,2,-7]
Prelude> u !!4 
// 8
Prelude> 123:u // (:) => CONS (Tbm funciona com letras)
// [123, 1,9,9,3,8,2,-7]

Prelude> let h = "FATEC"
Prelude> h
// "FATEC"
Prelude> '1':h
// "1FATEC"
Prelude> '2':h
// "2FATEC"

Prelude> let a = "CPS"
Prelude> let b = '1':a
Prelude> b
// "1CPS"
Prelude> '2':b
// "21CPS"

// pra limpar
:q
clear

Prelude> let h = "FATEC"
Prelude> "OI " ++ h
// "OI FATEC"
Prelude> h ++ "OI "
"FATECOI "
Prelude> "OLA PESSOAL DA " ++ b ++ " TUDO BLZ?"
// "OLA PESSOAL DA FATE TUDO BLZ?"

Prelude> let w1 = [1,2,3]
Prelude> let w2 = [4,5,6]
Prelude> w1 ++ w2
// [1,2,3,4,5,6]
Prelude> w2 ++ w1
// [4,5,6,1,2,3]

Prelude> let y = "FATEC SANTOS"
Prelude> y
// "FATEC SANTOS"
Prelude> take 4 y
// "FATE" pega os 4
Prelude> drop 4 y
// "C SANTOS" solta os 4

Prelude> let y = "FATEC SANTOS"
Prelude> drop 4 y
// "C SANTOS"
Prelude> take 3 y
// "FAT"
Prelude> take 3 (drop 4 y) - ou - Prelude> take 3 $ drop 4 y
// "C S"

Prelude> cycle [1,2,3] // loop infinito
// [1,2,3,1,2,3,1,2,3,1,2,3,...]
Prelude> take 145 ( cycle [1,2,3,4] )
// [1,2,3,4....3]

Prelude> [1..5] // FUNCIONA COM 'string' tbm
// [1,2,3,4,5]

Prelude> reverse [1..5] 
// [5,4,3,2,1] 

Prelude> [2*x | x <- [0..50]] // pega pares de 0 a 50  ... "|" é TAL QUE
// [2,4,6...50] 

Prelude> [2*x | x <- [0..50], x > 12] // pega pares de 0 a 50 e que seja maior que 12
// [14,16,18...50] 

Prelude> [2*x | x <- [0..50], x > 12, mod x 5 == 0] // pega pares de 0 a 50 e que seja maior que 12
// [...] 
{% endhighlight %}

{% highlight haskell %}
EXERCICIO O RESULTADO TEM QUE SER [9, 11, 13,15,17,19,21,23,25,27,29,31]
SOLUCAO 1: [2*x+1 | x <- [4..15]] 
SOLUCAO 2: [2*x+1 | x <- [0..50],x > 3, x < 16]
SOLUCAO 3: [x | x <- [9..31], mod x 2 == 1]
{% endhighlight %}

### em http://www.tutorialspoint.com/compile_haskell_online.php
 
{% highlight haskell %}
// PASSO 1
// create file `Aula1.hs` e deleta `main.hs`
Aula1.hs

// PASSO 2
// file Aula.hs e compila
module Aula1 where

dobro x = 2*x

somaquadrado a b = a*a + b*b

meio n1 n2 y = take n1 ( drop n2 y )

// PASSO 2
// no terminal `ghci` e `:l Aula1.hj`

// TESTE DE MESA DA FUNCAO somaQuadrado
somaQuadrado (dobro 1) (dobro 2) = 
somaQuadrado 2 4 = 
somaQuadrado 2 * 2 + 4 * 4 = 
somaQuadrado 4 = 16 = 20

// TESTE DE MESA DA FUNCAO meio
meio n1 n2 y = take n1 ( drop n2 y ) 
meio 3 4 "FATEC SANTOS" = take n1 ( drop n2 y )
take 3 ( drop 4 "FATEC SANTOS" )
take 3 ( "C SANTOS" )
"C S"
{% endhighlight %}


======================================

<span class="label label-success text-uppercase">Aula 2 - 17/08</span>

**no prompt**

{% highlight haskell %}
--lista de 0 a 100 os pares
[2*x | x<-[o..100]]

-- De zero a 10 sem o 5
[x | x<-[o..10],x/=5]

{% endhighlight %}


**Usando o If**

O if neste caso é uma função, não um desvio. Será a última vez que o if será usado.

{% highlight haskell %}
--Se for PAR mostra BANG, se for ÍMPAR imprimi BONG
[if mod x == 0 then "bang" else "bong" | x<-[o..10]]
{% endhighlight %}


#### Concatenação em vetor usando uma String que varia

{% highlight haskell %}
-- concatenado cada letra da palavra "FATEC" com um "A"
-- como tem caracter precisa usar o colchete
[[x] ++ "A" | x<-"FATEC"]
--saida: ["FA","AA","TA","EA","CA"]

-- Alternativa: pode ser com o operador cons (:)
-- como tem o : não precisa de colchete, vai direto
[x:a"A" | x<-"FATEC"]
{% endhighlight %}


**Exercício**

Ex. Faça uma *list compreenshion* que elimine as vogais de uma string:
*Resposta*:

{% highlight haskell %}
[x | x<-"FACULDADE DE TECNOLOGIA",x/='A',x/='E',x/='I',x/='o',x/='u']
-- Alternativa: Com *notElem*. Ele faz tudo automaticamente
[x | x<-"FACULDADE DE TECNOLOGIA",notElem x "AEIOU"]
{% endhighlight %}


#### Tipagem

*No código:* 
No haskell, é preciso dar o tipo de todos os parêmetros de entrada e um tipo (apenas) para a saída. 

{% highlight haskell %}
-- Esta função:
dobro x = 2*x

-- Será tipada assim:
-- O primeiro Double é pro parametro x, o segundo Double é pro 2*x (saída)

dobro :: Double -> Double
dobro x = 2*x


-- Função com três parâmetros
Mult x y z = x * y * z

-- Os três primeiros são para x,y,z. O ultimo double pro retorno
Mult :: Double -> Double -> Double -> Double
Mult x y z = x * y * z
{% endhighlight %}

É possível uma função de um tipo retornar outro. 
Quando tem mais de um parametro, por padrão, adiciona-se um s depois de x (nome do parametro, no caso).


**Função boomBang:**

{% highlight haskell %}
-- Tipando a função Boombang
boomBang :: [Int] -> [String] 
boomBang xs = [if mod x 2 == 0 then "BANG" else "BOOM" | x<-xs]
{% endhighlight %}


##### Cola

É possível ver uma "colinha" da tipagem de algo. Basta adicionar ```:t nomeDaFuncao```. Porém ele apresentará o tipo mais genérico possível.


**Função apenas com retorno**

Isso é uma função (que não recebe nada e retorna um inteiro). ISSO NÃO É UMA variável. Aqui não existe void, ainda que o retorno seja vazio.

{% highlight haskell %}
-- Funcao que nao recebe nada e retorna um 9 -Int- (Não é uma atribuição nem variável)
u :: Int
u = 9
{% endhighlight %}


#### Tupla

É uma estrutura coordenada, que não é uma lista. As tuplas são o único jeito de carregar coisas de tipagem diferentes (vetor não tem tipagem dinâmica). Porém, a tupla não é uma lista, ela é só uma jeito de carregar coisas de tipos diferentes. Os parametros devem ser enviados na ordem CERTA.

{% highlight haskell %}
-- tupla de Int e Int
soma2 :: Int -> (Int, Int)
soma2 x = (x-1, x+8)

-- tupla de Int e String (a ordem dos parametros precisam ser a mesma)
nomeIdade :: Int -> String -> (Int, String) 
nomeIdade x y = (x+1, "OLA "++y)
-- nomeIdade 3 "Ramon"
-- (4, "OLA RAMON")

-- EX2 - Faça uma função foo que recebe x, y e z como parâmetros e retorne
-- (x*y, z:[z]++"A", y-x+5.9)
-- foo :: Double -> Double -> Char -> (Double, [Char], Double)
foo :: Double -> Double -> Char -> (Double, String], Double)
foo x y z = ( x * y, z:[z]++"A", y-x+5.9 )
-- OBS: dê o tipo
{% endhighlight %}


#### ALGEBRAIC DATA TYPES

- **data** cria um novo tipo (enumeração = ENUM no java)
- **deriving Show** é para mostrar na tela
- ***"lado direito"*** (Segunda...) = values construct
- **deriving** é como se um extends

{% highlight haskell %}
data Dia = Segunda | Terça | Quarta | Quinta | Sexta | Sábado | Domingo deriving Show
-- :t Segunda
-- Segunda :: Dia
-- Segunda (erro se nao tiver `deriving Show`)
{% endhighlight %}


##### PATTERN MATCHING

Funciona como um if. Sempre que se pensar em if, usa-lo.
Aqui, cada linha com uma expressão corresponde a um *if*. Para representar o *else*, usa-se o **_** (underline). O underline representa cada parametro, caso haja mais de um, deve haver mais underlines.

{% highlight haskell %}
-- Agendar as datas como um if no java. Apenas se joga umvalor. Não podem ser defindas funções. 

agenda :: Dia -> String
agenda Domingo = "Faustão"
agenda Sabado = "Futebol"
agenda Sexta = "Cerveja"
agenda _ = "Trabalho"       -- ignora, else

-- entrada:> agenda "Sexta"
-- saida:> "Cerveja"


-- Em uma empresa um funcionario ganha por dia um salario fixo
-- porem aos domingos, ele ganha 50% a mais
-- aos sabados, 30% e nos demais dias, nenhum acrescido
-- fala uma funcao que represente esta situacao
salExtra :: Dia -> Double
salExtra Domingo = 1.5
salExtra Sabado = 1.3
salExtra _ = 0

calSal :: Double -> Dia -> Double
calSal x d = x + (x * salExtra)

--modo 2
salFla :: Dia -> Double -> Double
salFla Domingo x = x + (x * 0.5)
salFla Sabado x = x + (x * 0.3)
salFla _ x = x


-- como são passados dois parametros (dia,cargo) pra função fator, no else 
-- deve conter um underline para cada um.
fator :: Dia -> Cargo -> Double
fator Domingo Chefe = 2.0
fator Domingo Peao = 1.5
fator Sexta Chefe = 1.1
fator _ _ = 1.0
{% endhighlight %}


***Gists:***
- [Anotações da Flávia](https://gist.github.com/flaviacs/0173a73ee72be4ac98b7)
- [Anotações do Adam](https://gist.github.com/anonymous/7957349af8185f3a53df)

======================================

<span class="label label-success text-uppercase">Aula 3 - 24/08</span>

{% highlight haskell %}
module AULA3 where
--module Aula33 where

-- currying
-- pattern match

-- O tipo Pessoa possui dois value construtores 
-- Fisica e Juridica
{-
O value constructor Fisica possui dois campos de String e de tipo Int. O Value conctruutor Juridica possui um campo
String
-}
-- O Show da "poderes" de ser mostrado na tela via ghci
-- O value construtor Pessoa eh uma funcao que Recebe dois parametros, um string e um Int

data Pessoa = Fisica String Int | Juridica String deriving Show

-- Fisica "JOAO" 30
-- :t (Fisica "JOAO" 30)
-- :t (Juridica "FATEC" 30)
-- :t Fisica -- Fisica :: String -> Int -> Pessoa -- esse paramentro tem que ter String Int e devolver uma pessoa

rel :: Pessoa -> (String, String)
rel (Fisica x y) = ("Nome :" ++ x, "Idade: " ++ show y) -- o show equivalente toString
rel (Juridica x) = ("Nome :" ++ x, "PJ NAO POSSUI IDade")
-- RESTE: rel (Fisica "RAMON" 25) 

-- EX1
-- Faça uma funcao aniversario, que recebe uma Pessoa e retorna uma mensagem de aniversário com a idade atualizada a mais em um ano a mais.
-- ex: aniversario (Fisica "Ramon" 22) = "Parabens pelo seus 22 anos Ramon"
-- ex: aniversario (Juridica "Fatec" 22) = "Erro"
aniversario :: Pessoa -> String
aniversario (Fisica x y) = "Parabens pelo seus " ++ show (y+1) ++ " anos " ++ x
aniversario (Juridica x) = "ERRO"

module Aula33 where

{-

** Topicos ** 

- parseion function - Não user
- currying
- pattern match
- Record syntax

O tipo Pessoa possui dois value construtores `Fisica` e `Juridica`.

O value constructor Fisica possui dois campos de String e de tipo Int. O Value conctruutor Juridica possui um campo
String

O Show da "poderes" de ser mostrado na tela via ghci

O value construtor Pessoa eh uma funcao que Recebe dois parametros, um string e um Int

-}

data Pessoa = Fisica String Int | Juridica String deriving Show

-- Fisica "JOAO" 30
-- :t (Fisica "JOAO" 30)
-- :t (Juridica "FATEC" 30)
-- :t Fisica -- Fisica :: String -> Int -> Pessoa -- esse paramentro tem que ter String Int e devolver uma pessoa

rel :: Pessoa -> (String, String)
rel (Fisica x y) = ("Nome :" ++ x, "Idade: " ++ show y) -- o show equivalente toString
rel (Juridica x) = ("Nome :" ++ x, "PJ não possui idade")
-- TESTE: rel (Fisica "RAMON" 25) 

{-
    EX1
    Faça uma funcao aniversario, que recebe uma Pessoa e retorna uma mensagem de aniversário com a idade atualizada a mais em um ano a mais.
    TESTE: aniversario (Fisica "Ramon" 22) = "Parabens pelo seus 22 anos Ramon"
    TESTE: aniversario (Juridica "Fatec" 22) = "Erro"
-}
aniversario :: Pessoa -> String
aniversario (Fisica x y) = "Parabens pelo seus " ++ show (y+1) ++ " anos " ++ x
aniversario _ = "ERRO" -- ou aniversario (Juridica x) = "ERRO"



---------------------------------

{- 
É possível ter um value constructor com o mesmo nome de um data constructor 

Linha abaixo equivale = data Ponto = Ponto Double Double deriving Show
Esta usando: Record syntax
-}
data Ponto = Ponto {xval, yval :: Double} deriving Show 
-- com mais de um campo: {xval, yval :: Double, aval :: String}

-- Ponto 1.0 1.2
-- :t (Ponto 1.0 1.2)
-- :t (Ponto 5.0)
-- :t Ponto

-- let p = Ponto 2.4 5.5
-- p
-- xval p
-- yval p
-- :t xval -- ate o nome do campo tem tipo

-------

--distOrig
norma :: Ponto -> Double
norma (Ponto x y) = sqrt(x**2 + y**2)
-- norma (Ponto 2.0 1.0)
-- ^ int 2^2 ... ** double 2**2

-- normalinha
norma' :: Ponto -> Double
norma' (Ponto {xval=x, yval=y}) = sqrt(x**2 + y**2)

-- normalinhalinha
norma'' :: Ponto -> Double
norma'' p = sqrt(xval p**2 + yval p**2) -- nao ta usando pattern match pq o PM da uma forma ja pronta, exemplo (Ponto x y) ou (Ponto {xval=x, yval=y})

-- EX2
-- Faça uma função de translação que recebe um ponto, e dois doubles. Este ponto  deve ser empurrado na diração dos parametros double. A funcao retorna um ponto
-- translacao (Ponto 2 1) 1 1 = Ponto 3 2

translacao :: Ponto -> Double -> Double -> Ponto
translacao (Ponto x y) a b = Ponto (x+a) (y+b)


-- Metro, Litro, Kilograma são tipos de ENUMERACOES
data UnidadeSI = Metro | Litro | Kilograma deriving Show
data UnidadeImp = Jarda | Galao | Libra deriving Show
data Medida = MedidaMetrico Double UnidadeSI | 
              MedidaImperial Double UnidadeImp
              deriving Show

           -- MedidaMetrico 2 Metro
           -- t: (MedidaMetrico 2 Metro)
           -- MedidaImperial 2 Jarda

converter :: Medida -> Medida
converter (MedidaMetrico x Metro) = MedidaImperial (1.0936*x) Jarda
converter (MedidaMetrico x Litro) = MedidaImperial (0.264172052*x) Galao
converter (MedidaMetrico x Kilograma) = MedidaImperial (2.20462262*x) Libra

converter (MedidaImperial x Jarda) = MedidaMetrico (0.9144*x) Metro
converter (MedidaImperial x Galao) = MedidaMetrico (3.78541178*x) Litro
converter (MedidaImperial x Libra) = MedidaMetrico (0.45359237*x) Kilograma

-- TESTE converter (MedidaMetrico 2 Metro)
-- No Google 1m to yd

---------------------------------


soma :: Int -> Int -> Int -- soma :: Int -> (Int -> Int) agrupa parametro = funcao
soma x y = x + y

{-
:t (soma 4) -- currying

let u = soma 4
:t u
u 10
u 1

soma 4 = 4+y -- uma funcao
soma Int -> (Int -> Int)

let u = soma 4
let soma4 = soma 4
soma4 5 -- 9

-- CURRYING é uma tecnica que consiste em passar um número menor de parametros para a funcao, fazendo com que ela te retorna uma outra funcao com um valor fixo

-}

```javascript
function soma(x){
    return function(y){
        return x+y;
    }
}

var x = soma(4);
```
------------

--Qualquer funcao que possua dois parametros pode ser escrita em notacao infixa
(^-^) :: Int -> Int -> Int
(^-^) x y = x+y+7
-- teste 4 ^-^ 3 -- 14
-- teste (^-^) 4 3 -- 14

-- transformando mod igual do JAVA
(%) = mod
-- teste 4 % 3 -- 1

(!!!!) = (+)
-- teste 4 !!!! 1 -- 5

-- Currying com carinha feliz
let k = (4 ^-^)
k 10 -- 21

let y = (3 +)
y 2 -- 5


---------------------------------------

--Foo tipo de data
--Bar e Baz constructs
--String Int Campos
--data Foo = Bar String Int | Baz Int Int
data Foo = String :?: Int | Int :!: Int deriving Show
-- teste :t ("Raira":?:70)
-- teste :t (9:?:18)
-- teste :t (:?:)
-- teste :t (:!:)

foo :: Foo -> Foo
foo (x :?: y) = y :!: y
foo (x :!: y) = "" :?: (x+y)
-- foo ("Raira" :?: 70)
-- foo (90 :?: 90)


--[1,2,3,4] -- uma lista
--1:2:3:4:[] -- pro haskell enxerga assim

----------------------

fn :: [Int] -> Int 
fn (x:xs) = x -- LISTA NAO VAZIA
fn [] = 0 -- LISTA VAZIA
-- fn [3,2,1] -- 3
-- fn (3:2:1:[]) -- 3
{-
x:xs
1:2:3
x=1
xs=2:3
-}


-----------------------

-- LAMBDA *funcao anonima* EM haskell

let l = \x -> x+1
l 2 -- 3
:t l

-- LAMBBA FOD RECURSAO MAPPINg
{% endhighlight %}


======================================

<span class="label label-success text-uppercase">Aula 4 - 31/08</span>

{% highlight haskell %}
 module Aula4 where

{- Notação infixa no meio -} 

--(^-^) :: Int -> Int -> Int
--(^-^) x y = x+y+2

--(%) = mod
--(!!!) = (+)

{- Currying : Técnica da prog. funcional no qual, a função pode receber parametros a menos que o
declaro. usar let para atribuir a uma nova função
Gera nova função com os parametros que falta -}

--{ let somaDoisTres = somarTresNum 2 3 - esta linha fixa x e y, e deixa z livre. O retorno é uma funcao
--Int -> Int

--somaTresNum :: Int -> Int -> Int -> Int
--somaTresNum x y z = x + y + z

----------------------------------------------------------------

# TOPICOS
- high order functions

-- LAMBDA
-- do lado esquerdo `\x y = parametros`
-- do lado direito `espressão`

-- com nome
let u = \x y -> x+y
u 3 4 -- 7

```javascript
var u = function(x, y){ return x+y; }
u(3,4)
```

-- sem nome (anonima)
(\x y -> x+y) 3 4 -- 7

```javascript
function(x, y){ return x+y; }(3,4)
```
--

let w = \f x -> f(x+1)
w (\x->3*x) 4 -- 15
-- TESTE DE MESA
-- w (\x->3*x) 4 = 
-- w (\x->3*x) (4+1) =
-- (\x->3*x) 5 =
-- 3*5 = 15

triplo :: Int -> Int
triplo = x*3

--            |--------------|¹
--            |¹     |²-------------|²
aplicFoo :: (Int -> Int) -> Int -> Int
aplicFoo f x = f(x+1) 

-- Com LAMBDA
aplicFoo' :: (Int -> Int) -> Int -> Int
aplicFoo' \f x = f(x+1)
-- aplicFoo' triplo 4

-- 

-- let c = (\x y -> x+y) 3
-- c 5 -- 8

-- Mapper é um metodo que aplica uma função em todos os parametros
-- map triplo [1,2,3] --[3,6,9]
-- map (\x->1+x) [1,2,3,4] --[2,3,4,5]
-- map (+1) [1,2,3,4] --[2,3,4,5]
-- map (3*) [1,2,3,4] --[3,5,9,12]
-- filter (\x -> notEleme x "AEIOU") "FATEC" --"FTC" filter é o map disfarçado
-- filter (\x -> mod x 2 == 0) [1,2,3,4] --[2,4]
-- filter (\x -> mod x 2 == 1) [1,2,3,4] --[1,3]

-- :t map
-- map :: (a -> b) -> [a] -> [b]
-- uma função que recebe algo do tipo `a` e retorna algo do tipo `b`
-- [a]: lista de elemento do tipo a, mesma coisa para [b]

-- :t filter
-- filter :: (a -> Bool) -> [a] -> [a]
-- Só é do tipo `a` e se for verdadeiro mostra `a` se não, não!

-- Expressão que elimine os negativos de -5 a 5
-- filter (\x -> x > 0) [-5..5]
-- filter (>0) [-5..5]

-- Expressão ou Função que tranforme a String AABCAACB em [1,1,2,3,1,1,3,2]


{-
letra :: Char -> Int
letra 'A' = 1
letra 'B' = 2
letra 'C' = 3
map letra "AABCAACB"
-}

-- TIP
-- expressão GHCI
-- função no arquivo

`foldl (+) 0 [1,2,3,4]` --10
-- foldl pega uma funcao acumuladora, essa funcao deve conter dois parametros sempre, um valor inicial e uma lista a ser percorrida ao contrario
-- TESTE DE MESA
-- (+) 0 1 [2,3,4]
-- (+) 1 2 [3,4]
-- (+) 3 3 [4]
-- (+) 6 4 []
-- (+) 10 []
--
-- exemplo'
-- foldl (*) [1..6] --720 fatorial
--
-- exemplo''
-- foldl (\xs x -> x:xs) [] "FATEC" --"CETAF"
-- TESTE DE MESA
foldl (\xs x -> x:xs) [] "FATEC"
      -------|------- 
             f

-- TIP
-- 'A':'F':[] = "AF"

-- exemplo'''
-- Expressão que conta os elementos de um vetor de inteiros
-- 
-- foldl (\xs x -> xs+1) 0 [1,2,3,4,5,6]
-- foldl (\xs _ -> xs+1) 0 [1,2,3,4,5,6]
-- length [1..10]
--
-- foldl (\c _ -> c+1) 0 [1..33]
-- `c` é o 0
-- `_` é cada valor da lista          



--------------------------------


-- COMPOSIÇÃO

:t (.)
(.) :: (b -> c) -. (a -> b) -> (a -> c)
       ---f----    ----g---

       f: b -> c
       g: a -> b
       f.g a -> c
       (.) `a` entrada da função `f.g` é a entrada de `g` e `a` saída de `f`

-- exemplo
let u = \x -> x+1
let v = \x -> x^2 -- eleva ao quadrado
(u.v) 2 -- u.2^2 -- 4+1 -- 5 
u(v(2))
u.v $ 2
u $ v(2)
u $ v $ 2
(u.v.u) 2 -- 10

{% endhighlight %}

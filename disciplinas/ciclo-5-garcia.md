---
layout: page
title: Ciclo 5 - Garcia - Padrões de Projetos
header: Pages
group: navigation
---
{% include JB/setup %}

<span class="label label-warning text-uppercase"><span class="glyphicon glyphicon glyphicon-star"></span> Fixo</span>

- [Repositório com exemplos de utilização de padrões de projeto implementados em Java.](https://github.com/MarcosX/Padr-es-de-Projeto)
- [L1.pdf - Exercicio de Treino dado pelo Garcia Reflection]({{ site.production_url }}/media/L1.pdf) 
- [6PPL2.pdf - Exercicio 2 de Treino dado pelo Garcia Reflection]({{ site.production_url }}/media/6PPL2.pdf) 
- [E-Book Use a Cabeça - Padrões de Projetos.pdf](https://fatecspgov-my.sharepoint.com/personal/adam_macias_fatec_sp_gov_br/_layouts/15/guestaccess.aspx?guestaccesstoken=93JZ95qrU%2fs1UEgPDbqrXwiHP4KExXEq0WrGnMt6JSM%3d&docid=178cbdec3adc944e19eedfbd76af46bda)

***

<span class="label label-primary text-uppercase"><span class="glyphicon glyphicon glyphicon-star"></span> Aula 13/02</span>

## Ementa Tópicos especiais em Sistemas para Internet

1. [Polimorfismo](http://pt.wikipedia.org/wiki/Polimorfismo)  para métodos (GENERICS) / Collections
2. [Reflection](http://bit.ly/1F1nRlZ)
3. [Design Patterns](http://pt.wikipedia.org/wiki/Padr%C3%A3o_de_projeto_de_software)
  - [Strategy](http://pt.wikipedia.org/wiki/Strategy)
  - [Abstract Factory](http://pt.wikipedia.org/wiki/Abstract_Factory)
  - [Decorator](http://pt.wikipedia.org/wiki/Decorator)
  - [Singleton](http://pt.wikipedia.org/wiki/Singleton)
  - [Observer](http://pt.wikipedia.org/wiki/Observer)
  - [Visitor](http://pt.wikipedia.org/wiki/Visitor_Pattern)
  - [Proxy](http://bit.ly/1F1nQOE)
4. [Orientação a aspectos](http://pt.wikipedia.org/wiki/Programa%C3%A7%C3%A3o_orientada_a_aspecto)
5. Topicos especiais

***
 
## Referências bibliográficas

1. java reflection in action. Ira Foreman e Nate Foreman - 2004.
2. Design Patterns: Elements of Rensable (?) object-oriented software. Eric Gamma, Rich Helm, Ralph Jhonson e John vissides (?). (Gang of Four ou GOF).
3. Use a cabeça: Design patterns. Eric Freeman e Elisabeth Freeman.

***

## Polimorfismo de Subtipos

É a maneira de referenciar um objeto de várias formas.

<pre>
Gato g = new Gato()              |       a.arranhar()   [X]
Animal a  = new Gato()           |       g.arranhar()   [✓]

                        _________________________ 
                       |         ANIMAL          | 
                       |                         | 
                       | + void emitirSom()      | 
                       | + void dormir()         |
                       |_________________________|
                            ^                 ^
                            |                 |
       _________________________           _________________________
      |          GATO           |         |        CACHORRO         |
      |                         |         |                         |
      | + void emitirSom()      |         | + void emitirSom()      |
      | + void arranhar()       |         | + void cavar()          |
      |_________________________|         |_________________________|

</pre>

**Memória: Alocação** 

<pre>
                #1b7C                                #2K7D
                 __________                           __________
                |          |                         |          |
                |__________|                         |__________|
                    |                                     |
                g._/                                   a./
</pre>

- [Teoria dos tipos](http://pt.wikipedia.org/wiki/Teoria_dos_tipos)
- [Alocação de memória](http://pt.wikipedia.org/wiki/Aloca%C3%A7%C3%A3o_de_mem%C3%B3ria)

***
 
## Principio de POO
Programe para uma abstração, nunca para uma implementação.

***

## Polimorfismo Para Método (GENERICS)
Criar um tipo novo que englobe o outro. O foco é na estrutura do novo tipo e não no tipo englobado.

**Ex.:** Movimentar a mochila na cadeira, você pode fazer isso independente do que houver na mochila.

O ARRAY LIST É UM EXEMPLO. Ele lista qualquer coisa que for definido.
 
- ArrayList `<string>`
- ArrayList `<ninja>`

*** 

## Download arquivos aula
[aula-2015-02-13.rar]({{ site.production_url }}/media/aula-2015-02-13.rar) 

***

<span class="label label-primary text-uppercase"><span class="glyphicon glyphicon glyphicon-star"></span> Aula 20/02</span>

<div class="alert alert-info">Este inicio é uma atualizada sobre o que o ciro deu semestre passado. Isso ficou faltando (apenas pra ficar por dentro)</div>

## Bound
Usado para fazer restição. 

#### Upper boud
Ele não passa 'Joia', caso haja uma classe acima ele nao pega.

Se for usado uma string dará erro. Só serão aceitos os "filhos" (subclasse  Joia).

{% highlight java %}
public class Caixa < T extends Joia > {
  ...
}
{% endhighlight %}

#### Lower bound

<pre>
      |---------------|               |-------------------------|
      |     list      |               |          Number         |
      |---------------|               |-------------------------|
            ^                               ^             ^
            |                               |             |
      |---------------|             |-------------|    |-------------|
      |   ArrayList   |             |   integer   |    |   integer   |
      |---------------|             |-------------|    |-------------|
</pre>

<pre>
List< ? super Number > a = New arrayList< objeto >;
          |
          |-------> Só pode chegar até *NUMBER*
                    Não poderá chegar na classe *String* nem *Integer* porque é acima. 
</pre>

***

## Regra PECS

- *Super*: Só add();
- *Extends*: só faz get();

**Exemplo com arrayList:**

{% highlight java %}
public Class PortaJoia_ {
  ...
}
{% endhighlight %}
 
*** 

<div class="alert alert-info">Matéria do semestre</div>

## Reflection: 
Visto em php

{% highlight php %}
<?php
  class Cachorro{}
  $c = "cachorro";
  $d = new $c();
?>
{% endhighlight %}

- Conhecido como *blackmagic*
- É nada mais do que a habilidade de enxergar um *.class*' (no java).
- É um pacote que te d´´a premissão de ver informações no seu *.class*.:

- MetaDado
- MetaObjeto (meta classe) { representam informações da classe }
- Classes
- Type          
- Method        
- Field         
- Annotations   { Marcador para conversas com o compilador}
- Modifier      { abstrct, pretect, public, defout }
 
***

## Boilerplate
Repetição trecho de código em várias partes do arquivo mudando apenas pequenas coisas, como por exemplo um syso:

{% highlight java %}
public String toString(){
  syso "ClasseNome";
}
{% endhighlight %}

**Resolvemos assim:**

{% highlight java %}
public String toString(){
  Class < ? > c = this.Class(); // Pega todas as infos do .class
  return c.getSimpleName(); // Ele apresentará a classe pelo seu nome. Não apresentará o endereço de memória ao lado.
}
{% endhighlight %}

*** 

## Download arquivos aula
[aula-2015-02-20.rar]({{ site.production_url }}/media/aula-2015-02-20.rar) 

***

<span class="label label-primary text-uppercase"><span class="glyphicon glyphicon glyphicon-star"></span> Aula 06/03</span>

## Persistência com reflection
[Reflection.zip]({{ site.production_url }}/media/Reflection.zip)

> Códigos feito por Garcia e Adam (@annotations && Reflect)

## Download arquivos aula
[aula-2015-03-06-garcia.rar]({{ site.production_url }}/media/aula-2015-03-06-garcia.rar) 

***

<span class="label label-primary text-uppercase"><span class="glyphicon glyphicon glyphicon-star"></span> Aula 13/03</span>


## Padrão de Projeto: **DECORATOR**

<div class="alert alert-danger">Ele deu o exercicio dos prefeitos e cargos, e pediu um UML. (Precisa passar para cá a resoluções Adam e Flávia) e o enunciado.</div>

**Resposta Garcia com Decorator**
[garcia-13-03-PadraoDecorator.rar]({{ site.production_url }}/media/garcia-13-03-PadraoDecorator.rar) 


***

<span class="label label-primary text-uppercase"><span class="glyphicon glyphicon glyphicon-star"></span> Aula 20/03</span>

<div class="alert alert-danger">Pegar foto da exemplificação da esplicação com o Felipe (uml do padrão)</div>

## Padrão de Projeto: **STRATEGY**
Define uma família de algoritmos, encapsula e os torna intercambiaveis (variáveis).
***Principio***:Encapsule o que varia.

### Exercício 1:

Uma loja virtual prossue alguns produtos a venda. Os produtos são livors, DVDs e brinquedos. Cada produto possui nome e preço. A mesma loja oferece promoções diferentes a cada mês. Uma promoção reguçar desconta cada produto em 10% mais um desconto extra varia de 5% a 10% dependendo do mês. Uma liquidação desnconta 30% ao preço de cada produto. Há meses quenão há promoção descrita.
Esta situação: 
- A) Desenhe o diagrama de classes;
- B) Codifique com base em A).



### Arquivo  resolvido da forma errada pelo Garcia
    Fere aregra de aberto e fechado:
    - dificil de debugar
    - cresce esponencialmente

*** 

## Download arquivos aula

[aula-2015-03-20-garcia.zip]({{ site.production_url }}/media/aula-2015-03-20-garcia.zip) 
---
title: "Closures: block, proc e lambda - Ruby"
datePublished: Tue May 09 2023 14:44:37 GMT+0000 (Coordinated Universal Time)
cuid: clhgdut57000208l8glabeh4e
slug: closures-block-proc-e-lambda-ruby
canonical: https://dev.to/dnovais/closures-block-proc-e-lambda-ruby-18f7
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/VlZYu3nZIRI/upload/228f489399c93ecb7aba69a03f22e100.jpeg
tags: lambda, closure, ruby, developer, proc

---

Blocks, Procs e Lambdas são referenciados de maneira geral como “closure” e que por sua vez são uns dos aspectos mais poderosos do Ruby e também um dos mais complexos.

Para entedermos melhor que são closures precisamos compreender alguns conceitos:

### Escopo léxico

O escopo léxico serve para identificar qual o valor de uma variável em determinado lugar do código, daí o conceito chamado **Closest Variable Wins** (A variável mais próxima vence), ou seja, a atribuição de valor mais próxima dessa variável, será quem define o valor da mesma.

Ou seja, definindo as variáveis com o mesmo valor, mais próxima do comando `puts "#{prefix} #{name}"`, estas variáveis dentro do escopo terá o valor "Sra" e "Loren" e não mais "Sr" e "Diego" como foram definidas anteriormente. Essa é uma regra do escopo léxico, a variável mais próxima, vence.

```ruby
prefix = 'Sr'
name = 'Diego'

4.times do
	prefix = 'Sra'
	name = 'Loren'
	msg = 'Olá!'

	puts "#{msg} #{prefix} #{name}"
end

=> Sra Loren
=> Sra Loren
=> Sra Loren
=> Sra Loren
```

### Variável livre

Variável livre é uma variável definida em um escopo acima do escopo atual, ou seja no escopo pai. A variável livre no exemplo acima, seriam então as variáveis `prefix` e `name` definidas nas primeiras linhas. Ja a variável `msg` utilizada está dentro do mesmo escopo de execução, portanto não é uma variável livre.

## Closures

"Uma função que pode ser guardada como variável", talvez essa seja a definição mais famosa de Closure. Segundo Wei Hao em seu livro Mastering Ruby Closures, os conceitos acima comentados (escopo léxico e variável livre) são alguns dos principais conceitos para se entender Closures, como o mesmo explica, "Closure é uma função que o seu corpo referencia uma variável declarada no escopo pai". Segundo o Ruby Guides as Closures "capturam o escopo de execução atual" e "carregam variáveis e métodos vindos do contexto atual em que foram definidas", mas "não carregam valores e sim referências, portanto se as variáveis forem alteradas após criadas, as Procs sempre terão a última versão dessa variável".

Closure é uma funcionalidade que permite escrever um pedaço de código que:

* Pode ser atribuído e ou passado como parâmetro.
    
* Uma função que pode ser guardada como variável
    
* Pode ser executado em qualquer lugar.
    
* E referenciam variáveis no contexto onde são criados.
    

## Block

Ruby blocks como o Ruby Guides define, "são pequenas funções anônimas que podem ser passadas nos métodos". Podemos identificar Ruby Blocks quando vemos ou escrevemos no código comandos dentro dos `do / end` ou entre chaves `{block}` e os argumentos vão dentro de pipes `|args|`. Métodos famosos como o `.each`, `.times` e outros são bons exemplos de Blocks.

```ruby
method { |i| ... }

method do |i|
  ...
end
```

Ex. usando o `each`:

```ruby
[1,2,4,5].each do |number|
  puts number
end
```

Ex. usando o `times`:

```ruby
prefix = 'Sr'
name = 'Diego'

4.times do
	puts "#{prefix} #{name}"
end

=> Sr Diego
=> Sr Diego
=> Sr Diego
=> Sr Diego
```

### Como criar um block?

Imagine o seguinte cenário, onde devemos criar um método para ira concatenar por meio de interpolação o seu primeiro nome e seu ultimo nome

```ruby
def full_name
	first_name = 'Diego'
	last_name = 'Novais'
	
	"#{first_name} #{last_name}"
end

puts full_name

=> Diego Novais
```

Se formos refatorar o método usando block:

```ruby
def full_name
	yield
end

full_name do
	first_name = 'Diego'
	last_name = 'Novais'
	
	"#{first_name} #{last_name}"
end

=> Diego Novais
```

Podemos deixar nosso block mais dinâmico passando argumentos para nosso método e assim utilizando como parâmetros em nosso block:

```ruby
def full_name(prefix)
	puts prefix + yield
end

full_name('Sr. ') do |prefix|
	first_name = 'Diego'
	last_name = 'Novais'
	
	"#{first_name} #{last_name}"
end

=> Sr. Diego Novais
```

Como ultimo exemplo para fixar vamos criar nosso próprio `each` :

```ruby
def my_each(array)
  i = 0
  
  while i < array.size do
    yield array[i]
    i += 1
  end
end

array = [1, 2, 3, 4, 5]

my_each(array) do |number|
  puts number
end
```

Podemos também passar um block como parâmetro para um método:

```ruby
def full_name(&block)
	block.call
end

full_name do
	first_name = 'Diego'
	last_name = 'Novais'
	
	"#{first_name} #{last_name}"
end

=> Diego Novais
```

Mais um exemplo:

```ruby
def full_name(prefix, &block)
	puts prefix + block.call
end

full_name('Sr. ') do |prefix|
	first_name = 'Diego'
	last_name = 'Novais'
	
	"#{first_name} #{last_name}"
end

=> Sr. Diego Novais
```

## Proc

Um **Proc** se parece bastante com uma **lambda**, porém, caso não passe os argumentos não será disparado nenhum erro, pois um `proc` não se importa se irá passar um argumento ou não., vamos analisar isso com um pouco mais de código:

```ruby
say_something = proc { puts "Something..."  }
say_something.call

=> Something...
```

ou ...

```ruby
say_something = Proc.new do
	puts 'Something...'
end

say_something.call

=> Something...
```

Podemos também passar argumentos para um **Proc**:

```ruby
say_something = Proc.new do |name|
	puts "Hello #{name}"
end

say_something.call('Diego')

=> Hello Diego
```

Se não passarmos o argumento para um Proc, ele não ira se importar e não ira disparar um erro, considerando o exemplo anterior:

```ruby
say_something.call

=> Hello
```

## Lambda

Uma **Lambda** se parece mais com uma **função** do que uma **Proc**, principalmente pelo fato de respeitar os argumentos e pelo seu retorno, vamos analisar isso com um pouco mais de código, começando por algumas formas de definir um Lambda:

```ruby
# say_something = lambda { puts "Something..."  }
# ou...

say_something = -> { puts "Something..."  }
say_something.call

=> Something...
```

Podemos também passar argumentos para uma lambda:

```ruby
say_something = -> (name) { puts "Hello #{name}"  }
say_something.call('Diego')

=> Hello Diego
```

Obs.: se não passarmos o argumento um lambda dispara um erro.

### Lambda como blocos

Podemos também criar lambdas como blocks:

```ruby
say_something = lambda do |name|
	puts "Hello #{name}"
end

say_something.call('Diego')
```

Espero que este conteúdo possa ter te ajudado a compreender mais sobre Closures, block, proc e lambda. Te vejo no próximo conteúdo.
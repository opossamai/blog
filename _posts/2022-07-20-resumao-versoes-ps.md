---
layout: post
title:  "O que aconteceu de novo nas últimas versões do Powershell?"
date:   2022-07-20 20:00:00 -0300
categories: powershell atualizacao
---
O Windows Powershell como era conhecido há alguns anos atrás, mudou muito até os dias atuais (inclusive de nome). Diversas atualizações aconteceram para trazer melhorias à tecnologia e à comunidade que usa.  

Aqui vamos abordar algumas das principais mudanças das últimas três versões do Windows Powershell (5.0, 6.0 e 7.0).

## Windows Powershell 5.0
Lançada em Fevereiro de 2016, a versão 5.0 trouxe grandes avanços para a linguagem. Tornando-a ainda mais poderosa e abrangente, abrindo um leque ainda maior de possibilidades de utilização.

Vamos falar sobre algumas das principais mudanças:

### Classes
Talvez a maior e mais importante novidade dessa versão: a possibilidade de desenvolver utilizando classes.
Junto da versão 5.0 do Windows Powershell, foi adicionada a palavra-chave `Class` e toda uma série de sintaxes e semânticas similares à outras linguagens de programação orientadas a objeto.  
A introdução dessa possibilidade de criação de classes personalizadas pelo desenvolvedor, traz ao Powershell um novo espectro de desenvolvimento de aplicações e scripts. Dando mais ar e vida à linguagem.

### ConvertFrom-String
O cmdlet `ConvertFrom-String` é um passo da linguagem rumo a universalização. Abrindo ainda mais possibilidades para a operação com softwares/comandos que não trabalham com retornos .NET.  
`ConvertFrom-String` converte texto em objetos, seguindo um template informado pelo desenvolvedor.

Leia mais sobre [aqui](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/convertfrom-string?view=powershell-5.1).

### Módulo Microsoft.PowerShell.Archive
Inclui alguns cmdlets, como `Expand-Archive` e `Compress-Archive`, que permitem a compactação de arquivos em pastas ZIP e a extração das pastas desse mesmo formato. Acabando com a necessidade de instalação de softwares terceiros para realizar essa operações.

### Módulo PackageManagement
Esse módulo centraliza o gerenciamento de pacotes/softwares. Permitindo o manejo de múltiplos pacotes de diferentes provedores de forma simples e unificada. O desenvolvedor pode procurar, instalar, remover, etc. diferentes pacotes de diferentes provedores utilizando o mesmo comando e obtendo retornos padronizados.

### Módulo PowerShellGet
Uma facilitação da publicação, procura e instalação de módulos e recursos da [Powershell Gallery](https://www.powershellgallery.com/).

### CopyItem -ToSession e -FromSession
Agora é possível efetuar a cópia de itens entre sessões de diferentes computadores, criando uma sessão na máquina que será origem e/ou uma na máquina destino e então informando essas sessões para os parâmetros `-ToSession` e `-FromSession`.

> Leia a lista completa de alterações do Windows Powershell 5.1 [aqui](https://docs.microsoft.com/en-us/powershell/scripting/windows-powershell/whats-new/what-s-new-in-windows-powershell-50?view=powershell-5.1).

## Powershell Core 6.0
A versão 6.0 do, agora chamado somente de, Powershell, é a divisora de águas no ciclo da tecnologia.  
Lançada em Janeiro de 2018, a linguagem passa a ter seu código aberto a comunidade e ser multiplataforma.  
O objetivo do Powershell Core é ser o mais compatível possível com suas versões mais velhas (Windows Powershell), estimulando a migração para a nova versão sem muitos percalços, por parte dos usuários da linguagem.

Quais são as maiores novidades dessa versão? Veja abaixo:

### Multiplataforma
A ferramenta passa a ter suporte oficial ao macOS e uma série de distribuições Linux. Utilizando as soluções de cada sistema operacional para realizar as operações, como os sistemas de arquivos e logs.

### Instalação paralela (side-by-side)
A instalação da versão 6.0 do Powershell é feita separada do Windows Powershell, mantendo as duas versões instaladas e coexistindo.

### powershell.exe agora é pwsh.exe
A alteração da nomenclatura do executável é fundamental para se manter instalações simultâneas do Windows Powershell e Powershell Core.  
Assim, caso o usuário deseje executar a nova versão do Powershell, deve utilizar o executável `pwsh.exe`.

### Suporte a Docker
Powershell agora tem suporte aos Docker containers para a maior parte das plataformas.  

> Veja a lista completa de novidades do Powershell Core 6.0 [aqui](https://docs.microsoft.com/en-us/previous-versions/powershell/scripting/whats-new/what-s-new-in-powershell-core-60?view=powershell-6).

## Powershell 7.0
Lançada em Março de 2020, a versão 7.0 do Powershell traz uma série de grandes novidades, agora com a contribuição da comunidade no seu desenvolvimento.

### Foreach-Object -Parallel
Foi adicionado o parâmetro `-Parallel` ao cmdlet Foreach-Object. O parâmetro faz com que cada loop do laço execute paralelamente aos demais, podendo limitar o número de execuções simultâneas com o parâmetro `-ThrottleLimit`.
{% highlight powershell %}
    1..5 | Foreach-Object -Parallel {
        [bloco de script...]
    } -ThrottleLimit 5
{% endhighlight %}

### Operador ternário
Finalmente o famoso e tão pedido operador ternário foi adicionado à linguagem. Trazendo uma forma simplificada de fazer validações e executar ações para cada caso.
{% highlight powershell %}
(condicao) ? (caso sucesso) : (caso falha)
{% endhighlight %}

### Mais operadores de pipeline
Adicionados os operadores de pipeline `&&` e `||`, para encadear pipelines condicionalmente, funcionando de forma similar aos operadores `AND` e `OR`.  
O operador `&&` executa a operação da direita se a da esquerda for um sucesso.
{% highlight powershell %}
write-error "Erro" && Write-Host "O da esquerda passou"
>>Write-Host: Erro

write-host "Sucesso" && Write-Host "O da esquerda passou"
>>Sucesso
>>O da esquerda passou
{% endhighlight %}
O operador `||` executa a operação da direita se a da esquerda não for um sucesso.
{% highlight powershell %}
write-error "Erro" && Write-Host "O da esquerda passou"
>>Write-Host: Erro
>>O da esquerda passou

write-host "Sucesso" && Write-Host "O da esquerda passou"
>>Sucesso
{% endhighlight %}

Esses operadores usam as variáveis `$?` e `$LASTEXITCODE` para determinar se a operação anterior falhou ou não.

### Operadores de nulo
A versão 7.0 traz uma série de operadores de atribuição, acesso e condicionais, para trabalhar com valores nulos, como:  
Operador `??` traz a informação da direita se o da esquerda for nulo.  
{% highlight powershell %}
$valor = $null;
$valor ?? "teste";
>>teste
{% endhighlight %}
Operador `??=`atribui o valor informado se o valor a esquerda for nulo.  
{% highlight powershell %}
$valor = $null;
$valor ??= "valor era nulo, agora não é mais";
$valor
>>valor era nulo, agora não é mais
{% endhighlight %}
Operadores `?.` e `?[]` acessam os elementos e membros informados se os mesmos não forem nulos, se forem, retornam nulo.

Leia mais sobre todos esses operadores a partir [daqui](https://docs.microsoft.com/pt-br/powershell/module/microsoft.powershell.core/about/about_operators?view=powershell-7&preserve-view=true#null-coalescing-assignment-operator-).

### Melhoria dos erros
Isso mesmo, até mesmo os erros foram melhorados na versão 7.0 do Powershell.  
Foram feitas melhorias na demonstração de mensagens de erros, para facilitar a legibilidade dos mesmos. Permitindo que o usuário alterne o nível de detalhes que deseja que sejam demonstrados (ErrorView).  

Também foi intriduzido o cmdlet `Get-Error`, que traz uma visão completa, em forma de objeto, dos erros ocorridos.

> Veja a lista completa de novidades da versão 7.0 do Powershell [aqui](https://docs.microsoft.com/en-us/previous-versions/powershell/scripting/whats-new/what-s-new-in-powershell-70?view=powershell-7.1)

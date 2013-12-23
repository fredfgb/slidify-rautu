# Slidify-rautu

Utilização básica do [Slidify](http://www.slidify.org).

O Slidify é um pacote do [R](http://r-project.org), desenvolvido por
[Ramnath Vaidyanathan](https://github.com/ramnathv). Ele possibilita
escrever em [R Markdown](http://www.rstudio.com/ide/docs/r_markdown),
misturando a facilidade de escrita da linguagem
[Markdown](http://daringfireball.net/projects/markdown) com códigos do R
através do [Knitr](http://yihui.name/knitr/options).

A vantagem é que o Slidify faz todo o trabalho destes dois pacotes e
renderiza o resultado em um documento HTML5, possibilitando fazer slides
dinâmicos rapidamente.

O processo básico consiste em:
1. Editar o conteúdo em um arquivo `Rmd` (R Markdown)
2. Processar o contaúdo com o Slidify
3. Publicar o resultado em HTML em algum servidor

Aqui vamos utilizar o GitHub como servidor. Abaixo estão as instruções
detalhadas.

## Instalação

O Slidify não é um pacote do CRAN, por isso precisa ser instalado
diretamente da sua página de desenvolvimento no
[GitHub](https://github.com/ramnathv/slidify). A maneira mais fácil é
utilizar a função `install_github()` do pacote `devtools`. (O `devtools`
está no CRAN, e pode ser instaldo normalmente com
`install.packages()`). 

Além do pacote `slidify`, também é necessário instalar o
`slidifyLibraries` que contém diversos arquivos de configuração
utilizados pelo Slidify.

```r
require(devtools)
install_github("slidify", "ramnathv")
install_github("slidifyLibraries", "ramnathv")
```

## Utilização

### Criando um repositório no GitHub

A primeira coisa a fazer é criar um repositório no GitHub. Para isso
siga as instruções da
[página de ajuda do GitHub](https://help.github.com/articles/create-a-repo)
ou veja o [git-rautu](https://github.com/fernandomayer/git-rautu).

Por exemplo, aqui criei um diretório chamado `slidify-rautu` e iniciei
um repositório git nele.

### Iniciando a editoração com Slidify

Abra uma sessão do R dentro do diretório que você criou, e usa a função
`author("<diretorio>")` do Slidify para que ele gere todos os arquivos
necessários. Por exemplo,

```r
require(slidify)
author("slidify-template")
```
vai criar um novo diretório `slidify-template` com os arquivos
utilizados pelo Slidify. Como você já está em um repositório do GitHub,
ele criará automaticamente um novo *branch* chamado `gh-pages`, que é o
nome padrão para que o GitHub entenda que o conteúdo de um *branch* com
esse nome deve ser interpretado como uma página da web. Além disso, este
comando irá adicionar e *comitar* automaticamente todos estes arquivos
iniciais. Ainda, o arquivo `index.Rmd` deverá abrir em seu editor de
texto para que você possa iniciar a edição. (Caso não abra sozinho, ou
abra em um editor que você não queira utilizar, abra este arquivo da
forma que preferir).

Edite o conteúdo no arquivo `index.Rmd`. Veja como exemplo o arquivo
[](index.Rmd) deste repositório. 

### Processando o arquivo com Slidify

Após adicionar o conteúdo desejado, é hora de processar o arquivo
`index.Rmd` pelo Slidify no R:

```r
slidify("index.Rmd")
```

Esta função vai gerar os arquivos `index.md` (a conversão de R Markdown
para Markdown puro) e `index.html`. Este último arquivo está pronto para
a visualização em um navegador. Como é um arquivo estático, você pode
abri-lo diretamente no navegador para ver o resultado.

À medida que for editando o arquivo `index.Rmd` e usando a função
`slidify()`, você pode ir atualizando a página do arquivo `index.html`
para acompanhar o resultado final do seu trabalho.

### Publicando pelo GitHub

Note que até agora as modificações que foram feitas são apenas locais,
ou seja, nada foi publicado para o mundo.

Para publicar no GitHub utilizamos a função `publish()` com os seguintes
argumentos:
* `repo`: o nome do repositório aonde será publicado. Por exemplo, aqui
  o repositório é o `slidify-rautu`
* `username`: seu nome de usuário no GitHub
* `host`: o servidor utilizado, que por padrão já é o GitHub

Resumindo, a chamada dessa função será, neste caso,

```r
publish(repo = "slidify-rautu", username = "fernandomayer",
        host = "github")
```

Toda vez que essa função for chamada, os arquivos serão automaticamente
adicionados e *comitados* para o *branch* `gh-pages` do repositório do
GitHub, não sendo necessária mais nenhuma ação por parte do usuário.

O resultado estará então disponível no endereço
`http://<username>.github.io/<repo>`. Por exemplo, neste caso, os slides
deste repositório estão em
[http://fernandomayer.github.io/slidify-rautu](http://fernandomayer.github.io/slidify-rautu).

Note que não é necessário usar a função `publish()` a cada modificação
do arquivo `index.Rmd`. Você pode verificar as modificações localmente
no seu navegador enquanto edita este arquivo, e fazer a publicação uma
única vez apenas no final quando estiver tudo pronto.

Com o Slidify também é possível publicar no [Dropbox](http://www.dropbox.com) e
no [RPubs](http://rpubs.com) - veja `?publish` para isso.

## Resumo

Um *workflow* típico da utilização do Slidify consiste nos seguintes
passos (após já ter configurado um repositório `repo` no GitHub):

```r
require(slidify) # para carregar o pacote
author("diretorio") # apenas da PRIMEIRA VEZ
## Editar o arquivo index.Rmd
slidify("index.Rmd")
## Abra o arquivo resultante, index.html no navegador para ver o
## resultado
## Edite novamente o arquivo index.Rmd
slidify("index.Rmd")
## E assim sucessivamente...
## Quando estiver pronto pra publicação, faça
publish(repo = "repo", username = "nomedeusuario",
        host = "github")
```

## Mais informações

Você pode testar o Slidify direto no seu navegador, através deste
[playground](http://slidify.github.io/playground/index.html). Edite o
código à esquerda e veja o resultado na hora, à direita.

Com o Slidify você pode adicionar um
[quiz](http://slidify.github.io/iquiz) nos seus slides, ou até mesmo
gráficos dinâmicos com o [rCharts](http://rcharts.io)! Veja mais sobre
adicionar interatividade no link
[http://slidify.github.io/dcmeetup/demos/interactive](http://slidify.github.io/dcmeetup/demos/interactive) 


## Licença

<a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/deed.pt_BR"><img alt="Licença Creative Commons" style="border-width:0" src="http://i.creativecommons.org/l/by-sa/3.0/88x31.png" /></a><br />Esta obra foi licenciada sob uma Licença <a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/deed.pt_BR">Creative Commons Atribuição-CompartilhaIgual 3.0 Não Adaptada</a>.
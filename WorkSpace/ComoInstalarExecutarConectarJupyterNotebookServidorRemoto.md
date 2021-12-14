# Como Instalar, Executar, e Conectar no Jupyter Notebook em um Servidor Remoto

[Ubuntu](https://www.digitalocean.com/community/tags/ubuntu)[Python](https://www.digitalocean.com/community/tags/python)[Applications](https://www.digitalocean.com/community/tags/applications)[Ubuntu 18.04](https://www.digitalocean.com/community/tags/ubuntu-18-04)

- [![mrandrewandrade](https://secure.gravatar.com/avatar/11a2f40c612953c81eb6d3c94bfd00e5?secure=true&d=identicon)](https://www.digitalocean.com/community/users/mrandrewandrade)

- By [Andrew Andrade](https://www.digitalocean.com/community/users/mrandrewandrade)

  Published onDecember 12, 2019 20.3kviews

Português

*O autor selecionou [a Fundação do Software Apache](https://www.brightfunds.org/organizations/apache-software-foundation) para receber uma doação de $100 como parte do programa [Write for DOnations](https://do.co/w4do-cta).*

### Introdução

[O Jupyter Notebook](https://jupyter-notebook.readthedocs.io/en/stable/) é um aplicativo interativo Web de código aberto que permite que você escreva e execute códigos de computador em mais de 40 linguagens de programação, incluindo [Python](https://www.python.org/), [R](https://www.r-project.org/), [Julia](https://julialang.org/), e [Scala](https://www.scala-lang.org/). Um produto do [Projeto Jupyter](http://jupyter.org/about), Jupyter Notebook é útil para a programação iterativa, uma vez que ele permite que você escreva um pequeno fragmento de código, execute-o, e retorne o resultado.

O Jupyter Notebook dá a capacidade de criar documentos de anotação, referidos simplesmente como “notebooks”. Notebooks criados a partir do Jupyter Notebook são documentos de pesquisa compartilháveis, reproduzíveis que incluem elementos de rich text, equações, código e seus resultados (figuras, tabelas, gráficos interativos). Os notebooks também podem ser exportados para arquivos de código bruto, documentos HTML ou PDF, ou usados para criar slides interativos ou páginas Web.

Este artigo irá guiar você em como instalar e configurar o aplicativo Jupyter Notebook em um servidor Web do Ubuntu 18.04 e como se conectar a ele do seu computador local. Além disso, também vamos ver como usar o Jupyter Notebook para executar um exemplo de código Python.

## Pré-requisitos

Para completar este tutorial, você precisará de:

- Uma instância de servidor Ubuntu 18.04. Este servidor deve ter um usuário não-root com privilégios sudo e um firewall configurado. Você pode configurar isso seguindo nosso [guia de configuração inicial de servidor](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-18-04).
- Python 3, pip, e o módulo Python `venv` instalado no servidor. Faça isso seguindo os Passos 1 e 2 do nosso tutorial em [Como Instalar o Python 3 e Configurar um Ambiente de Programação Local no Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-programming-environment-on-an-ubuntu-18-04-server).
- Um navegador Web moderno funcionando no seu computador local que você usará para acessar o Jupyter Notebook.

Além disso, se seu computador local estiver usando o Windows, você precisará instalar o PuTTY nele para estabelecer um túnel SSH para seu servidor. Siga nosso guia em [Como Criar Chaves SSH com o PuTTY no Windows](https://www.digitalocean.com/community/tutorials/how-to-use-ssh-keys-with-putty-on-digitalocean-droplets-windows-users) para baixar e instalar o PuTTY.

## Passo 1 — Instalando o Jupyter Notebook

Uma vez que os notebook são usados para escrever, executar e ver o resultado de pequenos fragmentos de código, você primeiro precisará configurar o suporte de linguagem de programação. O Jupyter Notebook usa um *kernel* específico de linguagem, um programa de computador que executa e examina códigos. O Jupyter Notebook tem [muitos kernels em diferentes linguagens](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels), sendo padrão o [IPython](https://ipython.org/). Neste tutorial, você irá configurar o Jupyter Notebook para executar códigos Python através do kernel do IPython.

Supondo que você tenha seguido os tutoriais ligados na seção Pré-requisitos, você deve ter o [Python 3, pip e um ambiente virtual instalados](https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-local-programming-environment-on-ubuntu-18-04). Os exemplos neste guia seguem a convenção usada no tutorial pré-requisito na instalação do Python 3, que designa o ambiente virtual “`my_env`”, mas você deve sentir-se à vontade para renomear isso.

Inicie ativando o ambiente virtual:

```bash
source my_env/bin/activate
```

 

Copy

Em seguida, seu prompt será prefixado com o nome do seu ambiente.

Agora que você está no seu ambiente virtual, vá em frente e instale o Jupyter Notebook:

```bash
python3 -m pip install jupyter
```

 

Copy

Se a instalação tiver sido bem sucedida, você verá um resultado similar ao seguinte:

```
Output. . .
Successfully installed MarkupSafe-1.0 Send2Trash-1.5.0 backcall-0.1.0 bleach-2.1.3 decorator-4.3.0 entrypoints-0.2.3 html5lib-1.0.1 ipykernel-4.8.2 ipython-6.4.0 ipython-genutils-0.2.0 ipywidgets-7.2.1 jedi-0.12.0 jinja2-2.10 jsonschema-2.6.0 jupyter-1.0.0 jupyter-client-5.2.3 jupyter-console-5.2.0 jupyter-core-4.4.0 mistune-0.8.3 nbconvert-5.3.1 nbformat-4.4.0 notebook-5.5.0 pandocfilters-1.4.2 parso-0.2.0 pexpect-4.5.0 pickleshare-0.7.4 prompt-toolkit-1.0.15 ptyprocess-0.5.2 pygments-2.2.0 python-dateutil-2.7.3 pyzmq-17.0.0 qtconsole-4.3.1 simplegeneric-0.8.1 six-1.11.0 terminado-0.8.1 testpath-0.3.1 tornado-5.0.2
```

Com isso, o Jupyter Notebook foi instalado no seu servidor. Em seguida, vamos ver como executar o aplicativo.

## Passo 2 — Executando o Jupyter Notebook

O Jupyter Notebook deve ser executado do seu VPS para que você possa se conectar a ele da sua máquina local utilizando um Túnel SSH e seu navegador Web favorito.

Para executar o servidor do Jupyter Notebook, digite o seguinte comando:

```bash
jupyter notebook
```

 

Copy

Após executar este comando, você verá um resultado similar ao seguinte:

```
Output[I 19:46:22.031 NotebookApp] Writing notebook server cookie secret to /home/sammy/.local/share/jupyter/runtime/notebook_cookie_secret
[I 19:46:22.365 NotebookApp] Serving notebooks from local directory: /home/sammy/environments
[I 19:46:22.365 NotebookApp] 0 active kernels
[I 19:46:22.366 NotebookApp] The Jupyter Notebook is running at:
[I 19:46:22.366 NotebookApp] http://localhost:8888/?token=Example_Jupyter_Token_3cadb8b8b7005d9a46ca4d6675
[I 19:46:22.366 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[W 19:46:22.366 NotebookApp] No web browser found: could not locate runnable browser.
[C 19:46:22.367 NotebookApp]

    Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://localhost:8888/?token=Example_Jupyter_Token_3cadb8b8b7005d9a46ca4d6675&tokenExample_Jupyter_Token_3cadb8b8b7005d9a46ca4d6675
```

Você pode notar no resultado que há um aviso `No web browser found`. Isso é esperado, uma vez que o aplicativo está funcionando em um servidor e você provavelmente ainda não instalou um navegador Web nele. Este guia irá examinar como se conectar ao Notebook no servidor utilizando o tunelamento SSH na seção seguinte.

Por enquanto, saia do Jupyter Notebook pressionando `CTRL+C` seguido por `y`, e então pressione `ENTER` para confirmar:

```
OutputShutdown this notebook server (y/[n])? y
[C 20:05:47.654 NotebookApp] Shutdown confirmed
[I 20:05:47.654 NotebookApp] Shutting down 0 kernels
```

Então, saia do servidor utilizando o comando `exit`:

```bash
exit
```

 

Copy

Você acabou de executar o Jupyter Notebook no seu servidor. Entretanto, para acessar o aplicativo e começar a trabalhar com notebooks, você precisará se conectar ao aplicativo utilizando o tunelamento SSH e um navegador Web no seu computador local.

## Passo 3 — Conectando-se ao Aplicativo Jupyter Notebook com o Tunelamento SSH

O *Tunelamento SSH* é uma maneira simples e rápida de se conectar ao aplicativo Jupyter Notebook em execução no seu servidor. Secure shell (mais frequentemente conhecido como [SSH](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys)) é um protocolo de rede que permite que você se conecte a um servidor remoto com segurança em uma rede não segura.

O protocolo SSH inclui um mecanismo de encaminhamento de porta que permite que você encaminhe certos aplicativos em execução em um número de porta específico em um servidor para um número de porta específico no seu computador local. Iremos aprender como “encaminhar” com segurança o aplicativo Jupyter Notebook em execução no seu servidor (na porta `8888`, por padrão) para uma porta no seu computador local.

O método que você usa para estabelecer um túnel SSH irá depender do sistema operacional do seu computador local. Pule para a subsecção abaixo que é a mais relevante para a sua máquina.

**Nota:** É possível configurar e instalar o Jupyter Notebook utilizando o Console Web do DigitalOcean, mas se conectar ao aplicativo através de um túnel SSH deve ser feito através do terminal ou com o PuTTY.

### Tunelamento SSH utilizando macOS ou Linux

Se seu computador local está executando Linux ou macOS, é possível estabelecer um túnel SSH apenas executando um único comando.

`ssh` é o comando padrão para abrir uma conexão SSH, mas quando usado com a diretiva `-L`, você pode especificar que uma dada porta no host local (ou seja, sua máquina local) será encaminhada para um dado host e porta no host remoto (neste caso, seu servidor). Isso significa que o que estiver sendo executado na porta especificada no servidor remoto (`8888`, porta padrão do Jupyter Notebook) aparecerá na porta especificada no seu computador local (`8000` no comando exemplo).

Para estabelecer seu próprio túnel SSH, execute o seguinte comando. Sinta-se à vontade para alterar a porta `8000` para outra que você queira se, por exemplo, a `8000` estiver em uso por outro processo. É recomendável que você utilize uma porta maior ou igual a `8000`, uma vez que é pouco provável que esses números de porta sejam usados por outro processo. Certifique-se de incluir o endereço IP do seu próprio servidor e o nome do usuário não-root do seu servidor:

```bash
ssh -L 8000:localhost:8888 sammy@your_server_ip
```

 

Copy

Se não houver erros neste comando, ele irá logar você no seu servidor remoto. A partir daí, ative o ambiente virtual:

```bash
source ~/environments/my_env/bin/activate
```

 

Copy

Então, execute o aplicativo Jupyter Notebook:

```bash
jupyter notebook
```

 

Copy

Para se conectar ao Jupyter Notebook, utilize seu navegador Web favorito para navegar até a porta local no host local: `http://localhost:8000`. Agora que você está conectado ao Jupyter Notebook, continue para o Passo 4 para aprender a usá-lo.

### Tunelamento SSH utilizando Windows e PuTTY

O PuTTY é um cliente SSH de código aberto para o Windows que pode ser usado para [se conectar ao seu servidor](https://www.digitalocean.com/community/tutorials/how-to-use-ssh-keys-with-putty-on-digitalocean-droplets-windows-users). Após baixar e instalar o PuTTY na sua máquina Windows (tal como descrito no tutorial pré-requisito), abra o programa e digite o URL ou endereço IP do seu servidor, como mostrado aqui:

![Enter server URL or IP into Putty](https://assets.digitalocean.com/articles/jupyter_notebook/JN_putty_1.png)

Em seguida, clique em **+ SSH** ao final do painel esquerdo, e então clique em **Tunnels**. Nesta janela, digite a porta que você quiser usar para acessar o Jupyter na sua máquina local (`8000` ). É recomendável que você utilize uma porta maior ou igual a `8000`, uma vez que é pouco provável que esses números de porta sejam usados por outro processo. Se `8000` é usado por outro processo, no entanto, selecione um número de porta diferente e não utilizado. Em seguida, configure o destino como `localhost:8888`, uma vez que a porta `8888` é aquela na qual o Jupyter Notebook está funcionando. Então, clique no botão **Add** e as portas devem aparecer no campo **Forwarded** ports:

![Configure SSH tunnel in Putty](https://assets.digitalocean.com/articles/jupyter_notebook/JN_putty_2.png)

Finalmente, clique no botão **Open**. Isso irá conectar sua máquina ao servidor através do SSH e ligar as portas desejadas. Se nenhum erro aparecer, vá em frente e ative seu ambiente virtual:

```bash
source ~/environments/my_env/bin/activate
```

 

Copy

Então, execute o Jupyter Notebook:

```bash
jupyter notebook
```

 

Copy

Em seguida, navegue até a porta local no seu navegador Web favorito, por exemplo `http://localhost:8000` (ou qualquer número de porta que você escolheu), para se conectar à instância do Jupyter Notebook que está sendo executada no servidor. Agora que você está conectado ao Jupyter Notebook, continue para o Passo 4 para aprender a usá-lo.

## Passo 4 — Usando o Jupyter Notebook

Quando acessado através de um navegador Web, o Jupyter Notebook fornece um Painel do Notebook, que atua como um navegador de arquivos e dá a você uma interface para criar, editar e explorar notebooks. Pense nestes notebooks como documentos (salvos com uma extensão de arquivo `.ipynb`) que você pode preencher com qualquer número de células individuais. Cada célula possui um editor de texto interativo que pode ser usado para executar códigos ou escrever texto renderizado. Além disso, os notebooks permitem que você escreva e execute equações, inclua outras mídias valiosas, como imagens ou gráficos interativos, e eles podem ser exportados e compartilhados em vários formatos (`.ipyb`, `.pdf`, `.py`). Para ilustrar algumas destas funções, vamos criar um arquivo de notebook a partir do Painel do Notebook, escrever um quadro de texto simples com uma equação, e executar um código básico de Python 3.

Até este ponto, você deve ter se conectado ao servidor utilizando um túnel SSH e iniciado o aplicativo Jupyter Notebook do seu servidor. Após navegar para `http://localhost:8000`, você será apresentado com uma página de login:

![Jupyter Notebook login screen](https://assets.digitalocean.com/articles/jupyter_notebook/JN_login_screen_small.png)

No campo **Password** or token ao topo, digite o token exibido no resultado após você executar `jupyter notebook` do seu servidor:

```
Output[I 20:35:17.004 NotebookApp] Writing notebook server cookie secret to /run/user/1000/jupyter/notebook_cookie_secret
[I 20:35:17.314 NotebookApp] Serving notebooks from local directory: /home/sammy
[I 20:35:17.314 NotebookApp] 0 active kernels
[I 20:35:17.315 NotebookApp] The Jupyter Notebook is running at:
[I 20:35:17.315 NotebookApp] http://localhost:8888/?token=Example_Jupyter_Token_3cadb8b8b7005d9a46ca4d6675
[I 20:35:17.315 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[W 20:35:17.315 NotebookApp] No web browser found: could not locate runnable browser.
[C 20:35:17.316 NotebookApp]
. . .
```

De forma alternativa, você pode copiar aquele URL do resultado do seu terminal e colá-lo na barra de endereço do seu navegador.

Automaticamente, o Jupyter Notebook irá mostrar todos os arquivos e pastas armazenados no diretório do qual ele está sendo executado. Crie um novo arquivo de notebook clicando em **New** então **Python 3** no canto superior direito do Painel Notebook:

![Create a new Python3 notebook](https://assets.digitalocean.com/articles/jupyter_notebook/JN_new_python3.png)

Dentro deste novo notebook, mude a primeira célula para que aceite a sintaxe markdown clicando em **Cell** > **Cell Type** > **Markdown** na barra de navegação no topo. Além da remarcação, este Cell Type também permite que você escreva equações em LaTeX. Por exemplo, digite o seguinte na célula após alterá-la para markdown:

```
# Simple Equation

Let us now implement the following equation in Python:
$$ y = x^2$$

where $x = 2$
```

Para transformar o markdown em rich text, pressione `CTRL + ENTER` e o resultado deve ser o seguinte:

![Turn sample equation into rich text](https://assets.digitalocean.com/articles/jupyter_notebook/JN_sample_equation.png)

Você pode usar as células markdown para fazer anotações e documentar seu código.

Agora, vamos implementar uma equação simples e imprimir o resultado. Clique em **Insert** > **Insert Cell Below** para inserir uma célula. Nesta nova célula, digite o seguinte código:

```
x = 2
y = x*x
print(y)
```

Para executar o código, pressione `CTRL + ENTER`, e o resultado será o seguinte:

![Solve sample equation](https://assets.digitalocean.com/articles/jupyter_notebook/JN_sample_equation2.png)

Estes são alguns exemplos relativamente simples do que você pode fazer com o Jupyter Notebook. No entanto, ele é um aplicativo muito poderoso com muitos casos de uso possíveis. A partir daqui, adicione algumas bibliotecas Python e utilize o notebook como você faria com qualquer outro ambiente de desenvolvimento Python.

## Conclusão

Agora, você deve ser capaz de escrever códigos reprodutíveis Python e texto utilizando o Jupyter Notebook em funcionamento em um servidor remoto. Para fazer um tour rápido pelo Jupyter Notebook, clique em **Help** na barra de navegação superior e selecione o **User Interface Tour** como mostrado aqui:

![Finding Jupyter Notebook help tour](https://assets.digitalocean.com/articles/jupyter_notebook/JN_help_tour.png)

Se você estiver interessado, encorajamos você a aprender mais sobre o Jupyter Notebook através da [documentação do Projeto Jupyter](http://jupyter.org/documentation). Além disso, você pode construir desenvolver o que você aprendeu neste tutorial [aprendendo como programar em Python 3](https://www.digitalocean.com/community/tutorial_series/how-to-code-in-python-3).
# Como configurar/instalar o `BRL-CAD` no `Linux`

## Resumo

Neste documento estão contidos os principais comandos e configurações para configurar/instalar o `BRL-CAD` no `Linux`.

## _Abstract_

_In this document are contained the main commands and settings to set up/install the `BRL-CAD` on `Linux`._

## Descrição

### `BRL-CAD`

O `BRL-CAD` é um poderoso sistema de modelagem sólida de código aberto usado principalmente para design e análise de objetos 3D em ambientes técnicos e de engenharia. Ele oferece uma ampla variedade de ferramentas e recursos para criar, visualizar e simular geometrias complexas, tornando-o valioso para aplicações que envolvem modelagem 3D, como design de produtos, análise de estruturas e simulações virtuais. O `BRL-CAD` é conhecido por sua capacidade de lidar com modelos sólidos de alta complexidade e é amplamente utilizado em instituições acadêmicas e industriais para uma variedade de projetos e pesquisas que envolvem o trabalho com objetos tridimensionais detalhados e precisos. Sua natureza de código aberto permite que os desenvolvedores personalizem e estendam suas funcionalidades de acordo com suas necessidades específicas de modelagem e análise 3D.


## 1. Como configurar/instalar o `BRL-CAD` no `Linux Ubuntu` [1]

Para configurar o `BRL-CAD`, você pode seguir estas etapas:

1. Abra o terminal. Você pode fazer isso pressionando: `Ctrl + Alt + T`

2. Certifique-se de que seu sistema esteja limpo e atualizado.

    2.1 Limpar o `cache` do gerenciador de pacotes `apt`. Especificamente, ele remove todos os arquivos de pacotes (`.deb`) baixados pelo `apt` e armazenados em `/var/cache/apt/archives/`. Digite o seguinte comando: `sudo apt clean` 
    
    2.2 Remover pacotes `.deb` antigos ou duplicados do cache local. É útil para liberar espaço, pois remove apenas os pacotes que não podem mais ser baixados (ou seja, versões antigas de pacotes que foram atualizados). Digite o seguinte comando: `sudo apt autoclean`

    2.3 Remover pacotes que foram automaticamente instalados para satisfazer as dependências de outros pacotes e que não são mais necessários. Digite o seguinte comando: `sudo apt autoremove -y`

    2.4 Buscar as atualizações disponíveis para os pacotes que estão instalados em seu sistema. Digite o seguinte comando e pressione `Enter`: `sudo apt update`

    2.5 **Corrigir pacotes quebrados**: Isso atualizará a lista de pacotes disponíveis e tentará corrigir pacotes quebrados ou com dependências ausentes: `sudo apt --fix-broken install`

    2.6 Limpar o `cache` do gerenciador de pacotes `apt`. Especificamente, ele remove todos os arquivos de pacotes (`.deb`) baixados pelo `apt` e armazenados em `/var/cache/apt/archives/`. Digite o seguinte comando: `sudo apt clean` 
    
    2.7 Para ver a lista de pacotes a serem atualizados, digite o seguinte comando e pressione `Enter`:  `sudo apt list --upgradable`

    2.8 Realmente atualizar os pacotes instalados para as suas versões mais recentes, com base na última vez que você executou `sudo apt update`. Digite o seguinte comando e pressione `Enter`: `sudo apt full-upgrade -y`
    

## 2. Compilando [3]

### 2.1 Compilando o `BRL-CAD`

Esta Seção simplifica etapas para compilar.

### 2.1.1 Etapa 1: instalar ferramentas de desenvolvimento

Para compilar, você deve possuir ou instalar o `CMake` mais recente, um compilador recente e pelo menos 3 GB de espaço em disco. Você também deve possuir ou instalar o `Git` o qual irá clonar o código-fonte mais recente.

#### Versões mínimas:

- CMake deve ser 3.18 ou posterior

- Git deve ser 2.17 ou posterior

- O compilador deve ser compatível com C++ 11
    
    - Se estiver usando o Visual Studio, versão 2015 (14.0+) ou posterior
    
    - Se estiver usando GCC/G++, versão 4.8.1 ou posterior
    
    - Se estiver usando LLVM/Clang 3.3 ou posterior
    
    - Se estiver usando Intel, versão 2015 (15.0+) ou posterior

#### Subsistemas `Linux`

1. A instalação é mais fácil com um sistema de gerenciamento de pacotes como `apt`, `brew`, `yum` e `dnf` que é instalado para você: `sudo apt install build-essential make cmake -y`

### 2.2 Etapa 2: instalar dependências [3]

#### `Linux`

1. `BRL-CAD` precisa dos pacotes de desenvolvimento `Xorg`:

    ```
    sudo apto install libc6-dev libfreetype-dev libfontconfig-dev -y
    sudo apt install xserver-xorg-dev libx11-dev libxi-dev libglu1-mesa-dev -y
    ```

## 3. Habilitar chave ssh

1. **Verificar se você tem uma chave `SSH`:** Primeiro, verifique se você já tem uma chave `SSH` gerada no seu sistema. No terminal, digite: `cat ~/.ssh/id_rsa.pub`

    Se você receber uma mensagem dizendo que o arquivo não existe, você precisará criar uma nova chave `SSH`.

2. **Gerar uma Nova Chave `SSH` (se necessário):** Se você não tem uma chave `SSH`, crie uma com o seguinte comando: `ssh-keygen -t rsa -b 4096 -C "seu_email@example.com"`

    Substitua `"seu_email@example.com"` pelo email que você usa no GitHub.

    Durante o processo, será solicitado para você escolher onde salvar a chave e criar uma senha segura.

3. **Adicionar a Chave `SSH` ao `ssh-agent`:** Inicie o `ssh-agent` em background: `eval "$(ssh-agent -s)"`

    5.1 **Adicione sua chave `SSH` privada ao `ssh-agent`:** `ssh-add ~/.ssh/id_rsa`

4. **Adicionar a Chave `SSH` à sua Conta do GitHub:** 

    4.1 Copie a chave `SSH` para a sua área de transferência: `cat ~/.ssh/id_rsa.pub | xclip -sel clip`

    4.2 Vá para as configurações de `SSH` e `GPG` do `GitHub`.

    4.3 Clique em `"New SSH key"` ou `"Add SSH key"`.

    4.4 No campo `"Title"`, adicione um nome descritivo para a nova chave.

    4.5 Cole sua chave no campo `"Key"`.

    4.6 Clique em `"Add SSH key"`.

5. **Tentar Clonar Novamente:** Depois de adicionar a chave `SSH` à sua conta do `GitHub`, tente clonar o repositório novamente: `git clone git@github.com:BRL-CAD/brlcad.git`

Esses passos devem resolver o problema de permissão. Lembre-se de que a chave `SSH` precisa estar associada à conta do GitHub que tem acesso ao repositório que você está tentando clonar.

A pasta `"brlcad"` criada após a clonagem é um checkout completo do `BRL-CAD` e contém um `README` com informações adicionais. Se você tiver problemas para clonar do `git`, versões de origem de snapshot estarão disponíveis no link: <https://sourceforge.net/projects/brlcad/files/BRL-CAD%20Source/>


## 4. Etapa 4: crie um diretório `Build` [3]

Você pode criar uma pasta de compilação em qualquer lugar, mas normalmente ela é chamada de `"build"` e está no diretório de origem `"brlcad"` ou próximo a ela.

### 4.1 `Linux`

1. Execute o comando: `mkdir -p build`

## 5. Etapa 5: configurar

Primeiramente, é recomendado durante a configuração e compilação que você suspenda temporariamente qualquer software antivírus, pois eles são conhecidos por emitir alertas de falsos positivos e bloquear operações necessárias. Algumas ferramentas `BRL-CAD` usam portas de rede temporárias que também precisarão ser permitidas, se solicitado.

A seguir, você executará o `CMake` para configurar e gerar um sistema de compilação.

O `CMake` precisa saber o diretório de origem de nível superior (ou seja, o diretório `"brlcad"` que você clonou) e o diretório `"build"` que você criou estão localizados. Pela primeira vez, também recomendamos definir estas variáveis ​​CMake para evitar problemas triviais:

Para definir variáveis de ambiente ao usar o `CMake` em sistemas Linux, você pode usar a opção `-D` seguida do nome da variável e seu valor. Aqui estão os comandos para definir as variáveis de ambiente que você mencionou:

1. **`BRLCAD_ENABLE_STRICT`:** Para definir `BRLCAD_ENABLE_STRICT` como `"DESATIVADO"`, você pode usar o seguinte comando: `cmake -DBRLCAD_ENABLE_STRICT=OFF ..`

    Substitua `..` pelo caminho para o diretório onde você está executando o `CMake` ou especifique o caminho completo.

2. **`BRLCAD_ENABLE_COMPILER_WARNINGS`:** Para definir `BRLCAD_ENABLE_COMPILER_WARNINGS` como "DESLIGADO", você pode usar o seguinte comando: `cmake -DBRLCAD_ENABLE_COMPILER_WARNINGS=OFF ..`

3. **`BRLCAD_BUNDLED_LIBS`:** Para definir `BRLCAD_BUNDLED_LIBS` como "ON", você pode usar o seguinte comando: `cmake -DBRLCAD_BUNDLED_LIBS=ON ..`

    Certifique-se de que o caminho para o diretório onde está executando o `CMake` está correto e inclua o `..` no final do comando para indicar o diretório onde o arquivo `CMakeLists.txt` está localizado.

Depois de definir essas variáveis de ambiente com os comandos acima, você pode continuar com o processo de configuração e compilação usando o `CMake` para o projeto `BRL-CAD`. Certifique-se de revisar a saída do `CMake` para verificar se as variáveis foram definidas corretamente de acordo com suas configurações.

Consulte `INSTALL` para mais opções do `CMake` no link: <https://github.com/BRL-CAD/brlcad/blob/main/INSTALL>

Se o `CMake` tiver sucesso, haverá um resumo da compilação impresso no final, ele dirá `"Configurado"` e depois `"Gerado"` após um sistema de compilação ser finalmente escrito para a compilação do `BRL-CAD`.

Se o `CMake` não tiver êxito, verifique a saída em busca de mensagens de erro indicando o que está falhando ou faltando, pois normalmente é uma ferramenta ausente, uma biblioteca ausente ou uma configuração incorreta.

## 6. Compilar [3]

### 6.1 `Linux`

1. Ainda no diretório de compilação da Etapa 4, execute:  `make`

    - Se você tiver vários núcleos, poderá alternativamente compilar em paralelo especificando um número desejado de núcleos, por exemplo: `make -j10`

A instalação do `BRL-CAD` a partir do código fonte é um processo mais técnico que envolve várias etapas. Aqui está um guia geral sobre como fazer isso no Linux:

**Nota:** A compilação pode levar de alguns minutos a uma hora, dependendo do hardware. Se você tivesse uma CPU quad-core, você poderia executar '"make -j4" para acelerar as coisas compilando em paralelo.


## Etapa 7: Executar

Você não precisa instalar para executar o `BRL-CAD`. Você pode executar os binários que acabou de compilar como estão no diretório `brlcad/build/bin`. Das centenas de ferramentas do `BRL-CAD`, aqui estão apenas algumas para você começar:

    ```
    bin/benchmark run
    bin/mged
    bin/archer
    ```

O primeiro comando (benchmark) avaliará o desempenho do sistema e você poderá enviar os resultados para benchmark em `brlcad dot org`.

O segundo comando (`mged`) é o principal aplicativo de interface gráfica do usuário do `BRL-CAD`.

O terceiro comando (arqueiro) é a interface gráfica mais recente do `BRL-CAD` em desenvolvimento.

### 1.1 Codigo completo para configurar/instalar

Para instalar o `BRL-CAD` no `Linux` sem precisar digitar linha por linha, você pode seguir estas etapas:

1. Abra o `Terminal Emulator`. Você pode fazer isso pressionando: `Ctrl + Alt + T`

2. Digite o seguinte comando e pressione `Enter`:

    ```
    NÃO há.
    ```


## Referências

[1] OPENAI. ***FreeCAD e arquivos .prt no Linux.*** Disponível em: <https://chat.openai.com/c/4d66a3c1-dae0-4cf5-b9fb-3e4e2979a61e> (texto adaptado). ChatGPT. Acessado em: 29/01/2024 10:06.

[2] OPENAI. ***Vs code: editor popular.*** Disponível em: <https://chat.openai.com/c/b640a25d-f8e3-4922-8a3b-ed74a2657e42> (texto adaptado). ChatGPT. Acessado em: 29/01/2024 10:06.

[3] BRL-CAD. ***Compiling.*** Disponível em: <https://brlcad.org/wiki/Compiling> (texto adaptado). BRL-CAD team. Acessado em: 30/01/2024 09:34.


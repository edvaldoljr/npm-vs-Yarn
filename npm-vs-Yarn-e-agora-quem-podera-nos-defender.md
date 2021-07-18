# npm vs Yarn: e agora, quem poderá nos defender?

Ouvir sobre *npm* ou Yarn dentro da comunidade JavaScript é bastante comum, mas você sabe quais são suas diferenças, qual é o melhor ou até para que eles servem?

Podemos dizer que ambos são gerenciadores de dependências/pacotes, similares ao Composer do PHP e NuGet do .NET, permitindo o reaproveitamento de código e, por consequência, acelerando o desenvolvimento em contraste com o armazenamento de códigos JavaScript em outros projetos ou em CNDs como costumava ser feito. Afinal, se quando você vai fazer um bolo não precisa plantar o trigo e fazer a farinha, por que não aplicar essa mesma lógica ao desenvolvimento, não é mesmo?

> If you wish to make an apple pie from scratch, you must first invent the universe. – Carl Sagan

## *npm*: o que é?

O [*npm*](https://www.npmjs.com/) é um projeto Open Source criado em 2009 com objetivo de facilitar a troca de código JavaScript, sendo usado como gerenciador de pacotes padrão do [Node.js](https://nodejs.org/). Ao falarmos de *npm* podemos estar nos referindo a um destes itens:

1. O repositório aberto onde ficam armazenados os pacotes
2. Um cliente que permite o envio/download de código do repositório
3. Um site onde é possível pesquisar informações dos pacotes e ver a documentação do npm.

Também existe uma empresa chamada NPM, Inc., que é a mantenedora do repositório aberto de pacotes e coordena o desenvolvimento do *npm*. Ela também trabalha no desenvolvimento de soluções pagas focadas no mercado empresarial.

O *npm* utiliza um arquivo de configuração chamado package.json. Este arquivo é o responsável pela configuração do projeto como o nome,a versão, atalhos de comandos que *npm* executa, etc. Uma das funções mais importantes é a de armazenar uma lista de dependências que o projeto irá utilizar. Com este arquivo e o cliente do *npm* é possível instalar todas as dependências com apenas um comando, sendo muito útil quando você precisa executar um projeto em um novo ambiente ou durante a execução de ferramentas de integração contínua.

Mas, e quando o projeto é aquele ~~aerolito~~ monolito, com tantas dependências que você até cogita ver um episódio da sua série favorita enquanto instala? É aí que o Yarn se torna atrativo em comparação ao *npm*.

## Yarn: uma história

Em outubro de 2016, o Facebook lançou o [Yarn](https://yarnpkg.com/en/) em conjunto com o Google, Exponent e Tilde, com o objetivo de tornar o processo de instalação das dependências não só mais rápido, mas também mais seguro.

No Facebook, muitos dos projetos que dependiam do *npm* apresentavam certos problemas, como:

- Demora no tempo de instalação
- Dependência que não possuíam a mesma versão em diversas máquinas
- A forma que o *npm* executa códigos das dependências de forma automática

Após tentar algumas soluções alternativas para resolver estas questões, alguns engenheiros começaram a trabalhar em um cliente novo, buscando resolver estes problemas a partir da raiz.

Até o lançamento do Yarn, o *npm* realizava as instalações das dependências de forma não determinística, ou seja, a estrutura da pasta node_modules poderia ser diferente de uma pessoa para outra, causando aquele velho problema do “Mas na minha máquina funciona!”. Para contornar este problema, o Yarn faz uso de arquivos de lock (yarn.lock) e de um algoritmo de instalação determinístico. No arquivo de lock a versão exata da dependência é armazenada, garantindo que todas as instalações são iguais. Apesar de o *npm* já possuir uma opção para gerar arquivos de lock, o Yarn gera seu arquivo de lock automaticamente.

Para acelerar a instalação, o Yarn consulta um diretório de cache global, que é usado tanto para evitar que o download seja feito, quanto para permitir a instalação enquanto estiver offline, o que não era possível realizar com o *npm*.

O processo de instalação através do Yarn é feito em três etapas, sendo elas:

1. Busca recursiva de dependências no repositório do *npm*
2. Procura no cache global e, caso a dependência ainda não tenha sido baixada, salva uma cópia no cache global
3. Conecta as dependências ao copiá-las do cache global para a pasta node_modules local

Desta forma, o Yarn consegue maximizar o uso dos recursos disponíveis e reduzir o tempo de instalação. Em diversos testes de performance realizados após o lançamento do Yarn, [ele mostrou-se muito mais rápido que o *npm*](https://yarnpkg.com/lang/en/compare/).

Em março de 2017, após um ano e meio de desenvolvimento, foi lançada versão 5 do *npm*, trazendo diversas melhorias de performance semelhantes às presentes no Yarn. Nesta versão, o *npm* já cria um arquivo de lock chamado *package-lock.json* automaticamente; é capaz de instalar dependências a partir do cache; realiza validações de hashes SHA-512 e a velocidade de instalação aumentou cerca de 5x comparada com a anterior. Se você já instalou a versão 8 do Node.js, ela já conta com o *npm* 5 instalado por padrão.

## Mas, qual utilizar?

O melhor de tudo é que tanto o *npm* quanto o Yarn utilizam o *package.json*, dando a você a escolha sobre qual melhor se adequa à sua necessidade. Na Umbler não poderia ser diferente, não é mesmo?

Se você usa o *npm*, não é necessário mais nada. O comando `npm install` vai ser executado durante o deploy da sua aplicação. Lembrando que se você já usa o Node.js 8, é indicado que você adicione o arquivo *package-lock.json* no versionamento de código para aproveitar todos os benefícios da nova versão do *npm*.
Já se você usa o Yarn, é só ter certeza que o arquivo yarn.lock foi adicionado no controle de versão que, durante o deploy, será identificado o uso do Yarn e o comando `yarn install` será executado.

Está esperando o que para testar *npm* e *Yarn* agora mesmo? 


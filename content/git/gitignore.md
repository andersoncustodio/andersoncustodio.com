---
title: Gerenciando o Rastreamento de Arquivos com .gitignore
linkTitle: .gitignore
type: docs
prev: /git/
---

O arquivo `.gitignore` é utilizado para especificar quais arquivos ou diretórios devem ser ignorados pelo Git.

Isso é útil para evitar que arquivos temporários, arquivos de configuração local, dependências geradas automaticamente
e outros arquivos desnecessários sejam incluídos no repositório.

É possível utilizar múltiplos arquivos `.gitignore` em diferentes diretórios do projeto. As regras definidas
em cada arquivo `.gitignore` serão aplicadas apenas aos arquivos e diretórios contidos no mesmo diretório e
seus subdiretórios. No entanto, a prática mais comum é manter um único arquivo `.gitignore` na raiz do
repositório para gerenciar todas as exclusões de forma centralizada.

## Sintaxe
A sintaxe do arquivo `.gitignore` é simples e direta. Aqui estão algumas regras básicas:

- Linhas que começam com `#` são comentários e são ignoradas pelo Git.
- Linhas em branco também são ignoradas.
- Para ignorar um arquivo ou diretório específico, basta escrever o nome do arquivo ou diretório.
- Para ignorar todos os arquivos de um determinado tipo, use o caractere curinga `*`. Por exemplo, `*.log` ignora todos os arquivos com a extensão `.log`.
- Para ignorar um diretório e todo o seu conteúdo, adicione uma barra `/` no final do nome do diretório. Por exemplo, `logs/` ignora o diretório `logs` e todos os seus arquivos e subdiretórios.
- Para negar uma regra de ignorar, use o caractere de exclamação `!`. Por exemplo, `!important.txt` garante que o arquivo `important.txt` não seja ignorado, mesmo que uma regra anterior o ignore.
- Para ignorar arquivos ou diretórios em qualquer lugar do projeto, use `**`. Por exemplo, `**/temp` ignora todos os diretórios chamados `temp`, independentemente de sua localização.


## Exemplo de .gitignore
Aqui está um exemplo de um arquivo `.gitignore` típico para um projeto de desenvolvimento de software

```sh
# Ignorar arquivos de log
*.log
logs/

# Ignorar arquivos temporários
*.tmp
*.swp

# Ignorar diretórios de dependências
node_modules/
vendor/

# Ignorar arquivos de configuração local
.env
config/local.yml

# Ignorar arquivos de build
dist/
build/

# Negar a exclusão de um arquivo específico
!important.txt
```

## .gitkeep

O Git não rastreia diretórios vazios, então se você quiser manter um diretório vazio no repositório,
você pode adicionar um arquivo chamado `.gitkeep` dentro desse diretório. O arquivo `.gitkeep` não tem
nenhum significado especial para o Git, é apenas uma convenção para indicar que o diretório deve ser
mantido no repositório.

Com isso, você não precisa se preocupar em criar o diretório manualmente ou fazer algum script para
criar o diretório quando for clonar o repositório.

Como foi dito, é apenas uma convenção, você pode nomear esse arquivo como quiser, mas o nome `.gitkeep`
é amplamente utilizado e reconhecido pela comunidade.


## .git/info/exclude

Além do arquivo `.gitignore`, o Git também oferece um arquivo de exclusão local chamado `.git/info/exclude`.
Esse arquivo funciona de maneira semelhante ao `.gitignore`, mas é específico para o repositório local
e não é compartilhado com outros colaboradores do projeto.

O arquivo `.git/info/exclude` é útil para ignorar arquivos ou diretórios que são específicos do ambiente
de desenvolvimento local, como arquivos de configuração do editor de texto ou arquivos temporários gerados
pelo sistema operacional.

Então se você utilizar alguma ferramenta diferente dos outros colaboradores do projeto, você pode adicionar
as regras de exclusão específicas para essa ferramenta no arquivo `.git/info/exclude`, sem afetar o arquivo
`.gitignore` compartilhado.

## Modo White-list
Uma abordagem alternativa ao modo "padrão" de exclusão é o modo white-list, onde você especifica
quais arquivos ou diretórios devem ser rastreados pelo Git, ignorando todos os outros.

O modo white-list é uma abordagem de como configuramos o `.gitignore` para incluir apenas  os arquivos e diretórios que
queremos rastrear, não é necessariamente algum tipo de extensão ou funcionalidade  adicional do Git.

Para deixarmos o `.gitignore` em modo white-list, ele precisa apenas começar com as seguintes linhas:

```sh
# Ignorar tudo por padrão
*

# Não ignorar diretórios
!*/
```

A primeira linha de instrução com `*` ignora tudo de forma global, e a segunda com `!*/` garante que os diretórios
não sejam ignorados, veja que a segunda regra é específica para os diretórios, todos os arquivos ainda serão ignorados.

O `!*/` é o ponto-chave para o modo white-list, sem ele não iríamos conseguir incluir nenhum arquivo dentro de outros
diretórios, como dito anteriormente, todos os arquivos continuam sendo ignorados, em seguida temos que escrever regras
específicas para cada um dos arquivos ou diretórios que queremos rastrear.

Exemplos de regras para incluir arquivos ou diretórios específicos que queremos rastrear:
```sh
# Incluir arquivos específicos
!README.md

# Incluir todos os arquivos em um diretório específico e todos os seus subdiretórios
!/src/**/*

# Incluir arquivos específicos na raiz do projeto
!/package.json
!/package-lock.json
!/tsconfig.json

# Incluir um arquivo específico no diretório e subdiretórios
!/storage/**/.gitkeep

```

Com essa configuração, apenas os arquivos e diretórios explicitamente listados serão rastreados pelo Git,
enquanto todos os outros serão ignorados.


No exemplo acima, onde incluímos o arquivo `.gitkeep` dentro do diretório `storage`, foi necessário especificar
o caminho completo. Se tentássemos criar uma regra geral como `!**/.gitkeep`, o Git incluiria todos os
arquivos `.gitkeep` do projeto, mesmo aqueles localizados em diretórios que normalmente deveriam ser ignorados,
como `node_modules` ou `vendor`.

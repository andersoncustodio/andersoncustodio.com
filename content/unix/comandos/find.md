---
title: find - Procurar arquivos e diretórios
description: 'Utilizando o comando `find` para procurar arquivos e diretórios no Linux ou MacOS'
type: docs
---

## Diferentes formas de procurar por um arquivo

### Por nome

Com case-sensitive

```sh
find . -name "arquivos.txt"
```

Sem case-sensitive

```sh
find . -iname "arquivos.txt"
```

### Por tipo

Pesquisar por diretório

```sh
find . -type d
```
Pesquisar por arquivo

```sh
find . -type d
```

### Por data
Arquivos mais antigos em n dias
```sh
find . -mtime +1
```

Arquivos modificados em n dias
```sh
find . -mtime -1
```

Lista todos os arquivos alterados em menos de *1 minuto*
```sh
find . -mmin -1
```

Lista todos os arquivos alterados nas últimas *24 horas*
```sh
find . -newermt "-24 hours" -ls
```

Listar todos os arquivos alterados no dia *11/04/2020*
```sh
find . -newermt "2020-04-11" -ls
```

### Por permissão


Procurar arquivos por permissão por modo octal

```sh
find . -perm -744
```
### Por proprietário

Procurar arquivos pertencentes a um usuário

```sh
find . –user anderson
```

Procurar arquivos pertencentes a um grupo

```sh
find . –group adm
```

### Por tamanho

Procurar arquivos com o tamanho exato de 10m

```sh
find . -size 10M
```

Procurar arquivos com o tamanho superior a 10m

```sh
find . -size +10M
```
Com menos de 10m

```sh
find . -size -10M
```

### Por arquivo vazio

Procurar por arquivos ou pastas vazias

```sh
find . -empty
```

```sh
find . -type d -empty
```

```sh
find . -type f -empty
```

#### Unidades de medida para utilizar com o find -size

| Carácter | Descrição          |
|----------|--------------------|
| `c`      | bytes              |
| `k`      | kilobytes          |
| `M`      | megabytes          |
| `G`      | gigabytes          |
| `B`      | blocos de 512-byte |

### Procurar por tipo

Procurar arquivos por tipo

```sh
find . -type f
```
| Carácter | Descrição                  |
|----------|----------------------------|
| `f`      | arquivo normal             |
| `d`      | diretório ou pasta         |
| `l`      | link simbólico             |
| `c`      | dispositivos de caracteres |
| `b`      | dispositivos bloqueados    |

## Condicionais para combinar diferentes formas de pesquisa

### and

```sh
find -name "*dog" -type f
```
`-and` é o padrão, o comando acima é igual a `find -name "*dog" -and -type f`

### or

```sh
find -name "dog" -or -name "cat"
```

### not
```sh
find -not -name "dog"
```

### group

```sh
find \( -name "dog" -or -name "cat" \) -type f
```
{{< callout type="warning" >}}
É importante ter um espaço depois de `\(` e antes de `\)`, caso o contrário ocorrerá um erro.
{{< /callout >}}

#### Alias de condicionais

- `-o` = `-or`
- `-a` = `-and`
- `!` &nbsp; = `-not` (Talvez precise escapar `\!`)

## Executar ações com os arquivos encontrados

O find não seve somente como uma forma de procurar arquivos, ele também serve como um filtro para executar comandos.

### Deletar arquivos encontrados
Devemos tomar cuidado com esse parâmetro use-o apenas em ocasiões que o arquivo sempre terá que ser apagando, sem existir o risco de perder informação.

```sh
find . -name "*.tpm" -delete
```

### Executar um comando para cada arquivo encontrado

Com o parâmetro `-exec` podemos executar um comando para cada arquivo encontrado ou para todos ao mesmo tempo.

Esse parâmetro, por padrão, substitui os caracteres `{}` com o caminho de cada arquivo encontrado ou com a lista de todos os arquivos encontrados.

No final do `-exec` sempre temos que utilizar `\;` ou `+`:
- `\;` o comando será executado separadamente em cada arquivo encontrado.
- `+` o comando será executado uma única vez para todos os arquivos encontrados.

{{< callout >}}
Existem alguns comandos que aceitam como parâmetro mais de um arquivo ou caminho, `mkdir pata1 pasta2 pasta3` ou `touch arquivo1.txt arquivo2.txt arquivo3.txt`, são nesses casso que podemos utilizar o `+` no final do `-exec`, se for utilizado com um comando que não é compatível com esses exemplos o resultado não será o esperado.
{{< /callout >}}

Irá executar o `chmod` em cada arquivo encontrado

```sh
find -name "*.php" -exec chmod 755 {} \;
```
Irá executar o `chmod` uma única vez em todos os arquivos encontrados

```sh
find -name "*.php" -exec chmod 755 {} +;
```

## Outros

Limitar um número de subdiretórios

```sh
find . -maxdepth 1
```

## Exemplo prático

Procurar todos os arquivos `.php` e `.phtml` que não tem a permissão `755` e modificar a permissão para esse valor.

```sh
find . \( -name "*.php" -or -name "*.phtml" \) -type f -not -perm 0755 -exec chmod 755 {} \;
```

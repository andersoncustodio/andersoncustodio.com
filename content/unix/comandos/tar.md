---
title: tar - Unificador de arquivos
description: Utilizando o comando `tar` para compactar e unificar arquivos
type: docs
---
# 

O comando `tar` foi criado para o Unix, e seu nome deriva de "Tape ARchive", em português significa "Arquivo de Fita".

Este comando permite unir vários arquivos em um só, também é possível utilizar parâmetros `z`, `j` e `J` para compactar o arquivo `.tar`

Por esse motivo é comum termos arquivos com a extensão `.tar.gz`, ela indica que temos um arquivo `tar` compactado com `gzip`.

{{< callout type="warning" >}}
Diferente do comando `tar` o `gzip` não faz a união de arquivos, ele apenas compacta cada um separadamente, por isso é tão comum compactar arquivos `.tar` com `gzip`
{{< /callout >}}


### Compactando arquivos

Compactar um arquivo
{{< callout >}}
Embora seja possível utilizar o tar com gzip para apenas um arquivo, geralmente prefiro utilizar somente o comando `gzip`, repare que todos os comandos `tar` a seguir utilizam o parâmetro `z`.
{{< /callout >}}
```sh
tar -zcvf nome-arquivo.tar.gz arquivo.txt
```

Compactar múltiplos arquivos
```sh
tar -zcvf nome-arquivo.tar.gz arquivo.txt arquivo2.txt
```

Compactar um diretório
```sh
tar -zcvf nome-arquivo.tar.gz diretorio/
```

Compactar múltiplos diretório
```sh
tar -zcvf nome-arquivo.tar.gz diretorio/ diretorio2/
```

### Descompactar arquivo tar

Descompactar arquivos tar no diretório atual
```sh
tar -zxvf nome-arquivo.tar
```

Descompactar múltiplos arquivos
```sh
tar -zxvf nome-arquivo.tar nome-arquivo2.tar
```

| Parâmetro | Descrição                                       |
|-----------|-------------------------------------------------|
| `-c`      | Cria um novo arquivo tar                        |
| `-x`      | Extrai arquivo tar                              |
| `-z`      | Compacta o arquivo tar usando o algoritmo gzip. |
| `-v`      | Mostra os arquivos que estão sendo processados. |
| `-f`      | Especifica o nome do arquivo de arquivo tar.    |

---
title: gzip - Compactador de arquivos
description: Comando para compactar e descompactar arquivos
type: docs
---

Diferente do commando [tar](/unix/comandos/tar.md) o `gzip` faz a compressão de arquivos.

O `gzip` não compacta vários arquivos em um único arquivo, ao invés disso ele compacta cada arquivo separadamente, por esse motivo é comum termos arquivos `.tar.gz`, o `tar` unifica os arquivos e o `gzip` (arquivos com extensão `.gz`), faz o papel de compactador.

## Compactando arquivos

Por padrão o nome do arquivo permanecerá o mesmo, apenas adicionando `.gz` como extensão.
```sh
gzip arquivo.txt
```

Compactar vários arquivo com um comando. (lembrando que cada arquivo será compactado separadamente)
```sh
gzip arquivo.txt arquivo2.txt arquivo3.txt
```

Compactar arquivos em diretório de forma recursiva
```sh
gzip -r nome-diretorio/
```

## Descompactando arquivos

O `gzip` não tem um parâmetro para descompactar arquivos, mas sim um outro comando específico para esse propósito.
```sh
gunzip arquivo.txt.gz
```
Descompactar vários arquivo com um comando.
```sh
gunzip arquivo.txt.gz arquivo2.txt.gz arquivo3.txt.gz
```

Descompactar arquivos em diretório de forma recursiva
```sh
gunzip -r nome-diretorio/
```

## O comando `zcat`

O `gzip` também possui o comando `zcat`, com ele podemos visualizar o conteúdo de um gzip sem extrair o arquivo de fato.

```sh
zcat arquivo.gz
```

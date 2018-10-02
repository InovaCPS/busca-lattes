# Busca Lattes

Busca de professores por suas especialidades utilizando como base o seu lattes, extraído do sistema do CNPq.

## Equipe

A nossa equipe faz parte do departamento INOVA do CPS. Clique [aqui](Equipe.md) pra conhecê-los.

## Project Charter

![project charter](https://raw.githubusercontent.com/InovaCPS/busca-lattes/master/Imagens/Project%20Charter.png)

## Microsserviços

* [inova-proxy](https://github.com/InovaCPS/inova-proxy)
* [inova-log](https://github.com/InovaCPS/inova-log)

# Workflow - Getting Started

## Problema
O problema atual é que não temos um lugar para fazer busca de nossos professores.

## Objetivo
Criar um site que tenha um lugar para buscar nossos professores por suas habilidades e qualidades.

## Workflow
Este projeto é contruído sob a arquitetura de microsserviços, conheça mais clicando [aqui](https://exame.abril.com.br/negocios/dino/explorando-a-arquitetura-de-microsservicos/)

### Primeiro serviço (web-bot)

Neste primeiro serviço, é resolvido a comunicação entre CPS e CNPq, mandamos um CPF para o web service do CNPq e ele retorna para nós um xml, que irá subir para nossa base no S3.

A base de CPF's tem origem do nosso RH e ela será utilizada para atualizar nosso banco de dados.

![image](https://user-images.githubusercontent.com/43144590/45553023-0ac99680-b809-11e8-9679-c22414aeaa7b.png)

O nosso S3 solta as informações em xml.

### Segundo serviço (indexação)

Nosso segundo serviço recebe uma informação xml e faz um ciclo no S3 criando a indexação da informação.
O index é feito utilizando Whoosh, a lista de indexação é [cpf, bag-of-words, id_lattes, nome].

Neste [link](https://pythonprogramminglanguage.com/bag-of-words/) você pode ler mais sobre bag-of-words e seu funcionamento.

![image](https://user-images.githubusercontent.com/43144590/45553626-d35be980-b80a-11e8-9a52-2f869eb614bf.png)

Com o Whoosh http://whoosh.readthedocs.io/en/latest/intro.html é possível criar um index facilmente, usando o texto extraído dos CVs. Mais sobre como funcionam os índices de busca: https://en.wikipedia.org/wiki/Search_engine_indexing


## License

This project is licensed under the share-alike license - see the [LICENSE](LICENSE) file for details

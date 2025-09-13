# Análise de Malware em PDF

Repositório para a Análise de Ameaças em Documentos do Formato Portátil (PDF).

## Limitações dos Antivírus Comerciais

O *modus operandi* para a identificação de arquivos maliciosos consiste, tecnicamente, na consulta a bancos de dados conhecidos como *blocklists*. A plataforma VirusTotal emite diagnósticos sobre características malignas relacionadas a arquivos e servidores web, utilizando os resultados dos principais produtos antivírus comerciais do mundo. O VirusTotal possui Interfaces de Programação de Aplicação (APIs) que permitem aos programadores consultar a plataforma de forma automatizada.

Nesta análise, os arquivos PDF maliciosos são submetidos ao servidor do VirusTotal, onde são analisados pelos antivírus comerciais vinculados à plataforma. Cada antivírus pode fornecer três tipos de diagnóstico:

1.  **Malware:** A ameaça foi detectada (acerto).
2.  **Benigno:** A ameaça não foi detectada (falso negativo).
3.  **Omissão:** Nenhuma opinião foi emitida.

Para este estudo, foram investigados **73 antivírus comerciais** utilizando **727 amostras de PDF maliciosos**. O objetivo é avaliar a eficácia de cada antivírus contra esta categoria de ameaça.

Os resultados revelam uma grande disparidade. A detecção de *malware* variou de 0% a 96,56%, dependendo do antivírus. Em média, os 73 antivírus foram capazes de detectar **34,72%** das ameaças avaliadas, com um desvio padrão de **33,37%**. O alto desvio padrão indica que a proteção contra PDFs maliciosos pode sofrer variações abruptas dependendo da solução de segurança escolhida.

Quanto aos falsos negativos, em média, os antivírus atestaram erroneamente que o *malware* era benigno em **48,39%** dos casos, com um desvio padrão de **36,35%**. A taxa média de omissão foi de **16,89%**, com desvio padrão de **27,59%**.

Uma grande adversidade no combate a aplicações maliciosas é o fato de que os fabricantes de antivírus não compartilham suas *blocklists* devido a disputas comerciais. A análise dos dados aponta um fator agravante: o mesmo fornecedor nem sequer compartilha totalmente suas bases entre seus diferentes produtos (ex: McAfee e McAfee-GW-Edition).

Outro ponto crítico é a falta de um padrão na classificação dos *malwares*. Como não existe uma taxonomia unificada, os antivírus atribuem os nomes que desejam (ex: "Trojan.PDF.Generic" vs. "PDF:Phishing-A [Trj]"). Essa falta de padronização, somada ao não compartilhamento de informações, dificulta a detecção rápida e eficaz de ameaças.

#### Tabela 1: Amostra dos Resultados de Antivírus Comerciais (10 Melhores e 10 Piores)

| Antivírus              | Detecção (%) | Falso Negativo (%) | Omissão (%) |
| ---------------------- | :----------: | :----------------: | :---------: |
| **Melhores Desempenhos** |              |                    |             |
| GData                  |    96,56%    |       0,96%        |    2,48%    |
| Ikarus                 |    95,87%    |       3,30%        |    0,83%    |
| McAfee                 |    93,54%    |       3,85%        |    2,61%    |
| Avast                  |    93,26%    |       3,58%        |    3,16%    |
| AVG                    |    93,26%    |       0,41%        |    6,33%    |
| ESET-NOD32             |    90,10%    |       8,94%        |    0,96%    |
| Fortinet               |    89,27%    |       10,59%       |    0,14%    |
| Rising                 |    83,08%    |       15,13%       |    1,79%    |
| Avira                  |    81,02%    |       18,98%       |     0%      |
| Cynet                  |    80,61%    |       18,98%       |    0,41%    |
| ...                    |     ...      |        ...         |     ...     |
| **Piores Desempenhos** |              |                    |             |
| VBA32                  |    0,14%     |       99,86%       |     0%      |
| Zoner                  |    0,14%     |       98,90%       |    0,96%    |
| Acronis                |      0%      |       99,17%       |    0,83%    |
| Kingsoft               |      0%      |       96,84%       |    3,16%    |
| TACHYON                |      0%      |        100%        |     0%      |
| CMC                    |      0%      |        100%        |     0%      |
| SUPERAntiSpyware       |      0%      |       99,86%       |    0,14%    |
| Baidu                  |      0%      |       99,04%       |    0,96%    |
| Malwarebytes           |      0%      |       99,86%       |    0,14%    |
| TotalDefense           |      0%      |       89,80%       |   10,20%    |

*(Fonte: Análise de 727 amostras de PDF maliciosos via VirusTotal.)*

## Materiais e Métodos

Este projeto utiliza um banco de dados para a classificação de documentos PDF benignos e maliciosos, contendo **727 amostras maliciosas** e um número similar de amostras benignas. O *dataset* é, portanto, balanceado e adequado para o treinamento de modelos de inteligência artificial.

As amostras de *malware* são arquivos PDF extraídos de bancos de dados disponibilizados pela comunidade de segurança através da plataforma VirusShare. A construção do ambiente de teste para a análise dinâmica foi realizada utilizando o software de *sandbox* **Cuckoo**.

## Extração de Características Dinâmicas

As características dos arquivos PDF são extraídas através da análise dinâmica. Para isso, o documento malicioso é executado em um ambiente controlado (*sandbox*) para infectar, intencionalmente, um sistema operacional, enquanto seu comportamento é auditado em tempo real pelo Cuckoo. As principais características analisadas são:

###### Ações de Scripts

A auditoria verifica se o documento PDF, através de *scripts* embutidos (geralmente *JavaScript*), tenta:

* Executar processos externos ou *shellcode*.
* Utilizar funções de API suspeitas para interagir com o sistema operacional.
* Empregar técnicas de ofuscação de código para evadir a detecção.

###### Persistência

Verifica se o *malware* tenta se manter ativo no sistema após uma reinicialização, por meio de táticas como:

* Criar ou modificar arquivos em diretórios de inicialização do sistema (*startup*).
* Alterar chaves de registro do Windows para garantir a autoexecução.

###### Modificações no Sistema

É auditado se o arquivo suspeito tenta:

* Alocar memória de leitura, escrita e execução, geralmente para descompactar um *payload*.
* Identificar a presença de ferramentas de análise (antivírus, *debuggers*) para alterar seu comportamento.
* Criar, apagar ou modificar arquivos e certificados do sistema.

###### Ações de Rede

A auditoria verifica se o documento tenta:

* Conectar-se a uma URL ou endereço de IP suspeito para baixar uma segunda fase do ataque.
* Comunicar-se com servidores de Comando e Controle (C&C) conhecidos.
* Gerar tráfego de rede incomum (HTTP, DNS, etc.).

###### Comportamento de *Ransomware*

Verifica se o *malware* exibe comportamentos típicos de *ransomware*, como:

* Criptografar arquivos do usuário e adicionar extensões específicas.
* Escrever uma mensagem de resgate no disco.
* Tentar apagar cópias de sombra do sistema para dificultar a recuperação.

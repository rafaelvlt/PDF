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

#### Tabela 1: Amostra dos Resultados de Antivírus

| Antivírus | Detecção (%) | Falso Negativo (%) | Omissão (%) |
| :--- | :--- | :--- | :--- |
| GData | 96,56% | 0,96% | 2,48% |
| Ikarus | 95,87% | 3,30% | 0,83% |
| McAfee | 93,54% | 3,85% | 2,61% |
| AVG | 93,26% | 0,41% | 6,33% |
| Avast | 93,26% | 3,58% | 3,16% |
| ESET-NOD32 | 90,10% | 8,94% | 0,96% |
| Fortinet | 89,27% | 10,59% | 0,14% |
| Rising | 83,08% | 15,13% | 1,79% |
| Avira | 81,02% | 18,98% | 0,00% |
| Cynet | 80,61% | 18,98% | 0,41% |
| DrWeb | 77,44% | 21,87% | 0,69% |
| CAT-QuickHeal | 74,69% | 25,03% | 0,28% |
| Lionic | 67,68% | 30,26% | 2,06% |
| MicroWorld-eScan | 65,61% | 34,39% | 0,00% |
| Symantec | 64,65% | 29,44% | 5,91% |
| FireEye | 64,65% | 33,29% | 2,06% |
| BitDefender | 64,65% | 33,84% | 1,51% |
| Emsisoft | 63,96% | 34,25% | 1,79% |
| Arcabit | 59,83% | 39,89% | 0,28% |
| Sangfor | 58,87% | 34,94% | 6,19% |
| VIPRE | 56,26% | 42,37% | 1,38% |
| ViRobot | 56,26% | 43,74% | 0,00% |
| AhnLab-V3 | 55,57% | 44,43% | 0,00% |
| Antiy-AVL | 55,30% | 43,19% | 1,51% |
| SentinelOne | 55,16% | 37,00% | 7,84% |
| Tencent | 55,16% | 43,33% | 1,51% |
| Varist | 53,92% | 1,24% | 44,84% |
| Google | 52,54% | 1,24% | 46,22% |
| MAX | 51,86% | 33,29% | 14,86% |
| Kaspersky | 49,11% | 48,56% | 2,34% |
| Skyhigh | 46,08% | 7,29% | 46,63% |
| ZoneAlarm | 44,84% | 47,18% | 7,98% |
| Cyren | 43,88% | 0,00% | 56,12% |
| F-Secure | 41,68% | 57,91% | 0,41% |
| McAfee-GW-Edition | 41,40% | 0,14% | 58,46% |
| MaxSecure | 40,30% | 42,50% | 17,19% |
| ALYac | 28,75% | 68,78% | 2,48% |
| Microsoft | 23,25% | 72,49% | 4,26% |
| alibabacloud | 19,26% | 4,68% | 76,07% |
| Cylance | 15,27% | 47,73% | 37,00% |
| Kingsoft | 14,58% | 82,12% | 3,30% |
| CTX | 13,62% | 0,69% | 85,69% |
| VirIT | 10,59% | 46,77% | 42,64% |
| TrendMicro | 9,63% | 87,62% | 2,75% |
| TrendMicro-HouseCall | 9,35% | 89,96% | 0,69% |
| huorong | 9,22% | 9,77% | 81,02% |
| Ad-Aware | 8,67% | 32,87% | 58,46% |
| Sophos | 4,54% | 93,95% | 1,51% |
| Xcitium | 2,89% | 54,75% | 42,37% |
| Yandex | 1,24% | 98,21% | 0,55% |
| Baidu | 0,96% | 97,94% | 1,10% |
| NANO-Antivirus | 0,96% | 98,76% | 0,28% |
| ClamAV | 0,96% | 95,74% | 3,30% |
| K7GW | 0,55% | 99,31% | 0,14% |
| K7AntiVirus | 0,55% | 99,17% | 0,28% |
| TACHYON | 0,55% | 99,45% | 0,00% |
| Zillya | 0,41% | 97,11% | 2,48% |
| Qihoo-360 | 0,28% | 0,14% | 99,59% |
| Panda | 0,28% | 99,04% | 0,69% |
| Jiangmin | 0,14% | 99,04% | 0,83% |
| Bkav | 0,14% | 98,49% | 1,38% |
| Cybereason | 0,00% | 9,63% | 90,37% |
| CrowdStrike | 0,00% | 22,97% | 77,03% |
| tehtris | 0,00% | 23,80% | 76,20% |
| Comodo | 0,00% | 41,13% | 58,87% |
| BitDefenderTheta | 0,00% | 84,32% | 15,68% |
| Gridinsoft | 0,00% | 84,46% | 15,54% |
| VBA32 | 0,00% | 98,35% | 1,65% |
| Malwarebytes | 0,00% | 98,76% | 1,24% |
| Acronis | 0,00% | 99,72% | 0,28% |
| CMC | 0,00% | 99,72% | 0,28% |
| SUPERAntiSpyware | 0,00% | 100,00% | 0,00% |
| Zoner | 0,00% | 100,00% | 0,00% |

*(Fonte: Análise de 727 amostras de PDF maliciosos via VirusTotal.)*

#### Tabela 2: Exemplos de Classificações Divergentes para as Mesmas Amostras de Malware

| Antivírus | VirusShare_045289... | VirusShare_0b2549... | VirusShare_1a3809... |
| :--- | :--- | :--- | :--- |
| **Acronis** | (Não detectado) | (Não detectado) | (Não detectado) |
| **AhnLab-V3** | Phishing/PDF.Malurl.XG5 | Phishing/PDF.Malurl.XG4 | Phishing/PDF.Malurl.XG4 |
| **ALYac** | PDF.Spam.Heur.1 | (Não detectado) | (Não detectado) |
| **Antiy-AVL** | (Não detectado) | (Não detectado) | (Não detectado) |
| **Arcabit** | PDF.Spam.Heur.1 | PDF.Spam.Heur.1 | PDF.Spam.Heur.1 |
| **Avast** | PDF:PhishingX-gen [Phish] | PDF:PhishingX-gen [Phish] | PDF:PhishingX-gen [Phish] |
| **AVG** | PDF:PhishingX-gen [Phish] | PDF:PhishingX-gen [Phish] | PDF:PhishingX-gen [Phish] |
| **Avira** | HTML/Malicious.PDF.Gen2 | HTML/Malicious.PDF.Gen2 | HTML/Malicious.PDF.Gen2 |
| **Baidu** | (Não detectado) | (Não detectado) | (Não detectado) |
| **BitDefender** | PDF.Spam.Heur.1 | PDF.Spam.Heur.1 | PDF.Spam.Heur.1 |
| **BitDefenderTheta** | (Não detectado) | (Não detectado) | (Não detectado) |
| **Bkav** | (Não detectado) | (Não detectado) | (Não detectado) |
| **CAT-QuickHeal**| PDF.Phishing.44452 | PDF.Phishing.45004 | PDF.Phishing.43742 |
| **CMC** | (Não detectado) | (Não detectado) | (Não detectado) |
| **ClamAV** | (Não detectado) | (Não detectado) | (Não detectado) |
| **Cybereason** | (não listado) | (Não detectado) | (não listado) |
| **Cynet** | Malicious (score: 99) | Malicious (score: 99) | Malicious (score: 99) |
| **Cyren** | PDF/Captchaphish.D.gen!Camelot | (não listado) | (não listado) |
| **DrWeb** | PDF.Phisher.300 | PDF.Phisher.300 | PDF.Phisher.300 |
| **ESET-NOD32** | PDF/Phishing.A.Gen | PDF/Phishing.Agent.NDP | PDF/Phishing.Agent.NDP |
| **Emsisoft** | PDF.Spam.Heur.1 (B) | PDF.Spam.Heur.1 (B) | PDF.Spam.Heur.1 (B) |
| **F-Secure** | Malware.HTML/Malicious.PDF.Gen2 | Malware.HTML/Malicious.PDF.Gen2 | Malware.HTML/Malicious.PDF.Gen2 |
| **FireEye** | PDF.Spam.Heur.1 | PDF.Spam.Heur.1 | PDF.Spam.Heur.1 |
| **Fortinet** | PDF/Phishing.818B!tr | PDF/FakeRobot.EC81!tr | PDF/FakeRobot.EC81!tr |
| **GData** | PDF.Trojan-Stealer.Phishing.E | PDF.Trojan-Stealer.Phishing.E | PDF.Trojan-Stealer.Phishing.E |
| **Google** | Detected | Detected | Detected |
| **Gridinsoft** | (Não detectado) | (Não detectado) | (Não detectado) |
| **Ikarus** | Phishing.PDF.Doc | Phishing.PDF.Doc | Phishing.PDF.Doc |
| **Jiangmin** | (Não detectado) | (Não detectado) | (Não detectado) |
| **K7AntiVirus** | (Não detectado) | (Não detectado) | (Não detectado) |
| **K7GW** | (Não detectado) | (Não detectado) | (Não detectado) |
| **Kaspersky** | UDS:Hoax.PDF.Phish.gen | HEUR:Hoax.PDF.Phish.gen | HEUR:Hoax.PDF.Phish.gen |
| **Kingsoft** | (Não detectado) | (Não detectado) | (Não detectado) |
| **Lionic** | Trojan.PDF.Phishing.4!c | Trojan.PDF.Phishing.4!c | Hacktool.PDF.Phish.3!c |
| **MAX** | malware (ai score=82) | malware (ai score=81) | malware (ai score=85) |
| **Malwarebytes** | (Não detectado) | (Não detectado) | (Não detectado) |
| **MaxSecure** | Trojan.W32.pdf.spam.heur.1 | (Não detectado) | (não listado) |
| **McAfee** | PDF/Phish-FAK!045289229D5F| PDF/Phish-FOF!0B2549FC20D4 | PDF/Phish-FOF!1A3809A3C09F |
| **McAfee-GW-Edition**| BehavesLike.PDF.Suspicious.mb | (não listado) | (não listado) |
| **MicroWorld-eScan**| PDF.Spam.Heur.1 | PDF.Spam.Heur.1 | PDF.Spam.Heur.1 |
| **Microsoft** | (Não detectado) | (Não detectado) | (Não detectado) |
| **NANO-Antivirus** | (Não detectado) | (Não detectado) | (Não detectado) |
| **Panda** | (Não detectado) | (Não detectado) | (Não detectado) |
| **Rising** | Trojan.Phishing/PDF!1.D8B8 | Trojan.Phishing/PDF!1.D9C3 | Trojan.Phishing/PDF!1.D9C3 |
| **SUPERAntiSpyware** | (Não detectado) | (Não detectado) | (Não detectado) |
| **Sangfor** | Malware.Generic-HTML.Save.ma33 | Malware.Generic-HTML.Save.ma33 | Malware.Generic-HTML.Save.ma33 |
| **SentinelOne** | Static AI - Malicious PDF | Static AI - Malicious PDF | Static AI - Malicious PDF |
| **Skyhigh** | (não listado) | BehavesLike.PDF.Suspicious.lb | BehavesLike.PDF.Suspicious.lb |
| **Sophos** | (Não detectado) | (Não detectado) | (Não detectado) |
| **Symantec** | Trojan.Gen.NPE | Trojan.Gen.NPE | Trojan.Gen.NPE |
| **TACHYON** | (Não detectado) | (Não detectado) | (Não detectado) |
| **Tencent** | PDF.Win32.Script.900445 | Trojan.Pdf.Phishing.ll | Trojan.Pdf.Phishing.ll |
| **TrendMicro** | (Não detectado) | (Não detectado) | (Não detectado) |
| **TrendMicro-HouseCall**| (Não detectado) | (Não detectado) | (Não detectado) |
| **VBA32** | (Não detectado) | (Não detectado) | (Não detectado) |
| **VIPRE** | PDF.Spam.Heur.1 | PDF.Spam.Heur.1 | PDF.Spam.Heur.1 |
| **Varist** | (não listado) | PDF/Captchaphish.D.gen!Camelot | PDF/Captchaphish.D.gen!Camelot |
| **ViRobot** | PDF.Z.Agent.85089.IR | PDF.Z.Agent.77802.OH | PDF.Z.Agent.81686.NX |
| **VirIT** | (Não detectado) | (Não detectado) | (Não detectado) |
| **Xcitium** | (Não detectado) | (Não detectado) | (Não detectado) |
| **Yandex** | (Não detectado) | (Não detectado) | (Não detectado) |
| **Zillya** | (Não detectado) | (Não detectado) | (Não detectado) |
| **ZoneAlarm** | UDS:Hoax.PDF.Phish.gen | HEUR:Hoax.PDF.Phish.gen | HEUR:Hoax.PDF.Phish.gen |
| **Zoner** | (Não detectado) | (Não detectado) | (Não detectado) |
| **alibabacloud** | (não listado) | SypWare:PDF/Phishing.Akg

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

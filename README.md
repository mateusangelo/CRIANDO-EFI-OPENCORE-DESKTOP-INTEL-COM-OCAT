# CRIANDO EFI OPENCORE P/DESKTOP INTEL COM OCAT (OC Auxiliary Tools)
HACKINTOSH: CRIANDO EFI OPENCORE DESKTOP INTEL COM OCAT + GUIA INSTALAÇÃO COMPLETO 100% VANILLA 



Importante:

* A partir desse ponto o OC Auxiliary Tools será referenciado  como OCAT
* Esse guia é compativel com Desktop Intel com processadores de 1ª até 12ª geração
* Em caso de Duvidas, acesse nossas comunidades:
 *  YouTube 👉  [https://www.youtube.com/c/DicasdoMateus]()
 * Grupo Telegram 👉  [https://t.me/grupodicasdomateus]()
  *  Discord 👉  [http://dicasdomateus.com.br/d]()

Pré-requisitos:

* Ter um Pendrive USB, de preferencia 3.0, para criação da Imagem  de Instalação

Ferramentas para Download:

* OCAuxiliaryTools 👉 👉 [https://github.com/ic005k/QtOpenCoreConfig]()
* Aida64 Download 👉 👉 [https://www.aida64.com/]()
* Rufus 👉 👉 [https://rufus.ie]()


## 1) Definir Hardware:
Gerar report de Hardware do Aida64 e Definir:

* Processador:
* Chipset Placa Mãe:
* Placa de Vídeo #1:
* Placa de Vídeo  #2:
* Placa de Rede:

Extra: Vídeo detalhado de como instalar e usar o Aida64 [https://youtu.be/9v3U72dPZTo
]()

## 2) Verificar Placa de Vídeo
 Verificar se sua placa de Vídeo Externa (eGPU) é compatível com Hackintosh conforme lista abaixo. Caso voce só tenha iGPU ignorar essa parte.
 
<details>
<summary>Lista de Placas de Video Compativel com Hackintosh</summary>

| Sistema       | Placa de Video                                                                                                                                                                                                                                                                                                                                                                                 | Extra                                                                                                                                                         |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Monterey      | RX 460, 470, 480, 550 (Baffin Core), 560, 570, 580,  590<br>RX 6600XT, RX 6800 (XT), RX 6900 XT<br>RX 5500 (XT), RX 5600 (XT) , RX 5700 (XT)<br>VEGA 64, VEGA 56<br>R7/R9 240, 250, 250x, 260(X)/360(X), 265, 270(X)/370(X), 280(X)/380(X), 290(X)/380(X), Não, Fury (X)<br>HD 8740, 8760, 8770, 8850, 8870, 8890, 8950, 8970<br>HD 7700, 7730, 7750, 7770, 7790, 7850, 7870, 7950, 7970, 7990 | RX 6600Xt  Suportada no Monterey 12.1<br>RX 6800 e 6900 Suportada no Big Sur 11.4                                                                             |
| Big Sur       | GTX Titan, 780 (Ti), 770, 760 (Ti)<br>GT 740 (GK107), 730 (GK208), 720, 710(GK208)<br>GTX 690, 680, 660 Ti, 660 (GK104) 650 (GK107)<br>GT 640 (GK107/GK208), 635, 630 (GK107/GK208)<br>Quadro K6000, K5200, K5000, K4200, K4200, K600, K420, 410<br>NVS 510                                                                                                                                    | Pode instalar o Monterey Aplicando Patch                                                                                                                      |
| High Sierra   | GTX Titan X, 1080 (Ti), 1070 (Ti), 1060 (GP104 Não Suportada), 1050 (Ti), 1030, 1010<br>GTX 980 (Ti), 970, 960, 950, 750 (Ti), 745                                                                                                                                                                                                                                                             | shikigva=40 boot arg: Altere Smios para IMac14,2 para melhor suporte ao Nvidia Web Drivers<br>nvda\_drv\_vrl=1 para ativar os Drivers da Placa de Video Nvida |
| Não Suportada | Nvidia Serie 3000, 2000, 1600<br>GTX 660, 650 Ti, 650, 645 Todas GK106 Variants<br>GT 730, 720A, 710, 705, 640, 630, 620, 610 Todas GF108, GF117 ou GF119                                                                                                                                                                                                                                      |                                                                                                                                                               |

</details>

Extra: Placas de Videos Compativeis com MacOS Monterey [https://youtu.be/Z_1Il-jQuq8](https://youtu.be/Z_1Il-jQuq8)

## 3) Definir Template OC Auxiliary Tools

Verificar qual template do OC Auxiliary Tool sera utilizado para gerar a EFI, de acordo com a lista abaixo. Considerar as informações levantadas no Item 1 e 2. Caso tenha eGPU considerar a versão do MacOS que sua eGPU suporta para selecionar o template.

<details>
<summary>Lista de Templates OCAT</summary>



| Geração   | Config                                                   | Vídeo Integrado | Vídeo Externo | Versão Mínimo    | Versão Máximo | Extra                                                                                                                                                                                                        |
| --------- | -------------------------------------------------------- | --------------- | ------------- | ---------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 01 Gen    | Desktop\_01stGen\_Clarkdale\_iMac11,2.plist              | Não Suportado   | Sim           | Lion             | High Sierra   |                                                                                                                                                                                                              |
| 01 Gen    | Desktop\_01stGen\_Lynnfield\_Clarkdale\_MacPro6,1.plist  | Não Suportado   | Sim           | Leopard          | Monterey      | Para instalar Mojave ou Superior, Desabilitar igpu na bios ou adicionar o atributo -wegnoigpu no boot args                                                                                                   |
| 01 Gen    | Desktop\_01stGen\_Lynnfield\_iMac11,1.plist              | Não Suportado   | Sim           | Lion             | High Sierra   |                                                                                                                                                                                                              |
| 02 Gen    | Desktop\_02ndGen\_Sandy\_Bridge\_iMac12,2.plist          | Sim             | Não           | Lion             | High Sierra   | Para Vídeo Integrado Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 0A006601<br>Manter Device-id = 26010000<br>                                                               |
| 02 Gen    | Desktop\_02ndGen\_Sandy\_Bridge\_iMac12,2.plist          | Sim             | SIM           | Lion             | High Sierra   | Para Vídeo Integrado + Vídeo Externo Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 00000500<br>Manter Device-id = 02010000                                                   |
| 03 Gen    | Desktop\_03rdGen\_Ivy\_Bridge\_MacPro6,1.plist           | Não             | Sim           | Leopard          | Monterey      | Para instalar Mojave ou Superior, Desabilitar igpu na bios ou adicionar o atributo -wegnoigpu no boot args                                                                                                   |
| 03 Gen    | Desktop\_03rdGen\_Ivy\_Bridge\_iMac13,1.plist            | Sim             | Não           | Mavericks        | Catalina      | Para Vídeo Integrado Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 0A006601                                                                                                  |
| 03 Gen    | Desktop\_03rdGen\_Ivy\_Bridge\_iMac13,2.plist            | Sim             | Sim           | Mavericks        | Catalina      | Para Vídeo Integrado + Vídeo Externo Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 07006201                                                                                  |
| 03 Gen    | Desktop\_03rdGen\_Ivy\_Bridge\_iMac14,4.plist            | Sim             | Não           | Yosemite         | Big Sur       | Para Vídeo Integrado Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 0A006601                                                                                                  |
| 03 Gen    | Desktop\_03rdGen\_Ivy\_Bridge\_iMac15,1.plist            | Sim             | Sim           | El Captain       | Big Sur       | Para Vídeo Integrado + Vídeo Externo Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 07006201                                                                                  |
| 04 Gen    | Desktop\_04thGen\_Haswell\_iMac14,4.plist                | Sim             | Não           | Yosemite         | Big Sur       | Para instalar o Monterey alterar o SMBIOS para iMac16,2                                                                                                                                                      |
| 04 Gen    | Desktop\_04thGen\_Haswell\_iMac15,1.plist                | Sim             | Sim           | El Captain       | Big Sur       | Para instalar o Monterey alterar o SMBIOS para iMac17,1                                                                                                                                                      |
| 05 Gen    | Desktop\_05thGen\_Broadwell\_iMac16,2.plist              | Sim             | Não           | Sierra           | Monterey      | Para Vídeo Integrado Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 07002216                                                                                                  |
| 05 Gen    | Desktop\_05thGen\_Broadwell\_iMac17,1.plist              | Sim             | Sim           | Sierra           | Monterey      | Para Vídeo Integrado + Vídeo Externo Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 07006201                                                                                  |
| 06 Gen    | Desktop\_06thGen\_Skylake\_iMac17,1.plist                | Sim             | Não           | Sierra           | Monterey      | Para Vídeo Integrado Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 00001219                                                                                                  |
| 06 Gen    | Desktop\_06thGen\_Skylake\_iMac17,1.plist                | Sim             | Sim           | Sierra           | Monterey      | Para Vídeo Integrado + Vídeo Externo Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 01001219                                                                                  |
| 07 Gen    | Desktop\_07thGen\_Kaby\_Lake\_iMac18,1.plist             | Sim             | Não           | High Sierra      | Monterey      | Para Vídeo Integrado Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 00001259                                                                                                  |
| 07 Gen    | Desktop\_07thGen\_Kaby\_Lake\_iMac18,3.plist             | Sim             | Sim           | High Sierra      | Monterey      | Para Vídeo Integrado + Vídeo Externo Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 03001259                                                                                  |
| 08/09 Gen | Desktop\_08th-9thGen\_Coffee\_Lake\_iMac18,1.plist       | Sim             | Não           | High Sierra      | Monterey      | Para Vídeo Integrado Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 07009B3E                                                                                                  |
| 08/09 Gen | Desktop\_08th-9thGen\_Coffee\_Lake\_iMac18,3.plist       | Sim             | Sim           | High Sierra      | Monterey      | Preferencial para instalar com Placa de Vídeo Nvidia Suportado no High Sierra<br>Para Vídeo Integrado + Vídeo Externo Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 0300913E |
| 08/09 Gen | Desktop\_08th-9thGen\_Coffee\_Lake\_iMac19,1.plist       | Sim             | Não           | Catalina         | Monterey      | Para Vídeo Integrado Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 07009B3E                                                                                                  |
| 08/09 Gen | Desktop\_08th-9thGen\_Coffee\_Lake\_iMac19,1.plist       | Sim             | Sim           | Catalina         | Monterey      | Para Vídeo Integrado + Vídeo Externo Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 0300913E                                                                                  |
| 08/09 Gen | Desktop\_08th-9thGen\_Coffee\_Lake\_iMac19,1.plist       | Não             | Sim           | Catalina         | Monterey      | Para processador F, Apagar todos DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) e Alterar SMBIOS para iMacPro1,1                                                                                              |
| 08/09 Gen | Desktop\_08th-9thGen\_Coffee\_Lake\_iMac19,1\_Z390.plist |                 |               | Catalina         | Monterey      | Mesma Regra do IMac19,1 mas para quem usa Placa Mãe Z390                                                                                                                                                     |
| 08/09 Gen | Desktop\_08th-9thGen\_Coffee\_Lake\_iMac19,2.plist       |                 |               | Catalina         | Monterey      | Mesma Regra do IMac19,1                                                                                                                                                                                      |
| 08/09 Gen | Desktop\_08th-9thGen\_Coffee\_Lake\_iMac19,2\_Z390.plist |                 |               | Catalina         | Monterey      | Mesma Regra do IMac19,1 mas para quem usa Placa Mãe Z390                                                                                                                                                     |
| 10 Gen    | Desktop\_10thGen\_Comet\_Lake\_iMac20,1.plist            | Sim             | Não           | Catalina 10.15.6 | Monterey      | Para Vídeo Integrado Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 07009B3E                                                                                                  |
| 10 Gen    | Desktop\_10thGen\_Comet\_Lake\_iMac20,1.plist            | Sim             | Sim           | Catalina 10.15.6 | Monterey      | Para Vídeo Integrado + Vídeo Externo Manter DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id = 0300C89B                                                                                  |
| 10 Gen    | Desktop\_10thGen\_Comet\_Lake\_iMac20,1.plist            | Não             | Sim           | Catalina 10.15.6 | Monterey      | Para processador F, Apagar todos DeviceProperties -> PciRoot(0x0)/Pci(0x2,0x0) e Alterar SMBIOS para iMacPro1,1                                                                                              |
| 10 Gen    | Desktop\_10thGen\_Comet\_Lake\_iMac20,2.plist            |                 |               | Catalina 10.15.6 | Monterey      | Mesma Regra do IMac20,1 para processadores i9 de 10th                                                                                                                                                        |
| 11 Gen    | Desktop\_11thGen\_Rocket\_Lake\_MacPro7,1.plist          | Não Suportado   | Sim           | Catalina 10.15.6 | Monterey      |                                                                                                                                                                                                              |
| 11 Gen    | Desktop\_11thGen\_Rocket\_Lake\_iMacPro1,1.plist         | Não Suportado   | Sim           | Mojave           | Monterey      |                                                                                                                                                                                                              |

</details>

Alternativo, Lista de Templates OCAT em formato Excel 👉  [https://bit.ly/ocatexcel](https://bit.ly/ocatexcel)


## 4) Gerando a EFI
Executar o OCAT e gerar a EFI de acordo com o template selecionado no Item 3.

### 4.1) Criando EFI
Abrir o OCAT, clicar em Database, selecionar o Template e clicar duas vezes sobre ele para gerar.

### 4.2) Device Properties
Clicar em DP, e ajustar o Device Properties conforme regras abaixo:

* Para processadores F ou SMBIOS MacPro6,1, MacPro7,1 ou iMacPro1,1: Limpar todos os itens no Device Properties. 
* Para processadores com video integrado e com ou sem placa de video externa manter o Device Properties de acordo com a regra definida na coluna extra do item 3. Limpar os itens não necessario

			
### 4.3) Kernel
Adcionar kexts adcionais de USB e Placa de Rede

* USB
	* Adcionar as Kext USBInjectAll.kext
	* Se pendrive de Boot 3.0, setar Kernel -> Quirks -> XhciPortLimit = True
* Placa de Rede
	* Adcionar Kext conforme lista abaixo:

| Kext                      | Description                                                                                                                                                            |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| IntelMausi.kext           | Intel's 82578, 82579, I217, I218 and I219 NICs are officially supported.                                                                                               |
| AtherosE2200Ethernet.kext | Required for Atheros and Killer NICs.<br>Note: Atheros Killer E2500 models are actually Realtek based, for these systems please use RealtekRTL8111 instead.            |
| RealtekRTL8111.kext       | For Realtek's Gigabit Ethernet.<br>Sometimes the latest version of the kext might not work properly with your Ethernet. If you see this issue, try older versions.<br> |
| LucyRTL8125Ethernet.kext  | For Realtek's 2.5Gb Ethernet.                                                                                                                                          |
| SmallTreeIntel82576.kext  | Required for I211 NICs, based off of the SmallTree kext but patched to support I211.<br>Required for most AMD boards running Intel NICs.                               |



* Outras Kext Opcionais
	* Só adicione se necessário[]()
	
| Kext                     | Description                                                                                                                                                                     |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NVMeFix                  | Used for fixing power management and initialization on non-Apple NVMe.                                                                                                          |
| SATA-Unsupported         | Adds support for a large variety of SATA controllers, mainly relevant for laptops which have issues seeing the SATA drive in macOS.<br>We recommend testing without this first. |
| AppleMCEReporterDisabler | Useful starting with Catalina to disable the AppleMCEReporter kext which will cause kernel panics on AMD CPUs.<br>Recommended for dual-socket systems (ie. Intel Xeon).         |
| RestrictEvents           | Better experience with unsupported processors like AMD, Disable MacPro7,1 memory warnings and provide upgrade to macOS Monterey via Software Updates when available.            |

### 4.3) Boot Args
Em Nvram -> Add -> 7C436110-AB2A-4BBB-A880-FE41995C9F82 -> boot-args, adcionar parametros opcionais conforme lista abaixo:

* Especificos para GPU

| Boot-arg       | Description                                                                                                                                                                                                                                        |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| agdpmod=pikera | Disables Board-ID checks on AMD Navi GPUs (RX 5000 & 6000 series). Without this you'll get a black screen. Don't use on Navi Cards (i.e. Polaris and Vega).                                                                                        |
| \-igfxvesa     | Disables graphics acceleration in favor of software rendering. Useful if iGPU and dGPU are incompatible or if you are using an NVIDIA GeForce Card and the WebDrivers are outdated after updating macOS, so the display won't turn on during boot. |
| \-wegnoegpu    | Disables all GPUs but the integrated graphics on Intel CPU. Use if GPU is incompatible with macOS. Doesn't work all the time.                                                                                                                      |
| \-wegnoigpu    | to disable internal GPU                                                                                                                                                                                                                            |
| nvda\_drv=1    | Enable Web Drivers for NVIDIA Graphics Cards (supported up to macOS High Sierra only).                                                                                                                                                             |
| nv\_disable=1  | Disables NVIDIA GPUs (don't combine this with nvda\_drv=1)                                                                                                                                                                                         |

* Especificos para Debug

| Boot-arg                | Description                                                                                                                                                                                                                                                                                              |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \-v                     | \_V\_erbose Mode. Replaces the progress bar with a terminal output with a bootlog which helps resolving issues. Combine with debug=0x100 and keepsyms=1                                                                                                                                                  |
| debug=0x100             | Disables macOS'es watchdog. Prevents the machine from restarting on a kernel panic. That way you can hopefully glean some useful info and follow the breadcrumbs to get past the issues.                                                                                                                 |
| keepsyms=1              | Companion setting to debug=0x100 that tells the OS to also print the symbols on a kernel panic. That can give some more helpful insight as to what's causing the panic itself.                                                                                                                           |
| dart=0                  | Disables VT-x/VT-d. Nowadays, DisableIOMapper Quirk is used instead.                                                                                                                                                                                                                                     |
| cpus=1                  | Limits the number of CPU cores to 1. Helpful in cases where macOS won't boot or install otherwise.                                                                                                                                                                                                       |
| npci=0x2000/npci=0x3000 | Disables PCI debugging related to kIOPCIConfiguratorPFM64. Alternatively, use npci=0x3000 which also disables debugging of gIOPCITunnelledKey. Required when stuck at PCI Start Configuration as there are IRQ conflicts related to your PCI lanes. Not needed if Above4GDecoding can be enabled in BIOS |
| \-no\_compat\_check     | Disables macOS compatibility check. For example, macOS 11.0 BigSur no longer supports iMac models introduced before 2014. Enabling this allows installing andd booting macOS on otherwise unsupported SMBIOS. Downside: you can't install system updates if this is enabled.                             |

* Especificos para Audio

| Boot-arg | Description                                                                                                                                                                                       |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| alcid=1  | Used for setting layout-id for AppleALC, see supported codecs (opens new window)to figure out which layout to use for your specific system. More info on this is covered in the Post-Install Page |


### 4.4) Gerando Serial
Em Plataform Info, clicar em Generate ao lado do campo SytemProductName e ROM

### 4.5) Gravar EFI
Salvar todos os ajustes feitos na EFI para adicionar no Pendrive de Boot

## 5) Criar Pendrive de Boot:
Apos definir a versão a ser instalada, no link abaixo e fazer download da Imagem do MacOS a ser instalado:

* Download ISO From Olarila 👉 👉 [https://www.olarila.com/topic/6278-olarila-vanilla-images/](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html#making-the-installer-in-windows)

Links alternativos para Baixar o Big Sur 11.2

* ISO Big Sur 11.2 👉 👉 [https://bit.ly/ISOBigSur]() 
* ISO Big Sur 11.2 👉 👉 [https://bit.ly/ISOBIGSUR2]() 
* ISO Big Sur 11.2 👉 👉 [https://bit.ly/ISOBigSUR3]()

Apos baixar a imagem, usar o Rufus para gravar ela pendrive de boot.

Alternativo: Método oficial do Opencore para Criar Pendrive de Boot Direto da Apple no Windows [Aqui
](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html#making-the-installer-in-windows)
## 6) Copiando EFI para Pendrive:
Abrir o OCAT, clicar em MountESP, selecionar o pendrive na lista de disco disponiveis e clicar em Mount.

Apos abrir a partição EFI, delete todo o conteudo da partição e copie a pasta EFI gerada no passo 4 para ela.


## 7) Pre-Install Ajuste de Bios:
* Disable
	* Fast Boot
	* Secure Boot
	* Serial/COM Port
	* Parallel Port
	* VT-d 
	* CSM
	* Intel SGX
	* Intel Platform Trust
	* CFG Lock 
	* Thunderbolt (For initial setup)
* Enable
	* VT-x
	* Above 4G decoding
		* 2020+ BIOS Notes: When enabling Above4G, Resizable BAR Support may become an available on some Z490 and newer motherboards. Please ensure this is Disabled instead of set to Auto.
	* Hyper-Threading
	* Execute Disable Bit
	* EHCI/XHCI Hand-off
	* OS type: Windows 8.1/10 UEFI Mode
	* DVMT Pre-Allocated(iGPU Memory):  
		* 32MB Até Ivy Bridge (03Gen) rodando Catalina, 
		* 64MB para Ivy Bridge com Big Sur, Haswell ou Superior.  
	* SATA Mode: AHCI

Extra: Exemplo Ajuste de Bios 👉 [Bios 01](https://youtu.be/FOrov-ur4qA) [Bios 02](https://youtu.be/EUolzdvEpDA)

## 8) Instalar Mac OS:
Fazer boot pelo pendrive, no menu do Opencore, selecionar Install Mac Os [Nome da versão que escolher], e ir até o final.

* Caso tenha problema com video integrado, colocar o atributo -igfxvesa e tentar novamente
* Caso apareça mensagem de proibido, apos selecionar imagem para instalar, trocar pendrive de porta, escolhendo uma 2.0/3.0 na traseira da maquina.

Extra: Como instalar MacOS [Big Sur](https://youtu.be/i7F7WtXXbhs) e [Monterey](https://youtu.be/b6g-W4gyQm0)

## 9) Post Install:
* Copiar a pasta EFI para a partição EFI do disco que foi instalado o MacOS, para dar boot sem pendrive.

* Mapeament de USBs:
	* Como Mapear Portas USBs até big sur 11.2 👉 👉 [https://youtu.be/X6djBycrcx4 ](https://youtu.be/b6g-W4gyQm0)
	* Como Mapear Portas USBs acima big sur 11.3 👉 👉 [https://youtu.be/4z76yO5_2aU](https://youtu.be/b6g-W4gyQm0)
* Ajustando Audio HDMI e Mapeando Conectores 👉 👉 [https://youtu.be/NIoPq2w8q18](https://youtu.be/NIoPq2w8q18)


## 10) Referencias:

* Opencore Install Guide 👉 [https://dortania.github.io/OpenCore-Install-Guide/](https://dortania.github.io/OpenCore-Install-Guide/)
* Olarila - The Real Vanilla Hackintosh 👉 [https://www.olarila.com/](https://www.olarila.com/)
* OC Auxiliary Tools (OCAT) 👉 [https://github.com/ic005k/QtOpenCoreConfig](https://github.com/ic005k/QtOpenCoreConfig)
* OC-Little-Translated 👉 [https://github.com/5T33Z0/OC-Little-Translated](https://github.com/5T33Z0/OC-Little-Translated)
* WhateverGreen 👉 [https://github.com/acidanthera/WhateverGreen](https://github.com/acidanthera/WhateverGreen)

## 11) Agradencimentos:

* Dortania, Maldon, @ic005k (OCAT Team), @5T33Z0 (OCAT Templates)  
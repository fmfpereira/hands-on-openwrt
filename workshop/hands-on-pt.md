# Hands-on OpenWrt

## Selecionar o Firmware

https://firmware-selector.openwrt.org/

<details>
<summary>Exemplos</summary>

![[01_firmware-selector.jpg]]{width=60%}

![[02_firmware-selector-customize.jpg]]{width=60%}

![[03_firmware-selector-build-download.jpg]]{width=60%}

</details>

### Acesso ao Router

- Ligue-se à rede sem fios descrita no seu equipamento.
	- A palavra-passe é **12345678**.
- Aceda a http://192.168.20.1 e faça login.
	- Não introduza uma palavra-passe.
- O aviso para alterar a palavra-passe irá surgir.
	- Selecione a opção e altere a palavra-passe.
	- Ex: **12345**

<details>
<summary>Exemplos</summary>

![[05_openwrt-first-screen.jpg]]{width=60%}

![[06_openwrt-password-change.jpg]]{width=60%}

![[07_openwrt-status-menu.jpg]]{width=60%}

![[08_openwrt-system-menu.jpg]]{width=60%}

</details>

### Menus e Funcionalidades

- Navegue nos menus e explore as funcionalidades.

<details>
<summary>Exemplos</summary>

![[07_openwrt-status-menu.jpg]]

![[08_openwrt-system-menu.jpg]]

![[09_openwrt-network-menu.jpg]]

</details>

### Configuração da Interface Local

- Selecione "**Network**" e "**Interfaces**".
- Se no seu dispositivo aparecer a interface **wan**, pode avançar o próximo passo.
	- O Raspberry Pi 2 Zero W não tem placa de rede incorporada. Neste caso, iremos usar o telemóvel Android como interface **wan**.

#### Adicionar Interface WAN

- Ligue o seu telemóvel Android via USB à placa OTG.
- No telemóvel deverá aparecer a opção de que está ligado por USB.
	- Ative a opção 'USB tethering' ou 'Ancoragem USB'.
- Selecione o separador "**Devices**" no OpenWrt. Deverá aparecer um novo dispositivo, **usb0**.
- Volte ao separador "**Interfaces**" e selecione a opção "**Add new interface**".
	- Nome: **wan**
	- Protocolo: **DHCP Client**
	- Dispositivo: **usb0**
- No separador "**Firewall settings**", selecione a zona **wan**.
- Selecione o botão "**Save & Apply**".
- Se tudo correr como esperado, a interface **wan** deverá ter um IP, e deverá conseguir aceder à internet do seu computador.

<details>
<summary>Exemplos</summary>

![[10_openwrt-interfaces-page.jpg]]{width=60%}

![[11_openwrt-interfaces-page-devices.jpg]]{width=60%}

![[16_openwrt-interface-page-devices.jpg]]{width=60%}

![[17_openwrt-interface-page-add-new-interface.jpg]]{width=60%}

![[18_openwrt-interface-page-add-new-interface-general.jpg]]{width=60%}

![[19_openwrt-interface-page-add-new-interface-firewall.jpg]]{width=60%}

![[19_openwrt-interface-page-add-new-interface-firewall.jpg]]{width=60%}

![[20_openwrt-interface-page-add-new-interface-apply.jpg]]{width=60%}

![[21_openwrt-interface-page-add-new-interface-up.jpg]]{width=60%}

</details>

### Configuração da Rede sem Fios

- Selecione "**Network**" e "**Wireless**".
- Edite a rede sem fios e verifique as configurações.
	- Ex. Aqui é possível alterar o nome da rede sem fios e a palavra-passe.
- Nota: É possível adicionar múltiplas redes sem fios para diferentes fins. Infelizmente, nos Raspberry Pi, a placa de rede não suporta essa funcionalidade.

<details>
<summary>Exemplos</summary>

![[12_openwrt-wireless-page.jpg]]{width=60%}

![[13_openwrt-wireless-network-page.jpg]]{width=60%}

![[14_openwrt-wireless-network-page-general-setup.jpg]]{width=60%}

![[15_openwrt-wireless-network-page-wireless-security.jpg]]{width=60%}

</details>

### Firewall

- Navegue até "**Network**" e "**Firewall**".
- Verifique se a zona **lan** está a fazer *forward* para a zona **wan**.

<details>
<summary>Exemplos</summary>

![[22_openwrt-firewall-page.jpg]]{width=60%}

</details>

### Software

- Navegue até "**System**" e "**Software**".
- Atualize a lista e valide se o pacote **wireguard** está instalado.
- Pesquise a lista de pacotes e explore alguns que possa instalar no OpenWrt.

<details>
<summary>Exemplos</summary>

![[23_openwrt-software-page.jpg]]{width=60%}

</details>

### Configuração de uma VPN com o WireGuard

- Selecione "**Network**" e "**Interfaces**".
- Selecione "**Add new interface**" e confirme.
	- Nome: **wireguard**
	- Protocolo: **WireGuard VPN**
- Selecione "**Load configuration**".
	- Importe o conteúdo do ficheiro de configuração do WireGuard para o seu router, que foi distribuído numa pen.
- Selecione "Importar".
- Selecione o separador "**Firewall Settings**" e crie uma nova zona com o nome **wireguard** (tem que confirmar com a tecla Enter).
- Selecione o separador "**Peers**" e edite o Peer importado.
- Selecione a opção "**Route Allowed IPs**" e grave.
- Selecione no menu a opção "**Network**" e "**Firewall**".
- Edite a interface **lan**.
- Remova **wan** da seleção e selecione **wireguard** e grave.
- Na listagem de zonas, confirme as seguintes opções para a zona **wireguard**:
	- Input: **accept**
	- Output: **accept**
	- Intra zone forward: **reject**
	- Masquerading: **selecionado**
- Selecione "**Save & Apply**".
- Selecione o separador **Interfaces**.
- Valide que a interface **wireguard** está a receber e a transmitir dados.
- Abra o browser e pesquise por 'What is my IP?'.
- Valide que o seu IP tem origem no país da **VPN**.

<details>
<summary>Exemplos</summary>

![[23_openwrt-software-page.jpg]]{width=60%}

![[24_openwrt-interface-page-add-wireguard-interface.jpg]]{width=60%}

![[25_openwrt-interface-page-add-wireguard-interface-load.jpg]]{width=60%}

![[26_openwrt-interface-page-add-wireguard-interface-import.jpg]]{width=60%}

![[27_openwrt-interface-page-add-wireguard-interface-import-finish.jpg]]{width=60%}

![[28_openwrt-interface-page-add-wireguard-interface-firewall.jpg]]{width=60%}

![[29_openwrt-interface-page-add-wireguard-interface-firewall-create.jpg]]{width=60%}

![[30_openwrt-interface-page-add-wireguard-interface-peers.jpg]]{width=60%}

![[31_openwrt-interface-page-add-wireguard-interface-peer-routing.jpg]]{width=60%}

![[32_openwrt-firewall-page.jpg]]{width=60%}

![[33_openwrt-firewall-page-lan-forward.jpg]]{width=60%}

![[34_openwrt-firewall-page-wireguard-masquerade.jpg]]{width=60%}

</details>
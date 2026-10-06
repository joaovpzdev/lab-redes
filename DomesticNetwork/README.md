<div align="center">

# Home Lab: Rede Doméstica com Roteador Wi-Fi

**Cabeamento, roteador sem fio, DHCP, Wi-Fi com WPA2 e testes de conectividade**

![Cisco Networking Academy](https://img.shields.io/badge/Cisco-Networking%20Academy-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![Packet Tracer](https://img.shields.io/badge/Simulador-Packet%20Tracer-049fd9?style=for-the-badge)
![Tema](https://img.shields.io/badge/Tema-Redes%20Básicas-2ea44f?style=for-the-badge)
![Foco](https://img.shields.io/badge/Foco-Suporte%20N1-orange?style=for-the-badge)

</div>

---

## Sobre o lab

Laboratório prático do curso **Conceitos Básicos de Redes** (Cisco Networking Academy), feito no **Cisco Packet Tracer**.

**Cenário:** montar do zero a rede de uma casa nova. Isso inclui conectar os cabos ao serviço de TV a cabo e à internet, configurar o roteador sem fio, ativar uma rede Wi-Fi protegida e validar que todos os dispositivos chegam à internet.

>"o computador não tem internet", "o Wi-Fi não conecta", "o equipamento não pega IP".

---

## 🗺️ Topologia lógica

```mermaid
flowchart TB
    NET(["Internet<br/>servidor skillsforall.srv"])

    subgraph CASA["Casa da Natsumi"]
        direction TB
        SPL["📡 Cable Splitter<br/>separa vídeo e dados"]
        TV["📺 TV<br/>serviço de vídeo"]
        MODEM["📟 Cable Modem<br/>entrada de dados"]

        subgraph REDE["🛜 Rede local · DHCP · faixa 192.x.x.x"]
            direction TB
            RT{{"🔀 Home Wireless Router<br/>gateway padrão + servidor DHCP + AP Wi-Fi"}}
            OFFICE["🖥️ Office PC<br/>cabo · Gi1"]
            BEDROOM["🖥️ Bedroom PC<br/>cabo · Gi2"]
            LAPTOP["💻 Laptop da sala<br/>Wi-Fi 2,4 GHz · WPA2"]
        end
    end

    NET ==>|"cabo coaxial"| SPL
    SPL ==>|"coaxial"| TV
    SPL ==>|"coaxial"| MODEM
    MODEM -->|"Ethernet direto<br/>porta Internet"| RT
    RT ---|"Ethernet"| OFFICE
    RT ---|"Ethernet"| BEDROOM
    RT -.-|"Wi-Fi"| LAPTOP

    classDef cloud fill:#e0f2fe,stroke:#0284c7,color:#0c4a6e,stroke-width:2px;
    classDef carrier fill:#fef3c7,stroke:#d97706,color:#78350f,stroke-width:2px;
    classDef router fill:#dcfce7,stroke:#16a34a,color:#14532d,stroke-width:3px;
    classDef host fill:#ede9fe,stroke:#7c3aed,color:#3b0764,stroke-width:2px;
    classDef wifi fill:#fce7f3,stroke:#db2777,color:#831843,stroke-width:2px;

    class NET cloud;
    class SPL,TV,MODEM carrier;
    class RT router;
    class OFFICE,BEDROOM host;
    class LAPTOP wifi;
```

### Visão no simulador

![Topologia no Packet Tracer](img/topologia-packet-tracer.png)

---

## Dispositivos e conexões

| # | Origem | Porta | Destino | Porta | Cabo |
|---|--------|-------|---------|-------|------|
| 1 | Cable Splitter | Coaxial1 | Cable Modem | Port 0 | Coaxial |
| 2 | Cable Splitter | Coaxial2 | TV | Port 0 | Coaxial |
| 3 | Cable Modem | Port 1 | Home Wireless Router | Internet | Ethernet direto (straight-through) |
| 4 | Office PC | FastEthernet0 | Home Wireless Router | GigabitEthernet 1 | Ethernet direto |
| 5 | Bedroom PC | FastEthernet0 | Home Wireless Router | GigabitEthernet 2 | Ethernet direto |
| 6 | Laptop (sala) | Placa Wi-Fi | Home Wireless Router | Rede sem fio | Wi-Fi 2,4 GHz |

---

## Passo a passo resumido

### Parte 1 · Conectar os dispositivos 🔧
1. Ligar o serviço de TV a cabo ao **splitter**, que divide o sinal em dois caminhos: vídeo para a TV e dados para o modem.
2. Conectar o **cable modem** à porta *Internet* do roteador.
3. Ligar os dois PCs às portas Ethernet do roteador.
4. Teste: a TV exibe imagem ao ser ligada, o que confirma que o cabeamento coaxial está correto.

### Parte 2 · Configurar o roteador 🛠️
1. No Office PC, obter IP por **DHCP** e anotar o **gateway padrão**, que é o endereço do roteador.
2. Acessar a interface web do roteador pelo navegador, usando o endereço do gateway.
3. **Limitar o DHCP a 10 usuários**, porque a casa terá poucos dispositivos.
4. **Trocar a senha padrão de administrador** na aba *Administration*.
5. Ativar a rede **2,4 GHz**, renomear o **SSID** e proteger com **WPA2 Personal**.

### Parte 3 · Testar a conectividade ✅
1. Conectar o laptop ao Wi-Fi e conferir se ele recebeu IP.
2. Abrir `skillsforall.srv` no navegador do Office PC, do Bedroom PC e do laptop.
3. Se as três páginas carregarem, a rede com fio, o Wi-Fi, o DHCP e a saída para a internet estão funcionando.

---

## Como o DHCP entrega o IP (DORA)

```mermaid
sequenceDiagram
    autonumber
    participant C as 💻 Cliente (PC / Laptop)
    participant R as 🔀 Roteador (servidor DHCP)

    C->>R: DISCOVER · "Tem algum servidor DHCP aí?" (broadcast)
    R-->>C: OFFER · "Posso te oferecer este IP"
    C->>R: REQUEST · "Quero usar esse IP"
    R-->>C: ACK · "Confirmado, ele é seu por um tempo"
    Note over C,R: O cliente passa a ter IP, máscara, gateway e DNS
```

---

## Boas práticas de segurança aplicadas

| Prática | Por que importa |
|---|---|
| Trocar a senha padrão do roteador | Credenciais de fábrica são conhecidas e testadas por atacantes |
| Usar **WPA2 Personal** no Wi-Fi | Sem criptografia, qualquer pessoa por perto entra na rede |
| Escolher uma senha de Wi-Fi forte | A frase de acesso é a primeira barreira da rede sem fio |
| Limitar o pool de DHCP | Reduz o número de endereços disponíveis para dispositivos não previstos |

> **Nota:** as senhas usadas no exercício são valores de laboratório e foram omitidas aqui de propósito. Em ambiente real, use senhas únicas e nunca as publique em repositórios.

---

## Roteiro de diagnóstico (visão de suporte N1)

Quando o usuário disser **"estou sem internet"**, este é o raciocínio que o lab me ajudou a organizar:

```mermaid
flowchart TD
    A(["Usuário: estou sem internet"]) --> B{"Conexão física ou Wi-Fi<br/>está ativa?"}
    B -- "Não" --> B1["Verificar cabo, porta do roteador,<br/>Wi-Fi ligado e senha correta"]
    B -- "Sim" --> C{"O equipamento recebeu IP?<br/>ipconfig"}
    C -- "Não, IP 169.254.x.x" --> C1["Problema de DHCP:<br/>renovar IP, checar servidor DHCP"]
    C -- "Sim" --> D{"Responde ao gateway?<br/>ping gateway"}
    D -- "Não" --> D1["Problema na rede local:<br/>cabo, porta ou Wi-Fi"]
    D -- "Sim" --> E{"Alcança a internet?<br/>ping em IP externo"}
    E -- "Não" --> E1["Problema no roteador, modem<br/>ou no provedor: escalar"]
    E -- "Sim" --> F["Testar o site no navegador<br/>e verificar DNS"]

    classDef start fill:#dbeafe,stroke:#2563eb,color:#1e3a8a,stroke-width:2px;
    classDef fix fill:#fee2e2,stroke:#dc2626,color:#7f1d1d;
    classDef ok fill:#dcfce7,stroke:#16a34a,color:#14532d;
    class A start;
    class B1,C1,D1,E1 fix;
    class F ok;
```

### Comandos úteis para validar

```bash
ipconfig /all        # IP, máscara, gateway e servidor DHCP/DNS do equipamento
ipconfig /renew      # pede um novo IP ao servidor DHCP
ping <gateway>       # testa a comunicação com o roteador
ping <IP externo>    # testa a saída para fora da rede local
```

---


## Ferramentas

`Cisco Packet Tracer` · `Ethernet` · `Cabo coaxial` · `Wi-Fi 2,4 GHz` · `WPA2` · `DHCP` · `IPv4`

---

## Autor

**João Victor Paixão Zolim**
 [LinkedIn](https://www.linkedin.com/in/joao-victor-paixao-zolim) · [GitHub](https://github.com/joaovpzdev)

> Laboratório realizado para fins educacionais, no curso Conceitos Básicos de Redes da Cisco Networking Academy.

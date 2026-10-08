<div align="center">

# Lab Redes

**Laboratórios práticos de redes e segurança de redes no Cisco Packet Tracer**

![Cisco Networking Academy](https://img.shields.io/badge/Cisco-Networking%20Academy-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![Packet Tracer](https://img.shields.io/badge/Simulador-Packet%20Tracer-049fd9?style=for-the-badge)
![Tema](https://img.shields.io/badge/Tema-Redes%20e%20Segurança-2ea44f?style=for-the-badge)

</div>

---

## Sobre o repositório

Este repositório reúne laboratórios que fiz durante os cursos da **Cisco Networking Academy**. Cada lab simula um cenário real no **Cisco Packet Tracer** e é documentado como um relatório técnico: topologia, endereçamento, configurações, testes, problemas encontrados e lições aprendidas.

Os labs seguem uma progressão: começam com uma rede doméstica simples e avançam até a rede de uma empresa protegida em várias camadas.

## O que você encontra aqui

| Pasta | Lab | Nível | Principais temas |
| --- | --- | --- | --- |
| [DomesticNetwork](DomesticNetwork/README.md) | Rede doméstica com roteador Wi-Fi | Básico | Cabeamento, roteador sem fio, DHCP, Wi-Fi WPA2, diagnóstico de suporte N1 |
| [DefenseNetwork](DefenseNetwork/README.md) | Defesa em profundidade em uma pequena empresa | Intermediário | VLANs, roteamento entre VLANs, ACL estendida, port security |
| [NetworkDefenseLabs](NetworkDefenseLabs/) | Série de 7 labs de defesa de redes | Intermediário a avançado | Hardening, SSH, segurança de switches, ACLs, AAA, firewall, VPN |

### Série Network Defense Labs

Série em andamento que constrói, lab por lab, a rede de uma empresa com matriz, filial e acesso à internet. Cada lab adiciona uma camada de defesa.

| Lab | Tema | Status |
| --- | --- | --- |
| [Lab 1](NetworkDefenseLabs/Lab01-AcessoSeguro/README.md) | Montagem da topologia e acesso seguro (senhas, SSH, proteção contra força bruta) | ✅ Concluído |
| Lab 2 | VLANs, trunks e roteamento entre VLANs | ⏳ Próximo |
| Lab 3 | Segurança de switches (port security, DHCP snooping, BPDU Guard) | ⏳ |
| Lab 4 | Listas de controle de acesso (ACLs) | ⏳ |
| Lab 5 | AAA, Syslog e NTP | ⏳ |
| Lab 6 | Firewall baseado em zonas (ZBF) | ⏳ |
| Lab 7 | VPN IPsec site a site | ⏳ |

## Como cada lab está organizado

Cada pasta tem um `README.md` com o relatório completo e uma pasta `img/` com as capturas de tela. Em geral, os relatórios trazem:

- **Cenário e objetivo** do lab
- **Topologia** e tabela de endereçamento
- **Configuração passo a passo**, com os comandos explicados
- **Verificação**, com os testes e seus resultados
- **Problemas encontrados e soluções**, com os erros reais que aconteceram durante o lab
- **Lições aprendidas** e próximos passos

## Como reproduzir

1. Instale o [Cisco Packet Tracer](https://www.netacad.com/cisco-packet-tracer) (gratuito com uma conta da Networking Academy).
2. Escolha um lab e siga o README dele: a topologia, o endereçamento e os comandos estão todos documentados.
3. Compare seus resultados com as capturas de tela da pasta `img/`.

> As senhas mostradas nas configurações são apenas de laboratório, ou foram substituídas por `<...>`. Nunca reutilize senhas de lab em equipamentos reais.

## Ferramentas

`Cisco Packet Tracer` · `Cisco IOS` · `Ethernet` · `Wi-Fi` · `VLAN` · `ACL` · `SSH` · `DHCP` · `NAT` · `IPsec`

---

## Autor

**João Victor Paixão Zolim**
[LinkedIn](https://www.linkedin.com/in/joao-victor-paixao-zolim) · [GitHub](https://github.com/joaovpzdev)


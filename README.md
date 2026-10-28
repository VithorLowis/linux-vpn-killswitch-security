# Linux VPN Kill Switch — Network Security

**Projeto de laboratório | Linux | Network Security | nftables | WireGuard | systemd**

[Português](#português) · [English](#english)

---

## Português

### 1. Objetivo

Implementar e validar, em um laboratório Linux próprio, um mecanismo de
proteção de tráfego de saída destinado a reduzir o risco de conexões
diretas pela interface física quando uma VPN está em uso.

### 2. Tecnologias

- Kali Linux
- nftables
- WireGuard
- NetworkManager
- systemd
- Git e GitHub CLI

### 3. Arquitetura

A solução combina:

- Regras de filtragem de tráfego de saída.
- Exceções limitadas para o estabelecimento do túnel e serviços
  essenciais de rede.
- Bloqueio de tráfego pela interface física não autorizado.
- Persistência das regras por meio de um serviço systemd.
- Dependência de inicialização entre o serviço de proteção e o
  NetworkManager.
- Verificação de rotas, conectividade e estado do túnel.

Os detalhes específicos da infraestrutura foram omitidos
intencionalmente.

### 4. Metodologia de validação

Os testes foram executados no próprio laboratório, sem atingir
sistemas de terceiros.

| Teste | Resultado observado |
|---|---|
| Validação sintática das regras | Aprovada |
| Reinicialização do serviço | Serviço permaneceu ativo |
| Reinicialização do sistema | Serviço e regras presentes após o boot |
| Roteamento IPv4 e IPv6 | Rotas observadas pelo túnel VPN |
| Conectividade pública IPv4/IPv6 | Funcionou após o boot |
| Tentativa de conexão direta IPv4 | Timeout; contador de bloqueio aumentou |
| Tentativa de conexão direta IPv6 | Timeout; contador de bloqueio aumentou |
| Consulta DNS direta de teste | Timeout |
| DNS configurado | Servidores associados à conexão VPN |

**Interpretação:** os resultados são consistentes com o bloqueio do
tráfego direto testado. Um timeout isolado não prova, por si só, que
todo o tráfego foi bloqueado. A validação não constitui garantia de
ausência absoluta de vazamentos.

### 5. Decisões de segurança

- Separar a documentação dos arquivos reais do sistema.
- Não armazenar credenciais ou tokens no repositório.
- Não publicar chaves privadas, configurações WireGuard ou logs brutos.
- Manter o repositório privado durante a revisão.
- Verificar os arquivos antes de cada publicação.
- Documentar limitações e não declarar garantias não demonstradas.

### 6. Limitações e trabalho futuro

- Capturar tráfego durante a inicialização para investigar possíveis
  vazamentos transitórios.
- Testar cenários de queda e reconexão da VPN com procedimento de
  recuperação controlado.
- Verificar o comportamento diante de mudanças de interface e rota.
- Avaliar DNS com captura de pacotes e análise independente.
- Revisar as dependências do systemd e os cenários de falha.
- Repetir os testes após atualizações relevantes do sistema.

### 7. Escopo ético

Projeto de laboratório próprio para aprendizado e demonstração de
controles defensivos. Nenhum teste foi direcionado a sistemas de
terceiros.

---

## English

### Overview

This project documents a Linux VPN kill switch laboratory using
nftables, WireGuard, NetworkManager, and systemd.

The goal is to reduce the risk of outbound traffic bypassing the VPN
tunnel and to validate the behavior of the configured controls.

### Validation summary

- Firewall rules passed syntax validation.
- The service and rules were present after a system reboot.
- IPv4 and IPv6 routes were observed through the VPN interface.
- Direct connection attempts and a direct DNS test timed out.
- Firewall counters increased during direct connection attempts.

These observations support the expected filtering behavior but do not
prove the absence of every possible leak, especially during early boot.

### Limitations

Further packet-capture testing, controlled VPN-failure testing, DNS
analysis, and review of systemd failure scenarios remain necessary.

This is a defensive laboratory project. Infrastructure-specific
identifiers, addresses, credentials, private keys, and raw system
configuration are intentionally excluded.

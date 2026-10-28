# Plano de Testes — VPN Kill Switch

## Português

### Escopo

Testes autorizados exclusivamente no laboratório Linux do proprietário.

### Observações concluídas

- A validação sintática das regras nftables foi concluída com sucesso.
- O serviço Kill Switch estava ativo após a reinicialização do sistema.
- A tabela do firewall estava presente após a inicialização.
- As rotas IPv4 e IPv6 observadas utilizavam a interface da VPN.
- As tentativas de conexão direta IPv4 e IPv6 expiraram por timeout.
- Os contadores de descarte do firewall aumentaram durante as tentativas
  de conexão direta.
- Uma consulta DNS direta de teste expirou por timeout.

Esses resultados são observações do laboratório. Timeouts isolados não
comprovam, por si só, que todas as conexões foram bloqueadas.

### Testes pendentes

- Capturar pacotes durante a inicialização e a reconexão da VPN.
- Testar falha e recuperação da VPN em uma janela de manutenção controlada.
- Verificar o comportamento do DNS por meio de captura de pacotes.
- Revisar IPv6, mudanças de interface e cenários alternativos de roteamento.
- Revisar as dependências do systemd e o comportamento em cenários de falha.

### Tratamento de evidências

Não armazenar saídas brutas de comandos, endereços IP reais, chaves
privadas, tokens, detalhes do endpoint VPN, identificadores de redes
Wi-Fi ou logs sem sanitização.

Registrar somente observações sanitizadas e conclusões dos testes.

---

## English

### Scope

Authorized testing exclusively on the owner's Linux laboratory.

### Completed observations

- nftables rule syntax validation completed successfully.
- The Kill Switch service was active after system reboot.
- The firewall table was present after startup.
- The observed IPv4 and IPv6 routes used the VPN interface.
- Direct IPv4 and IPv6 connection attempts timed out.
- Firewall drop counters increased during direct connection attempts.
- A direct DNS test query timed out.

These are laboratory observations. Timeouts alone do not prove that
all connections were blocked.

### Required follow-up

- Capture packets during boot and VPN reconnection.
- Test VPN failure and recovery in a controlled maintenance window.
- Verify DNS behavior using packet capture.
- Review IPv6, interface changes, and alternative routing scenarios.
- Review systemd dependencies and failure behavior.

### Evidence handling

Do not store raw command output, real IP addresses, private keys,
tokens, VPN endpoint details, Wi-Fi identifiers, or unsanitized logs.

Record only sanitized observations and test conclusions.

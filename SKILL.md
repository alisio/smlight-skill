---
name: smlight
description: Use quando trabalhar com dispositivos SMLIGHT SLZB, SLZB-OS, coordenadores Zigbee ou Thread, integração com Home Assistant, ZHA ou Zigbee2MQTT, configuração, diagnóstico ou firmware.
---

# SMLIGHT

Use a documentação oficial correspondente ao modelo, hardware, firmware e versão instalados. Recursos, interfaces e procedimentos diferem entre produtos e versões; não suponha que todo dispositivo SMLIGHT execute SLZB-OS.

## Procedimento

1. Identifique modelo e revisão, firmware do sistema e do rádio, modo de operação, conexão e integração usada. Solicite os dados ausentes quando mudarem a resposta.
2. Consulte a referência pertinente e confirme na documentação oficial da versão em uso. Diferencie o hub Zigbee integrado ao SLZB-OS de um rádio controlado por Zigbee2MQTT ou ZHA externo; identifique onde estão a rede e seus backups.
3. Diagnostique por camadas: alimentação e rede, SLZB-OS, rádio, controlador Zigbee ou Thread, MQTT e Home Assistant. Prefira leituras e preserve senhas, tokens, chaves de rede e backups.
4. Antes de alterar configurações, reiniciar, migrar, atualizar ou restaurar, explique destino, impacto, interrupção possível, backup e recuperação; peça confirmação explícita. Confira o resultado após a operação. Não suponha que downgrade ou migração de rede sejam possíveis.

| Tarefa | Referência |
| --- | --- |
| Modelo, rádios, modos, Zigbee, Thread e Home Assistant | [Dispositivos e integração](reference/dispositivos.md) |
| Interface web, MQTT, automação e Ansible | [Gestão e automação](reference/gestao.md) |
| Diagnóstico, backups, recuperação e firmware | [Operação e diagnóstico](reference/operacao.md) |

## Cuidados

- Um rádio não deve ser controlado simultaneamente por múltiplos clientes; confirme a topologia antes de conectar outro controlador.
- Alterações de rede, rádio, canal ou identidade Zigbee podem interromper o acesso ou exigir migração; valide o procedimento para o cenário exato.
- Diferencie firmware do SLZB-OS, firmware do rádio e ESPHome; atualização de um não implica atualização dos demais.
- Não invente endpoints ou parâmetros, nem trate a API interna da interface web como contrato estável. Se não houver método documentado para a versão, informe a limitação.

Fontes: [manuais SMLIGHT](https://smlight.tech/support/manuals/), [manual do Zigbee Hub](https://smlight.tech/support/manuals/books/slzb-os/chapter/zigbee-hub), [API MQTT](https://smlight.tech/support/manuals/books/slzb-os/page/mqtt-api) e [ESPHome SMLIGHT](https://github.com/smlight-tech/slzb-esphome).

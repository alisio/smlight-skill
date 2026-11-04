# Skill SMLIGHT

Skill para orientar a configuração, operação, integração e diagnóstico de dispositivos SMLIGHT e SLZB-OS. As capacidades variam conforme modelo, firmware e modo de operação; consulte a documentação oficial aplicável.

## Instalação

Copie `SKILL.md` e o diretório `reference/` juntos para um diretório chamado `smlight` no local de skills do cliente. Verifique antes se o destino já existe e preserve alterações locais. Consulte a documentação da versão do cliente para confirmar o local suportado e a necessidade de reinício.

| Cliente | Diretório de usuário usual |
| --- | --- |
| OpenCode | `~/.config/opencode/skills/smlight` |
| Claude Code | `~/.claude/skills/smlight` |
| Codex | `~/.agents/skills/smlight` |

## Uso

Peça ao agente, por exemplo: “Use a skill smlight para diagnosticar meu coordenador SLZB sem alterar a configuração.” Informe modelo, versão, modo e integração quando disponíveis. Confirme que o cliente carregou a skill; disponibilidade não garante acionamento automático.

## Atualização

As cópias instaladas são independentes. Compare `SKILL.md` e `reference/` com a cópia instalada antes de atualizar e preserve modificações locais. A cópia de arquivos não remove referências antigas.

## Fontes

- [Manuais SMLIGHT](https://smlight.tech/support/manuals/)
- [Manual do Zigbee Hub](https://smlight.tech/support/manuals/books/slzb-os/chapter/zigbee-hub)
- [API MQTT do SLZB-OS](https://smlight.tech/support/manuals/books/slzb-os/page/mqtt-api)
- [ESPHome SMLIGHT](https://github.com/smlight-tech/slzb-esphome)

# Dispositivos e integração

Identifique o modelo exato e sua revisão na documentação do fabricante antes de indicar fonte de alimentação, recursos de rede, rádios ou firmware. O catálogo e a lista de capacidades mudam; não extrapole de um modelo para outro.

- A família SLZB-06 inclui modelos com um rádio Zigbee/Thread; modelos MR têm dois rádios e podem operar redes separadas simultaneamente. Confirme a combinação efetiva de hardware e firmware.
- Séries U oferecem recursos adicionais em modelos compatíveis; USB host, OTBR e Bluetooth dependem do modelo e firmware. SLZB-07 é uma linha USB: não presuma interface web ou SLZB-OS para ela.
- Zigbee e Thread no mesmo rádio com firmware multiprotocolo não equivalem a duas redes em rádios separados; consulte as recomendações atuais do Home Assistant e do fabricante.
- No modo coordenador externo, Zigbee2MQTT ou ZHA gerencia a rede por meio do rádio. No Zigbee Hub integrado, a pilha roda no SLZB-OS e pode integrar-se via MQTT. São arquiteturas distintas, com backup e migração próprios.
- Para Thread, diferencie RCP com OTBR externo de OTBR no dispositivo. Confirme suporte, versão e requisitos de rede antes de configurar.
- Para ZHA ou Zigbee2MQTT, consulte a documentação da integração e o gerador de configuração do dispositivo quando disponível. Use a interface, porta, protocolo e driver correspondentes ao rádio e firmware; evite clientes simultâneos no mesmo rádio.

Fontes: [manuais SMLIGHT](https://smlight.tech/support/manuals/), [Zigbee Hub](https://smlight.tech/support/manuals/books/slzb-os/chapter/zigbee-hub), [Zigbee2MQTT](https://www.zigbee2mqtt.io/) e [Home Assistant](https://www.home-assistant.io/integrations/zha/).

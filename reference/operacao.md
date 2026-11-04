# Operação e diagnóstico

## Diagnóstico

Registre modelo, versão do SLZB-OS, firmware do rádio, modo, topologia e sintomas. Verifique alimentação e conectividade antes de investigar rádio, controlador, broker e Home Assistant. Consulte logs sem divulgar segredos; isole cada camada antes de propor mudanças.

Uma falha de descoberta no Home Assistant não prova falha na rede Zigbee. Uma resposta MQTT ou HTTP confirma apenas o que a interface informa; verifique também o estado observado na integração e nos dispositivos.

## Mudanças, backup e recuperação

Antes de alterar rede, canal, modo ou firmware, identifique onde a rede e suas chaves são mantidas e faça backup protegido pelo método do controlador efetivamente em uso. Confirme compatibilidade do backup com o destino e o procedimento de restauração; tenha acesso físico e plano de recuperação quando necessário. Não prometa migração sem reemparelhamento.

Na migração, confirme se o destino importa o estado e a identidade da rede; preservar a rede não garante preservar nomes, grupos ou integrações. Não opere dois coordenadores com a mesma identidade simultaneamente. Preserve o controlador e os dados de origem até validar o destino e defina quando interromper ou retornar.

Diferencie atualização do sistema da atualização do rádio. Confira notas da versão de origem e de destino, modelo, alimentação, janela de interrupção e recuperação antes de pedir autorização. Não apague backups antigos automaticamente: algumas versões podem mudar formatos ou exigir procedimento especial. Após atualizar, confirme versão, conectividade, controlador e funcionamento dos dispositivos.

Quando possível, verifique a integridade do backup e teste a restauração antes da mudança. Identifique os serviços afetados e critérios de conclusão ou interrupção; considere o tempo necessário para dispositivos adormecidos voltarem a comunicar.

Se o manual apresentar orientações divergentes entre versões, exponha a incerteza e confira a versão específica antes de agir. Mudanças de canal, chaves e firmware podem afetar dispositivos adormecidos ou exigir intervenção física.

Fonte: [manuais SMLIGHT](https://smlight.tech/support/manuals/), notas da versão instalada e documentação do controlador efetivamente usado.

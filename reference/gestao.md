# Gestão e automação

## Escolha da interface

Verifique no manual da versão quais opções são suportadas: interface web, MQTT, métricas, eventos ou outras interfaces documentadas. A API MQTT do Zigbee Hub e a API MQTT geral do SLZB-OS não são intercambiáveis; confirme versão, modo, tópicos e autenticação antes de usar. A documentação fornecida situa a API MQTT geral a partir da versão 3.2.4, mas os recursos específicos podem exigir versões posteriores.

A API interna da interface web não é um contrato público estável. Se uma operação não tiver interface documentada para a versão instalada, informe isso e proponha o procedimento oficial disponível; não adivinhe endpoints, parâmetros ou semântica de retorno.

Restrinja o acesso de gestão à rede confiável e proteja credenciais e chaves. Confirme se a versão oferece TLS antes de transmitir segredos; quando não oferecer, avalie um túnel seguro apropriado, sem expor a interface diretamente à internet.

## Ansible

Ansible é uma opção de automação, não um requisito. Identifique primeiro o método de gestão documentado e o ambiente onde os módulos serão executados; não presuma acesso SSH ao dispositivo. Compare estado atual e desejado quando a interface permitir, mantenha segredos em mecanismo apropriado e evite registrá-los em logs. Declare explicitamente limitações de idempotência, check mode e recuperação quando não puderem ser verificadas.

Solicite confirmação antes de executar mudanças e teste inicialmente em ambiente isolado ou dispositivo autorizado. Após aplicar, leia o estado novamente quando possível; aceite da requisição não prova que a mudança funcionou.

Sem leitura confiável do estado, não afirme idempotência nem verificação posterior. O modo de verificação do Ansible, por si só, não garante que uma API não tenha efeitos colaterais.

Fonte: [API MQTT do fabricante](https://smlight.tech/support/manuals/books/slzb-os/page/mqtt-api) e documentação oficial aplicável à versão instalada.

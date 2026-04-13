Por que o secret aparece como ***? 
O GitHub Actions registra todos os valores declarados como secrets e instrui o runner a substituir qualquer ocorrência deles nos logs pelo texto ***, mesmo que você tente imprimi-los explicitamente. 
É uma proteção automática e irremovível. Variáveis do tipo vars são configuração não-sensível, então aparecem normalmente.

O deploy_app consegue ler BUILD_VERSION do build_app? 
Não. Cada job é executado em um runner completamente isolado — uma máquina virtual nova e efêmera. Variáveis de env existem apenas na memória daquele runner durante aquela execução. Quando o deploy_app inicia, ele está em uma máquina diferente que nunca teve BUILD_VERSION. Para compartilhar dados entre jobs seria necessário usar outputs ou artifacts.

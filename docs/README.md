# Modelagem do Sistema de Robôs Autônomos em um Armazém

## Descrição Geral 
Em um armazém automatizado, dois robôs móveis transportam caixas de insumos entre um Buffer de Entrada (BE) e máquinas de processamento. Cada robô tem uma rota específica e restrições operacionais que garantem a segurança e eficiência do transporte.  Os  robôs  seguem  trajetórias  predefinidas,  e  eventos  como  solicitações  de transporte,  falhas  ou  congestionamentos  podem  ocorrer.

## Componentes do Sistema

### Buffer de Entrada
O acesso ao estoque do armazém ocorre atráves do **Buffer de Entrada**. Cada robô possui uma baia especifíca de acesso ao buffer, evitando colisão entre eles ao acessar a área. 

### Máquinas de Produção
A produção ocorre atráves de máquinas que operam com os insumos armazenados no estoque. Ao serem iniciadas, as máquinas devem requisitar os insumos a um dos robôs, que descarregaram-os e esperam a próxima requisição. Ao finalizar o processo, as máquinas ficam ociosas e podem fazer uma nova requisição.

#### Estados 
- **Ociosa**: máquina ociosa após processamento.
- **EsperandoInsumo**: máquina após a requisição, esperando pelo robô.
- **EmProcessamento**: máquina processando o insumo.

#### Eventos
- request_M1_R1
### Robôs Autônomos



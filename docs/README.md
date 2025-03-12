# 📜Modelagem do Sistema de Robôs Autônomos em um Armazém

## 🔎 Descrição Geral 
Em um armazém automatizado, dois robôs móveis transportam caixas de insumos entre um Buffer de Entrada (BE) e máquinas de processamento. Cada robô tem uma rota específica e restrições operacionais que garantem a segurança e eficiência do transporte.  Os  robôs  seguem  trajetórias  predefinidas,  e  eventos  como  solicitações  de transporte,  falhas  ou  congestionamentos  podem  ocorrer.

## ⚙️ Componentes do Sistema

### 🏢 Buffer de Entrada
O acesso ao estoque do armazém ocorre atráves do **Buffer de Entrada**. Cada robô possui uma baia especifíca de acesso ao buffer, evitando colisão entre eles ao acessar a área. 

### 👷‍♂️ Máquinas de Produção
A produção ocorre atráves de máquinas que operam com os insumos armazenados no estoque. Ao serem iniciadas, as máquinas devem requisitar os insumos a um dos robôs, que descarregaram-os e esperam a próxima requisição. Ao finalizar o processo, as máquinas ficam ociosas e podem fazer uma nova requisição.

#### Estados 
- **Ociosa**: máquina ociosa após processamento.
- **EsperandoInsumo**: máquina após a requisição, esperando pelo robô.
- **EmProcessamento**: máquina processando o insumo.

#### Eventos
- **request_MX_R1, request_MX_R2, request_MX_R3**: A máquina X solicita um insumo ao robô.
- **R1_unload_MX, R2_unload_MX, R3_unload_MX**: O robô descarrega o insumo na máquina X.
- **MX_release**: A máquina X entrega o produto e finaliza o processamento.


<p align="center">
<img src="https://github.com/user-attachments/assets/1c5eb4c6-d666-4e14-b566-b706810416fa" height="200" align="center">
</p>

<p align="center">Figura 02: Autômato da Máquina 01</p>

### 🤖 Robôs Autônomos
Os robôs são encarregados de, após receberem uma solicitação, enviar os insumos para as 4 máquinas. O robô 01 é responsável pelo suprimento das máquinas 1 e 2, enquanto o robô 02 é responsável pelas máquinas 3 e 4. É possível que durante a entrega dos insumos, os robôs apresentem falhas e não consigam finalizar sua tarefa. Para contornar isto, o robô 03 é programado para finalizar o pedido do robô inoperante e substituí-lo enquanto ele não resetar. 

#### Estados - Robôs de Entrega
- **Ocioso**: Robôs esperando uma requisição das máquinas.
- **LocalizandoPedidoParaMX**: Robô em deslocamento para o buffer de entrada.
- **TranspCaixaParaMX**: Robô levando os insumos para a máquina X.
- **EmFalha_MX**: Robô inoperante após receber um pedido da máquina X.
  
#### Eventos - Robôs de entrega
- **request_MX_R1, request_MX_R2**:  A máquina X solicita um insumo ao robô.
- **R1_load_box, R2_load_box**: Os robôs carregam os insumos do buffer de entrada.
- **R1_unload_MX, R2_unload_MX**: Os robôs descarregam os insumos nas máquinas.
- **R1_failure_in_MX, R2_failure_in_MX**: Os robôs falham enquanto levavam pedidos para a máquina X.
- **R1_reset, R2_reset**: Os robôs resetaram seu funcionamento.

<p align="center">
<img src="https://github.com/user-attachments/assets/aaf10960-e171-4a17-8e2b-21930b6fad99" height="200" align="center">
</p>
<p align="center">Figura 03: Autômato do Robô 01</p>

#### Estados - Robô Substituto
- **Ocioso**: Robô aguardando ser acionado.
- **R3LocalizandoPedidoParaMX**: Robô em deslocamento para o buffer de entrada.
- **R3TranspCaixaParaMX**: Robô levando os insumos para a máquina X.
- **R3AcionadoPara_MX_MY**: Robô disponível para ser responder os chamados da máquina X e Y.

#### Eventos - Robôs Substituto 
- **R1_failure_in_MX, R2_failure_in_MX**: Os robôs falharam, acionando o robô 03.
- **R3_load_box**: O robô carrega os insumos do buffer de entrada.
- **R3_unload_MX**: O robôs descarrega os insumos nas máquinas.
- **request_MX_R3**:  A máquina X solicita um insumo ao robô.
- **R1_reset, R2_reset**: Os robôs resetaram seu funcionamento.

<p align="center">
<img src="https://github.com/user-attachments/assets/70059840-3424-483f-bbe6-0f7b3a37f573" height="400" align="center">
</p>
<p align="center">Figura 04: Autômato do Robô 03</p>


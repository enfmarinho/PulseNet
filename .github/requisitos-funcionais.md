# Sistema de Monitoramento de Sensores Hospitalares

---

## Requisitos Funcionais (RF)

### Sensores
- RF1: O sistema deve coletar dados de sensores de frequência cardíaca, frequência respiratória, pressão arterial e eletrocardiograma.
- RF2: Cada sensor deve enviar suas leituras para o coletor com uma periodicidade de no mínimo uma vez por segundo.

### Coletor
- RF3: O coletor deve processar dados em tempo real, com latência máxima de 500ms da leitura do sensor até o processamento inicial.
- RF4: Em caso de falha de um coletor, o sistema deve ter um mecanismo de fallback automático, garantindo a continuidade da operação de ingestão de dados.

### Mensageria
- RF5: A mensageria deve agrupar sensores em clusters de alto volume (Cluster 1) e clusters de baixa carga (Cluster 2) para otimização do fluxo de dados.
- RF6: Cada sensor deve publicar seus dados em tópicos específicos, utilizando uma chave de leitura para identificação e roteamento.
- RF7: A arquitetura da mensageria deve gerenciar o paralelismo interno para processar múltiplos streams de dados simultaneamente, evitando gargalos.

### Gateways
- RF8: Cada gateway deve registrar e atualizar automaticamente quais partições está consumindo da mensageria.
- RF9: Se um gateway falhar, suas partições devem ser reatribuídas a outro gateway disponível em no máximo 10 segundos, sem perda de dados.
- RF10: O sistema deve permitir a adição de múltiplos gateways de forma dinâmica para balanceamento de carga.
- RF11: Os gateways devem enviar os dados de sensores para o Load Balancer.

### Load Balancer
- RF12: O Load Balancer deve distribuir uniformemente os dados recebidos dos gateways para as aplicações clientes.

### Aplicações Cliente
- RF13: O Dashboard de Monitoramento deve exibir os dados de todos os sensores em tempo real, com uma taxa de atualização de no mínimo 200ms.
- RF14: O Serviço de Alerta deve monitorar as leituras dos sensores e emitir alertas em menos de 1 segundo após a detecção de uma leitura crítica.
- RF15: O Serviço de Alerta deve suportar fallback em caso de falha, garantindo que a emissão de alertas não seja interrompida.
- RF16: A Lógica Médica deve avaliar os critérios de medição e determinar a severidade de cada leitura (crítica, atenção, estável).
- RF17: O sistema deve enviar comandos para acionar LEDs e alarmes sonoros que indiquem o estado do paciente.

### Corredor/Leito
- RF18: Os LEDs (vermelho para crítico, amarelo para atenção, verde para estável) devem ser atualizados em até 500ms após o recebimento de um alerta.
- RF19: Alarmes sonoros para sinais críticos devem ser disparados imediatamente após a detecção do alerta.

---


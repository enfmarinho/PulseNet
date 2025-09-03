# Requisitos do Sistema de Monitoramento de Sensores Hospitalares

## 1. Sensores
- Sensores de frequência cardíaca
- Sensores de frequência respiratória
- Sensores de pressão arterial
- Sensores de eletrocardiograma

## 2. Coletor
- Deve coletar dados de todos os sensores conectados.
- Deve suportar 1 processo em execução + 2 de fallback em caso de falha.

## 3. Mensageria
- Suporte a clusters de sensores:
  - Cluster 1: Sensores principais de alto volume
  - Cluster 2: Sensores secundários e específicos, com baixa carga
- Cada sensor → tópico → chave = dado lido
- Paralelismo tratado internamente

## 4. Gateways
- Cada gateway adiciona informações sobre quais partições consome.
- Se um gateway cair, as partições são reatribuídas e o registro é atualizado.
- Gateways individuais (Gateway 1, Gateway 2, ..., Gateway N)

### 4.1 Gateway Register
- Registrar quais gateways estão ativos

### 4.2 Load Balancer
- Distribuir dados dos sensores entre os gateways ativos

## 5. Aplicações Cliente
### 5.1 Dashboard de monitoramento
- Aplicação Web que consome dados dos gateways
- Monitoramento do lado da cama do paciente

### 5.2 Serviço de alerta
- Monitora dados dos sensores
- Emite alertas nos leitos
- Suporte a 1 processo em execução + 2 de fallback
- Envia dados para lógica médica

### 5.3 Lógica médica
- Avaliação de medições dos pacientes
- Critérios de decisão para alertas críticos ou estáveis

## 6. Corredor/Leito
- LEDs e alarmes para sinalização visual/auditiva:
  - LED de sinais críticos
  - Alarme de sinais críticos
  - LED de sinais estáveis
  - LED de sinais de atenção

### Outros Requisitos a Considerar:

- Usabilidade: A interface do dashboard deve ser intuitiva para profissionais de saúde, com treinamento mínimo.
- Conformidade: O sistema deve estar em conformidade com as regulamentações de privacidade de dados de saúde (por exemplo, LGPD).
- Auditoria: O sistema deve registrar todos os eventos de alerta e as ações tomadas (por exemplo, alarmes silenciados) para fins de auditoria.
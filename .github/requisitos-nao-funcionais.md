# Sistema de Monitoramento de Sensores Hospitalares

---

## Requisitos Não Funcionais (RNF)

### Desempenho
- RNF1: O sistema deve processar dados de 1.000 sensores por segundo, com picos de até 2.000 sensores/segundo.
- RNF2: A latência de ponta a ponta (do sensor ao alerta/dashboard) não deve exceder 1 segundo.
- RNF3: O sistema deve suportar simultaneamente o Cluster 1 (alto volume) e o Cluster 2 (baixa carga).

### Confiabilidade
- RNF4: O sistema deve manter a operação de ingestão de dados e alertas mesmo se um coletor ou gateway falhar.
- RNF5: A mensageria deve garantir que nenhuma mensagem seja perdida, mesmo em caso de falhas de componentes.
- RNF6: O paralelismo da mensageria deve ser gerido internamente para evitar congestionamento e garantir a ordem dos eventos por sensor.

### Escalabilidade
- RNF7: O sistema deve permitir a adição de novos gateways e aplicações clientes de forma dinâmica, sem necessidade de downtime.
- RNF8: A arquitetura deve suportar um aumento de 50% no número de sensores e clusters.

### Manutenibilidade
- RNF9: O sistema deve ser composto por microsserviços modularizados (Sensor, Coletor, Mensageria, Gateways, Aplicações Cliente).
- RNF10: A adição de um novo tipo de sensor ou critério de alerta deve ser possível através de configurações, sem alterar o código-fonte dos componentes centrais.

### Segurança
- RNF11: Todos os dados sensíveis dos pacientes devem ser criptografados em trânsito (TLS) e em repouso (AES-256).
- RNF12: O acesso ao dashboard e aos serviços de alerta deve ser autenticado e autorizado via MFA (Autenticação Multifator).

### Disponibilidade
- RNF13: O sistema deve ter uma disponibilidade de 99,9%, minimizando o downtime.
- RNF14: Os mecanismos de fallback devem garantir a operação parcial e a detecção de sinais críticos, mesmo durante falhas.


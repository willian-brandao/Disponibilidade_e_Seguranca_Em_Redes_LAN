
# Configuração de Porta Híbrida - Manual de Comandos
## Comandos de Configuração
### Etapa 1: Configurar Tipo de Link como Híbrido
```
[Switch-GigabitEthernet1/0/1] port link-type hybrid
```
Explicação: Define o tipo de link da porta como híbrido, permitindo o tráfego de múltiplas VLANs com diferentes comportamentos de tagging.

### Etapa 2: Associar VLANs à Porta Híbrida
```
[Switch-GigabitEthernet1/0/1] port hybrid vlan vlan-id-list {tagged | untagged}
```
Explicação:

vlan-id-list: Lista de IDs de VLAN a serem associadas à porta

tagged: Mantém as tags VLAN nos quadros (uso entre switches)

untagged: Remove as tags VLAN dos quadros (uso para dispositivos finais)

Exemplos:
```
[Switch-GigabitEthernet1/0/1] port hybrid vlan 10,20,30 tagged
[Switch-GigabitEthernet1/0/1] port hybrid vlan 40,50 untagged
```
### Etapa 3: Definir VLAN PVID (VLAN Nativa)
```
[Switch-GigabitEthernet1/0/1] port hybrid pvid vlan vlan-id
```
Explicação:
Define a VLAN padrão (PVID) para a porta híbrida
Quadros que chegam sem tag recebem automaticamente esta VLAN ID

Exemplo:
```
[Switch-GigabitEthernet1/0/1] port hybrid pvid vlan 10
```
### Observação Importante

Conversão entre Tipos de Porta
## Para converter porta trunk para híbrida ou vice-versa:
## Primeiro configure como porta de acesso
```
[Switch-GigabitEthernet1/0/1] port link-type access
```
## Depois configure como desejado
```
[Switch-GigabitEthernet1/0/1] port link-type hybrid
```
### Comportamento Padrão

Por padrão, uma porta híbrida permite apenas a passagem de quadros da VLAN 1
É necessário configurar explicitamente as VLANs desejadas

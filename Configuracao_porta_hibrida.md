Configuração de Porta Híbrida - Manual de Instruções
bash
# ETAPA 1: Configurar o tipo de link como híbrido
# Entra no modo de configuração da interface GigabitEthernet1/0/1
# system-view: acessa o modo de configuração global do switch
system-view

# Interface GigabitEthernet1/0/1: seleciona a porta física para configuração
interface GigabitEthernet1/0/1

# port link-type hybrid: define o tipo de link como híbrido
# (permite tráfego de múltiplas VLANs com ou sem tags)
port link-type hybrid
bash
# ETAPA 2: Associar VLANs à porta híbrida
# port hybrid vlan: adiciona a porta às VLANs especificadas
# vlan-id-list: lista de IDs de VLAN separados por vírgula ou intervalo
# tagged: mantém as tags VLAN nos quadros (para VLANs tagged)
# untagged: remove as tags VLAN nos quadros (para VLANs untagged)
port hybrid vlan 10,20,30 tagged
port hybrid vlan 40,50 untagged
bash
# ETAPA 3: Definir a VLAN PVID (Port VLAN ID)
# port hybrid pvid vlan: define a VLAN nativa/untagged padrão
# vlan-id: ID da VLAN que será usada como padrão para quadros sem tag
# Os quadros sem tag receberão automaticamente esta VLAN ID
port hybrid pvid vlan 10
bash
# COMANDO DE VERIFICAÇÃO:
# Sai do modo de interface e verifica a configuração
quit
display current-configuration interface GigabitEthernet1/0/1

# OU verifica especificamente as configurações de VLAN da porta
display port hybrid
bash
# OBSERVAÇÃO IMPORTANTE:
# Para converter entre porta trunk e híbrida, primeiro deve-se:
# 1. Configurar como porta de acesso (reset)
port link-type access
# 2. Depois configurar como híbrida
port link-type hybrid
Explicação dos Conceitos:

Porta Híbrida: Permite passar múltiplas VLANs, algumas tagged (com tag) e outras untagged (sem tag)

VLAN Tagged: Mantém a tag VLAN - usado para comunicação entre switches

VLAN Untagged: Remove a tag VLAN - usado para dispositivos finais

PVID: VLAN ID padrão para quadros que chegam sem tag


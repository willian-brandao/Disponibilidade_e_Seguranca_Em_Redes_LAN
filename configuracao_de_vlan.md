# Configuração de VLAN 
## Criar VLAN e adicionar portas
Etapa 1 – Criar uma VLAN
```
vlan vlan-id
```
Descrição: Cria uma VLAN no switch e entra no modo de configuração dessa VLAN.

Etapa 2 – Atribuir portas à VLAN
```
port interface-list
```
Descrição: Atribui uma ou mais portas físicas à VLAN criada.
As portas passam a encaminhar tráfego pertencente à VLAN.

## Configurar porta como tronco (trunk)
### Etapa 1 – Definir o tipo de link da porta como trunk

```
[Switch-GigabitEthernet1/0/1] port link-type trunk
```
Descrição: Configura a porta para operar como trunk, permitindo transportar várias VLANs simultaneamente.

### Etapa 2 – Permitir VLANs no trunk
```
[Switch-GigabitEthernet1/0/1] port trunk permit vlan { vlan-id-list | all }
```
Descrição: Especifica quais VLANs podem trafegar pelo trunk.
```
vlan-id-list: lista de VLANs permitidas
```
all: permite todas as VLANs existentes

Sem essa configuração, apenas a VLAN 1 é permitida por padrão.

### Etapa 3 – Definir VLAN nativa (PVID)
```
[Switch-GigabitEthernet1/0/1] port trunk pvid vlan vlan-id
```
Descrição: Define a VLAN nativa da porta trunk.
A VLAN nativa recebe quadros sem tag (untagged).

Observação: Por padrão, o PVID do trunk é VLAN 1.
Se o equipamento conectado utilizar outra VLAN como PVID, é necessário ajustar para evitar inconsistências e falhas de comunicação.

# Projeto de Banco de Dados para Oficina

Este projeto tem como objetivo a criação de um banco de dados relacional para gerenciar as operações de uma oficina. O banco de dados foi desenvolvido a partir de um modelo conceitual utilizando o modelo Entidade-Relacionamento (ER) e implementado em MySQL. O esquema lógico foi projetado para armazenar informações sobre clientes, veículos, equipes, mecânicos, serviços e ordens de serviço.

## Esquema Lógico

O banco de dados contém as seguintes tabelas e relacionamentos:

### Tabelas

1. **Oficina**
   - `idOficina`: Identificador único da oficina.
   - `Razão Social`: Razão social da oficina.
   - `Nome de Fantasia`: Nome de fantasia da oficina.

2. **Cliente**
   - `idCliente`: Identificador único do cliente.
   - `Nome`: Nome do cliente.
   - `Oficina_idOficina`: Chave estrangeira referenciando a oficina.
   
3. **Equipe**
   - `idEquipe`: Identificador único da equipe.
   - `Descrição`: Descrição da equipe.

4. **Veículo**
   - `idVeiculo`: Identificador único do veículo.
   - `Descrição`: Descrição do veículo.
   - `Marca`: Marca do veículo.
   - `Placa`: Placa do veículo.
   - `Cliente_idCliente`: Chave estrangeira referenciando o cliente.
   - `Equipe_idEquipe`: Chave estrangeira referenciando a equipe responsável.

5. **Mecânico**
   - `idMecânico`: Identificador único do mecânico.
   - `Nome`: Nome do mecânico.
   - `Oficina_idOficina`: Chave estrangeira referenciando a oficina.
   - `Equipe_idEquipe`: Chave estrangeira referenciando a equipe.
   - `Endereço`: Endereço do mecânico.
   - `Especialidade`: Especialidade do mecânico.

6. **Serviço**
   - `idServiço`: Identificador único do serviço.
   - `Descrição`: Descrição do serviço.
   - `Tipo de Serviço`: Tipo do serviço (ex: reparo, manutenção).
   - `Data do Serviço`: Data em que o serviço foi realizado.

7. **Itens de Serviço**
   - `idItens de Serviço`: Identificador único do item de serviço.
   - `Descrição`: Descrição do item.
   - `Valor`: Valor do item de serviço.
   - `Numero de Serie`: Número de série do item.

8. **Serviço/Itens**
   - Relaciona os itens aos serviços, indicando a quantidade de itens utilizados em cada serviço.

9. **Veículo/Serviço**
   - Relaciona os veículos aos serviços realizados, permitindo acompanhar a quantidade e o valor dos serviços prestados a cada veículo.

10. **Ordem de Serviço**
    - `idOrdem de Serviço`: Identificador único da ordem de serviço.
    - `Descrição`: Descrição da ordem de serviço.
    - `Data de Emissão`: Data em que a ordem de serviço foi emitida.
    - `valor`: Valor da ordem de serviço.
    - `Veiculo/Serviço_Veiculo_idVeiculo`: Chave estrangeira referenciando o veículo.
    - `Veiculo/Serviço_Serviço_idServiço`: Chave estrangeira referenciando o serviço.
    - `Data Autorização`: Data em que a ordem de serviço foi autorizada.
    - `Status`: Status da ordem de serviço (ex: pendente, concluída).
    - `Data Conclusão`: Data em que o serviço foi concluído.

### Relacionamentos

- **Cliente e Oficina**: Cada cliente está associado a uma oficina.
- **Veículo e Cliente/Equipe**: Cada veículo pertence a um cliente e é associado a uma equipe.
- **Mecânico e Oficina/Equipe**: Cada mecânico trabalha em uma oficina e pertence a uma equipe.
- **Serviço e Oficina**: Cada serviço é realizado em uma oficina.
- **Veículo e Serviço**: Cada veículo pode ter vários serviços associados a ele.
- **Itens de Serviço e Serviço**: Itens de serviço estão relacionados aos serviços específicos.
- **Ordem de Serviço e Veículo/Serviço**: Cada ordem de serviço está associada a um veículo e a um serviço específico.

## Script de Criação do Banco de Dados

O script SQL para a criação do banco de dados foi desenvolvido utilizando MySQL e está disponível no repositório. Ele inclui a criação de todas as tabelas, definições de chaves primárias e estrangeiras, além de garantir a integridade referencial entre as entidades.

## Consultas SQL

Foram criadas diversas consultas SQL para realizar as operações de recuperação de dados, incluindo:

- Recuperações simples com `SELECT`.
- Filtros com a cláusula `WHERE`.
- Criação de expressões para gerar atributos derivados.
- Ordenações de dados com `ORDER BY`.
- Uso de `HAVING` para filtragem em grupos.
- Junções entre tabelas para fornecer uma perspectiva mais completa dos dados.

Exemplo de consulta complexa:

```sql
SELECT c.Nome, v.Placa, s.Descrição, os.Data de Emissão
FROM Cliente c
JOIN Veiculo v ON c.idCliente = v.Cliente_idCliente
JOIN Veiculo/Serviço vs ON v.idVeiculo = vs.Veiculo_idVeiculo
JOIN Serviço s ON vs.Serviço_idServiço = s.idServiço
JOIN Ordem de Serviço os ON vs.Veiculo_idVeiculo = os.Veiculo/Serviço_Veiculo_idVeiculo
WHERE os.Status = 'Concluída'
ORDER BY os.Data de Emissão DESC;

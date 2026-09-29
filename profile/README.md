# Iron Deploy

**Controle na camada de execução para agentes de IA que operam infraestrutura.**

Agentes de IA já rodam `terraform`, `kubectl` e CLIs de nuvem com as credenciais de quem os usa. Guardrail no prompt não é controle: o controle precisa ficar fora do agente, e a aprovação só funciona quando mostra o alcance do que vai mudar. A Iron Deploy constrói essa camada.

## Produtos

### Iron Brake
O freio que mostra o que o agente vai destruir. Intercepta o comando **antes** de rodar, bloqueia o que nunca é certo e mostra o alcance do que muda, por exemplo quantos recursos serão criados, apagados ou substituídos em um `terraform apply`.

- Local-first: binário Go único, sem rede e sem telemetria
- Código aberto: [IronDeploy/IronBrake](https://github.com/IronDeploy/IronBrake)

### Iron Shield
Raio-X das credenciais ao alcance do agente. Lista o que o agente consegue enxergar (variáveis de ambiente, perfis de nuvem, tokens em cache) sem ler nem imprimir nenhum valor de segredo.

## Como pensamos

1. **Controle fora do agente.** Ele vive na camada de execução, não no prompt.
2. **Aprovação com alcance.** Um "sim ou não" não basta: é preciso ver o que será destruído.
3. **O valor está no time.** Política, aprovação e auditoria de grupo são o que falta hoje.

O Iron Brake é um cinto de segurança: reduz risco, não o elimina, e não substitui backup isolado nem privilégio mínimo.

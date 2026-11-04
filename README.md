# SPHY Framework - RDTSC & Chaos Stress Validation Suite

Este repositório fornece o script oficial de validação empírica para o **Framework SPHY**. O objetivo deste utilitário é auditar datasets atômicos de alta precisão gerados sob condições extremas de estresse estocástico, comprovando a estabilidade e a coerência de fase do manifold sem expor a lógica proprietária do kernel subjacente.

---

## O Que Este Validador Faz

O script `sphy_validator_rdtsc.py` realiza uma varredura estrita e de leitura (*read-only*) no dataset gerado (`sphy_ghz_chaos_rdtsc_dataset.csv`), executando as seguintes verificações de integridade em 12.000 frames de execução:

1. **Auditoria de Coerência e Variância:** Valida se o manifold mantém 100.00% de coerência de fase e variância global zerada ($0.00$), mesmo sob injeção máxima de caos.
2. **Estresse de Ruído Térmico e Bit-Flip ($P = 1.0$):** Confirma que o sistema absorve e neutraliza perturbações estocásticas e inversões de bits simuladas no hardware[cite: 1, 2].
3. **Invariância de Memória:** Assegura que o consumo de memória permaneça estático e restrito à pilha (`6152 KB`, com alocação zero de *heap*), garantindo complexidade estrita $\mathcal{O}(1)$[cite: 1, 2].
4. **Telemetria de Silício (RDTSC):** Processa os registros de ciclo de clock do processador travados em 2.49 GHz e timestamps de alta precisão (`CLOCK_MONOTONIC_RAW`)[cite: 1, 2].

---

## Requisitos de Sistema

O validador é escrito em Python puro e não requer dependências externas complexas para execução básica.

* **Python:** Versão `3.6` ou superior.
* **Sistema Operacional:** Compatível com ambientes Linux (testado e otimizado em Pop!_OS / Ubuntu)[cite: 1, 2].

---

## Como Executar

1. Certifique-se de que o arquivo de dataset gerado (`sphy_ghz_chaos_rdtsc_dataset.csv`) está presente no mesmo diretório do script[cite: 1, 2].
2. Execute o validador via terminal:

```bash
python3 sphy_validator_rdtsc.py

# 🛡️ Flow Check Test

Repositório de demonstração e testes ("Sandbox") para validação de fluxos de governança de branches utilizando GitHub Actions.

Este projeto serve como ambiente de homologação para as Actions:
- [**Branch Flow Guard**](https://github.com/Malnati/branch-flow-guard)
- [**PR Comment Template**](https://github.com/Malnati/pr-comment)

## 📋 Objetivo

Garantir que o ciclo de vida do código respeite a hierarquia de ambientes definida pela governança, bloqueando automaticamente Pull Requests que violem a sequencialidade (ex: tentar mergear uma *feature* direto em Produção).

## 🚀 Fluxo de Governança Definido

As regras configuradas neste repositório seguem um fluxo estrito de promoção de código:

1.  `✨ Feature/Fix` &rarr; 🛠️ **Development** _(dev, develop)_
2.  🛠️ **Development** &rarr; 🧪 **Staging** _(homol, staging)_
3.  🧪 **Staging** &rarr; 🚀 **Production** _(main, master)_

> **Regra de Ouro:** Qualquer tentativa de "furar fila" ou pular etapas (ex: `dev` &rarr; `main`) resultará no bloqueio imediato da PR.

## ⚙️ Como Funciona a Automação

O workflow `branch-flow.yml` é acionado em eventos de Pull Request (`opened`, `edited`, `synchronize`). O processo executa os seguintes passos:

1.  **Branch Flow Guard:** Analisa a origem (`head`) e o destino (`base`) da PR, gerando um relatório de conformidade em JSON.
2.  **Sticky Comment:** Um bot posta (ou atualiza) um comentário na PR com o status da validação, utilizando um ID único para evitar spam.
3.  **Governance Check:** Se o fluxo for inválido, o workflow falha propositalmente, impedindo o merge e exibindo orientações de correção nos logs e no comentário.

## 🧪 Cenários de Teste

Para validar as Actions, recomenda-se simular os seguintes cenários:

| Cenário | Origem (Head) | Destino (Base) | Resultado Esperado |
| :--- | :--- | :--- | :--- |
| **Integração Contínua** | `feature/*` | `develop` | ✅ **Autorizado** |
| **Promoção para Homol** | `develop` | `homol` | ✅ **Autorizado** |
| **Promoção para Prod** | `homol` | `main` | ✅ **Autorizado** |
| **Violação (Pular Etapa)** | `feature/*` | `main` | ⛔ **Bloqueado** |
| **Violação (Origem Inválida)** | `develop` | `main` | ⛔ **Bloqueado** |

## 🛠️ Stack

* **GitHub Actions:** Orquestração do pipeline de CI/CD.
* **[Malnati/branch-flow-guard](https://github.com/Malnati/branch-flow-guard):** Lógica de validação de fluxo e governança.
* **[Malnati/pr-comment](https://github.com/Malnati/pr-comment):** Renderização de templates Markdown e gerenciamento de comentários (*Sticky Mode*).

---
*Mantido por [Ricardo Malnati](https://github.com/Malnati)*

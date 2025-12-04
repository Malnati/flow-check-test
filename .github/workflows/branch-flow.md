## 🛡️ Branch Flow Guard

| Origem | Destino | Status |
| :---: | :---: | :---: |
| `{{head_branch}}` <br> _({{head_type}})_ | `{{base_branch}}` <br> _({{base_type}})_ | {{status_icon}} |

> **Resultado:** {{message}}

{{#if violation_code}}
⚠️ **Violação Detectada:** O código `{{violation_code}}` indica que esta regra é inegociável.
Por favor, feche esta PR e siga o fluxo correto.
{{/if}}

---
<small>Verificado automaticamente via Branch Flow Guard</small>

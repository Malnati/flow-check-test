## 🛡️ Branch Flow Guard

<div align="center">

| 🚦 Status | 🛫 Origem | 🛬 Destino |
| :---: | :---: | :---: |
| **{{ui.message_md}}** | `{{context.head_branch}}` | `{{context.base_branch}}` |

</div>

{{#unless compliance.allowed}}
> [!WARNING]
> **Atenção:** {{ui.message_md}}
>
> O código de violação é: `{{compliance.violation_code}}`.
{{/unless}}

{{#if compliance.allowed}}
> [!NOTE]
> Fluxo validado com sucesso em {{timestamp}}.
{{/if}}

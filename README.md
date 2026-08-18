# UI3 — Guia rápido de uso

Este README mostra como carregar a biblioteca UI3 e como adicionar um item simples na aba de configurações.

URL RAW usada neste exemplo:
https://raw.githubusercontent.com/cubodegelo1116/ui/refs/heads/main/ui3

1) Carregar a biblioteca

```lua
local rawUrl = "https://raw.githubusercontent.com/cubodegelo1116/ui/refs/heads/main/ui3"
local UI3 = loadstring(game:HttpGet(rawUrl))()

if not UI3 then
    error("UI3 não foi carregada. Verifique a URL raw e a permissão de HttpGet")
end
print("UI3 carregada com sucesso")
```

2) Adicionar um item rápido nas configurações

Tente estas opções (a biblioteca pode usar nomes diferentes):

```lua
local tabs = { UI3.U3SettingsTab, UI3.SettingsTab, UI3.Settings }
local added = false
for _, tab in ipairs(tabs) do
    if tab and type(tab.AddItem) == "function" then
        tab:AddItem({
            Name = "Meu item",
            Description = "Ação rápida",
            Callback = function()
                print("Meu item acionado")
                -- coloque aqui a ação desejada
            end,
        })
        added = true
        break
    end
end

if not added then
    warn("Aba de configurações não encontrada. Verifique os nomes na sua versão do UI3.")
end
```

Se a lib tiver AddToggle ou AddButton, use assim:

```lua
if UI3 and UI3.U3SettingsTab and type(UI3.U3SettingsTab.AddToggle) == "function" then
    UI3.U3SettingsTab:AddToggle({
        Name = "Ativar recurso",
        Default = false,
        Callback = function(value)
            print("Toggle mudou para", value)
        end,
    })
end
```

Boas práticas
- Use a URL RAW exata para garantir que `game:HttpGet` retorne o código correto.
- Teste em ambiente isolado antes de usar em scripts finais.
- Se precisar que eu ajuste os nomes dos métodos conforme o arquivo `ui3`, posso adaptar o exemplo.

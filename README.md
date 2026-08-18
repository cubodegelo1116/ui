# UI3 — Tutorial de Uso

Este README explica como carregar a biblioteca UI3 via um link RAW (usando loadstring) e como adicionar um item adicional na aba de configurações (U3SettingsTab).

> Observação: exemplos abaixo supõem um ambiente onde `loadstring(game:HttpGet(url))()` funciona (ex.: clientes/exploits que permitem HttpGet + loadstring). Ajuste a URL RAW para o caminho correto do arquivo `ui3.lua` no seu repositório.

## 1) Carregar a biblioteca via RAW + loadstring

Substitua `YOUR_RAW_URL_HERE` pela URL raw do arquivo UI3 no GitHub, por exemplo:
`https://raw.githubusercontent.com/<usuario>/<repo>/main/path/to/ui3.lua`

Exemplo:

```lua
local rawUrl = "https://raw.githubusercontent.com/USERNAME/REPO/main/ui3.lua" -- coloque sua URL raw aqui
local UI3 = loadstring(game:HttpGet(rawUrl))()
```

Depois de executar isso, `UI3` normalmente será a tabela/objeto retornado pela biblioteca. A API exata pode variar — veja a seção "Notas sobre API" abaixo.

## 2) Exemplo simples: verificar carregamento

```lua
if not UI3 then
    error("UI3 não foi carregada. Verifique a URL raw e a conexão HttpGet")
end
print("UI3 carregada com sucesso")
```

## 3) Adicionar um item à U3SettingsTab

Muitos wrappers de UI expõem uma aba de configurações ou um objeto `U3SettingsTab`. Abaixo há um padrão genérico para adicionar um item; adapte conforme a API real da UI3 que você está usando.

Exemplo genérico (seguro):

```lua
-- assume que UI3 já foi carregada e é uma tabela
local settingsTabCandidates = {
    UI3.U3SettingsTab, -- nome solicitado pelo autor
    UI3.SettingsTab,    -- alternativa comum
    UI3.Settings,       -- outra alternativa possível
}

local added = false
for _, tab in ipairs(settingsTabCandidates) do
    if tab and type(tab.AddItem) == "function" then
        tab:AddItem({
            Name = "Meu Item Extra",
            Description = "Descrição (opcional)",
            Callback = function()
                -- ação ao clicar/ativar o item
                print("Meu Item Extra acionado")
                -- coloque aqui a funcionalidade desejada
            end,
            -- você pode incluir outros campos aceitos pela lib (p.ex. Default, Type, Options, etc.)
        })
        added = true
        break
    end
end

if not added then
    warn("Não encontrei U3SettingsTab com método AddItem. Verifique a API da UI3 e ajuste o exemplo.")
end
```

Alternativa se a API for diferente (ex.: `AddToggle` / `AddButton`):

```lua
-- Exemplo: adicionar toggle, caso a biblioteca ofereça AddToggle
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

## 4) Boas práticas
- Use a URL raw exata (https://raw.githubusercontent.com/...) para garantir que `game:HttpGet` retorne o código correto.
- Teste em um ambiente isolado antes de usar em produção/versões finais.
- Se a biblioteca pedir configurações iniciais (p.ex. criar janela), siga a documentação da UI3 para criar a janela/aba antes de adicionar itens.

## 5) Notas sobre a API
Como diferentes forks/versões da UI3 podem ter APIs distintas, os exemplos acima são intencionalmente genéricos. Se você quiser, me diga o conteúdo do `ui3.lua` (ou o link raw) e eu adapto exemplos concretos com os nomes e parâmetros corretos da API.

---

Se desejar, posso:
- Atualizar este README com sua URL raw específica e exemplos prontos; ou
- Abrir um exemplo completo que cria uma janela, adiciona botões, toggles e registra a entrada nas configurações.


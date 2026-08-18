# UI3 — Guia Completo de Uso

Bem-vindo à **UI3**, uma biblioteca de UI avançada para Roblox scripts. Este guia mostra como usar todos os componentes e criar interfaces profissionais.

---

## 📥 1. Carregando a Biblioteca

```lua
local rawUrl = "https://raw.githubusercontent.com/cubodegelo1116/ui/refs/heads/main/ui3"
local UI3 = loadstring(game:HttpGet(rawUrl))()

if not UI3 then
    error("UI3 não foi carregada. Verifique a URL raw")
end

print("✓ UI3 carregada com sucesso!")
```

---

## 🪟 2. Criando uma Janela

```lua
-- Criar a janela principal
local Window = UI3.CreateWindow("Meu Script", "v1.0")

-- Window é o objeto raiz que contém abas e páginas
print("Janela criada: " .. Window.Name)
```

**Funcionalidades da Janela:**
- ✅ Arrastar pela barra de título
- ✅ Redimensionar pelo canto inferior direito
- ✅ Minimizar (−) e Fechar (×)
- ✅ Suporta temas personalizados

---

## 📑 3. Criando Abas

```lua
-- Criar abas dentro da janela
local TabHome = Window:AddTab("Home")
local TabSettings = Window:AddTab("Configurações")
local TabInfo = Window:AddTab("Informações")

-- Cada aba contém componentes
print("Abas criadas com sucesso!")
```

---

## 🎮 4. Componentes Disponíveis

### 📌 **AddButton** — Botão Clicável

```lua
local page = TabHome

AddButton(page, "Clique em mim!", function()
    print("Botão foi clicado!")
end)

AddButton(page, "Fazer algo", function()
    print("Executando ação...")
    -- Coloque sua lógica aqui
end)
```

**Características:**
- Hover effect (muda cor ao passar o mouse)
- Callback quando clicado
- Aparência profissional com bordas arredondadas

---

### 🔘 **AddToggle** — Interruptor On/Off

```lua
local page = TabSettings

local Toggle1 = AddToggle(page, "Ativar Recurso", false, function(value)
    print("Toggle mudou para: " .. tostring(value))
    
    if value then
        print("✓ Recurso ATIVADO")
    else
        print("✗ Recurso DESATIVADO")
    end
end)

-- Você também pode controlar o toggle programaticamente
-- Toggle1:SetState(true)   -- Força o estado ligado
-- local estado = Toggle1:GetState()  -- Pega o estado atual
```

**API do Toggle:**
- `SetState(boolean)` — Mudar o estado
- `GetState()` — Obter estado atual

---

### 📊 **AddSlider** — Controle Deslizante

```lua
local page = TabSettings

local Slider1 = AddSlider(page, "Velocidade", 0, 100, 50, function(value)
    print("Velocidade: " .. value)
end)

local Slider2 = AddSlider(page, "Volume", 0, 200, 100, function(value)
    print("Volume: " .. value .. "%")
end)

-- Você pode também controlar o slider programaticamente
-- Slider1:SetValue(75)
-- local valor = Slider1:GetValue()
```

**API do Slider:**
- `SetValue(number)` — Mudar o valor
- `GetValue()` — Obter valor atual

**Parâmetros:**
- `text` — Nome do slider
- `min` — Valor mínimo
- `max` — Valor máximo
- `default` — Valor inicial
- `callback` — Função chamada quando muda

---

### 📝 **AddTextLabel** — Texto Simples

```lua
local page = TabInfo

AddTextLabel(page, "Versão: 1.0")
AddTextLabel(page, "Autor: Seu Nome")
AddTextLabel(page, "Status: Ativo")
```

**Uso:** Mostrar informações textuais na UI.

---

### 📄 **AddParagraph** — Caixa de Informação

```lua
local page = TabInfo

AddParagraph(page, "Como Usar", "Esta é uma caixa de informação.\nVocê pode usar quebras de linha com \\n")

AddParagraph(page, "Aviso!", "Certifique-se de seguir as regras do servidor.")

AddParagraph(page, "Dicas", "1. Teste tudo antes de usar\n2. Leia os comentários do código\n3. Sempre salve seus scripts")
```

**Características:**
- Título em negrito
- Texto envolvido automaticamente
- Fundo com estilo de card

---

### 🎯 **AddDropdown** — Menu Suspenso

```lua
local page = TabSettings

AddDropdown(page, "Selecione", {"Opção 1", "Opção 2", "Opção 3"}, function(selected)
    print("Selecionado: " .. selected)
end)

AddDropdown(page, "Modo", {"Easy", "Normal", "Hard", "Insano"}, function(mode)
    print("Modo: " .. mode)
end)
```

**Características:**
- Abre lista de opções ao clicar
- Fecha automaticamente ao selecionar
- Mostra seleção atual no botão

---

### ⌨️ **AddTextBox** — Campo de Entrada

```lua
local page = TabSettings

AddTextBox(page, "Digite seu nome", "Padrão", function(text)
    print("Você digitou: " .. text)
end)

AddTextBox(page, "Comando", "", function(input)
    if input == "reset" then
        print("Resetando...")
    end
end)
```

**Características:**
- Aceita entrada do usuário
- Callback ao digitar
- Placeholder customizável

---

### ⏱️ **AddCooldownButton** — Botão com Tempo de Espera

```lua
local page = TabHome

AddCooldownButton(page, "Usar Poder", 5, function() -- 5 segundos de cooldown
    print("Poder ativado!")
    -- Lógica aqui
end)

AddCooldownButton(page, "Ataque Especial", 10, function()
    print("Atacando...")
end)
```

**Características:**
- Desativa automaticamente durante cooldown
- Mostra tempo restante
- Muda cor durante espera

---

## 🎨 5. Sistema de Temas

### Usando Temas Pré-definidos

```lua
local Window = UI3.CreateWindow("Meu Script", "v1.0")

-- Registrar um novo tema
Window:RegisterTheme("Dark", {
    Background = Color3.fromRGB(20, 20, 20),
    Button = Color3.fromRGB(40, 40, 40),
    Text = Color3.fromRGB(255, 255, 255),
    Accent = Color3.fromRGB(0, 150, 200),
})

-- Aplicar tema
Window:SetTheme("Dark")

-- Ou aplicar um tema customizado diretamente
Window:SetTheme({
    Background = Color3.fromRGB(15, 15, 15),
    Button = Color3.fromRGB(35, 35, 35),
    Text = Color3.fromRGB(200, 200, 200),
})
```

### Cores Disponíveis para Customizar

```lua
{
    Background = Color3.fromRGB(18, 28, 32),      -- Fundo da janela
    TitleBar = Color3.fromRGB(22, 35, 40),        -- Barra de título
    TabBackground = Color3.fromRGB(15, 24, 28),   -- Fundo das abas
    TabSelected = Color3.fromRGB(30, 50, 58),     -- Aba selecionada
    Button = Color3.fromRGB(28, 45, 52),          -- Botões
    ButtonHover = Color3.fromRGB(35, 55, 65),     -- Botão ao passar mouse
    Text = Color3.fromRGB(230, 240, 245),         -- Texto principal
    TextDark = Color3.fromRGB(140, 160, 170),     -- Texto secundário
    Accent = Color3.fromRGB(0, 180, 200),         -- Cor destaque
    ToggleOn = Color3.fromRGB(0, 190, 140),       -- Toggle ligado
    ToggleOff = Color3.fromRGB(45, 60, 68),       -- Toggle desligado
    Border = Color3.fromRGB(40, 65, 75),          -- Bordas
    Cooldown = Color3.fromRGB(160, 50, 50),       -- Botão em cooldown
    Error = Color3.fromRGB(220, 50, 50),          -- Erro (vermelho)
    Success = Color3.fromRGB(50, 200, 100),       -- Sucesso (verde)
    Warning = Color3.fromRGB(255, 200, 50),       -- Aviso (amarelo)
}
```

---

## 📚 6. Exemplo Completo de Script

```lua
-- Carregar UI3
local rawUrl = "https://raw.githubusercontent.com/cubodegelo1116/ui/refs/heads/main/ui3"
local UI3 = loadstring(game:HttpGet(rawUrl))()

if not UI3 then error("UI3 não carregou!") end

-- Criar janela
local Window = UI3.CreateWindow("Meu Admin Script", "v1.0")

-- ═══════════════════════════════════════════
-- ABA: HOME
-- ═══════════════════════════════════════════

local TabHome = Window:AddTab("Home")

AddButton(TabHome, "Teletransportar", function()
    print("Você será teletransportado...")
    -- local player = game.Players.LocalPlayer
    -- player.Character.HumanoidRootPart.CFrame = CFrame.new(0, 50, 0)
end)

AddButton(TabHome, "Damage", function()
    print("Dano aplicado!")
end)

-- ═══════════════════════════════════════════
-- ABA: CONFIGURAÇÕES
-- ═══════════════════════════════════════════

local TabSettings = Window:AddTab("Configurações")

local AutoAttack = AddToggle(TabSettings, "Auto Attack", false, function(enabled)
    if enabled then
        print("🔴 Auto Attack ATIVADO")
    else
        print("⚪ Auto Attack DESATIVADO")
    end
end)

local Speed = AddSlider(TabSettings, "Velocidade", 0, 100, 50, function(speed)
    print("Velocidade: " .. speed)
end)

AddDropdown(TabSettings, "Dificuldade", {"Fácil", "Normal", "Difícil"}, function(diff)
    print("Dificuldade: " .. diff)
end)

-- ═══════════════════════════════════════════
-- ABA: INFORMAÇÕES
-- ═══════════════════════════════════════════

local TabInfo = Window:AddTab("Informações")

AddTextLabel(TabInfo, "UI3 v2.0")
AddTextLabel(TabInfo, "Script criado por: Seu Nome")

AddParagraph(TabInfo, "Sobre este Script", 
    "Este é um script completo usando UI3.\n" ..
    "Contém vários componentes e funcionalidades.\n" ..
    "Sempre teste em um lugar seguro!"
)

-- ═══════════════════════════════════════════
-- TEMAS CUSTOMIZADOS
-- ═══════════════════════════════════════════

Window:RegisterTheme("Cyberpunk", {
    Background = Color3.fromRGB(10, 10, 20),
    Button = Color3.fromRGB(30, 30, 60),
    Accent = Color3.fromRGB(255, 0, 150),
    Text = Color3.fromRGB(0, 255, 200),
})

-- Para usar:
-- Window:SetTheme("Cyberpunk")

print("✓ Script carregado com sucesso!")
```

---

## 🔑 Dicas de Boas Práticas

### ✅ DO's

```lua
-- ✓ Validar entrada do usuário
AddTextBox(page, "Nome", "", function(text)
    if text and #text > 0 then
        print("Nome válido: " .. text)
    else
        print("Nome inválido!")
    end
end)

-- ✓ Usar callback para reagir a mudanças
local Toggle = AddToggle(page, "Feature", false, function(value)
    if value then
        -- Fazer algo
    end
end)

-- ✓ Organizar com abas
local Tab1 = Window:AddTab("Principal")
local Tab2 = Window:AddTab("Avançado")
```

### ❌ DON'Ts

```lua
-- ✗ Criar muitas janelas
-- local Window1 = UI3.CreateWindow(...)
-- local Window2 = UI3.CreateWindow(...)
-- Uma janela com abas é suficiente!

-- ✗ Esquecer de validar
AddTextBox(page, "Número", "", function(text)
    -- ✗ local num = tonumber(text)  -- Pode ser nil!
    -- ✓ Faça assim:
    local num = tonumber(text) or 0
end)
```

---

## 🚀 Recursos Adicionais

- **Animações Suaves:** Todos os componentes usam tweening automático
- **Responsividade:** A UI se adapta ao tamanho da tela
- **Dark Theme Padrão:** Esteticamente agradável e profissional
- **ZIndex Management:** Gerenciamento automático de profundidade

---

## ❓ FAQ

**P: Como mudo o tamanho da janela?**  
R: Arraste pelo canto inferior direito! Ou modifique no código:

```lua
Main.Size = UDim2.new(0, 520, 0, 380)  -- Largura, Altura
```

**P: Posso ter múltiplas janelas?**  
R: Tecnicamente sim, mas recomenda-se 1 janela com várias abas.

**P: Como removo a UI?**  
R: Clique o botão `×` na barra de título.

**P: Posso adicionar ícones aos botões?**  
R: No momento, use emojis no texto: `AddButton(page, "🔓 Abrir", callback)`

---

## 📝 Changelog

**v2.0** (2026)
- ✨ Sistema de temas melhorado
- ✨ Novos componentes (Dropdown, TextBox, etc)
- 🐛 Fixes de performance
- 🎨 UI mais polida

---

Feito com ❤️ por PDDEV / RCCDEV

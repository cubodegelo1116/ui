Claro. Fiz bem simples, direto e com exemplos pequenos. Sem emoji e sem texto com cara de documentação automática.

````md
# UI3

Uma biblioteca simples para criar interfaces no Roblox usando Luau.

## Como começar

Primeiro, carregue a biblioteca:

```lua
local UI = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/cubodegelo1116/ui/refs/heads/main/ui3"
))()
````

Depois crie sua janela:

```lua
local Window = UI.CreateWindow("Meu Hub", "by PDDev")
```

O primeiro texto é o título.

O segundo texto é o subtítulo. Ele é opcional.

---

# Criando uma Tab

Para criar uma aba:

```lua
local Main = Window:CreateTab("Main")
```

Agora você pode colocar componentes dentro dela.

---

# Button

Um botão é feito assim:

```lua
Main:AddButton("Clique aqui", function()
    print("Clicou!")
end)
```

Quando o jogador clicar no botão, o código dentro do `function` será executado.

---

# Toggle

Toggle é um botão que pode ficar ligado ou desligado:

```lua
Main:AddToggle("Speed", false, function(state)
    print(state)
end)
```

`false` significa que começa desligado.

Se quiser começar ligado:

```lua
Main:AddToggle("Speed", true, function(state)
    print(state)
end)
```

O `state` será:

```lua
true
```

ou:

```lua
false
```

---

# Slider

Slider serve para escolher um número:

```lua
Main:AddSlider("WalkSpeed", 16, 100, 16, function(value)
    print(value)
end)
```

A ordem é:

```lua
"Nome", mínimo, máximo, valor inicial, função
```

Por exemplo:

```lua
Main:AddSlider("Power", 0, 500, 100, function(value)
    print("Power:", value)
end)
```

---

# TextLabel

Para colocar um texto:

```lua
Main:AddTextLabel("Meu texto")
```

---

# Paragraph

Paragraph serve para colocar um título e um texto maior:

```lua
Main:AddParagraph(
    "Informação",
    "Esse é um texto explicando alguma coisa."
)
```

---

# Dropdown

Dropdown serve para escolher uma opção:

```lua
local Dropdown = Main:AddDropdown(
    "Player",
    {"Player1", "Player2", "Player3"},
    function(value)
        print(value)
    end
)
```

Quando o jogador escolher uma opção, `value` vai receber o nome escolhido.

## Alterar as opções

Você pode trocar as opções depois:

```lua
Dropdown.SetOptions({
    "Player1",
    "Player2",
    "Player3",
    "Player4"
})
```

## Escolher uma opção pelo código

```lua
Dropdown.SetValue("Player2")
```

## Ver a opção escolhida

```lua
print(Dropdown.GetValue())
```

## Ver todas as opções

```lua
local options = Dropdown.GetOptions()
```

---

# TextBox

TextBox serve para o jogador digitar alguma coisa:

```lua
Main:AddTextBox("Digite aqui", function(text)
    print(text)
end)
```

O `text` contém o que o jogador digitou.

---

# Cooldown Button

É um botão que possui cooldown:

```lua
Main:AddCooldownButton("Executar", 5, function()
    print("Executou")
end)
```

O `5` significa 5 segundos de cooldown.

---

# Mais de uma Tab

Você pode criar quantas tabs quiser:

```lua
local Main = Window:CreateTab("Main")
local Player = Window:CreateTab("Player")
local Settings = Window:CreateTab("Settings")
```

Depois coloque os componentes na tab que quiser:

```lua
Main:AddButton("Button", function()
    print("Main")
end)

Player:AddSlider("Speed", 16, 100, 16, function(value)
    print(value)
end)

Settings:AddToggle("Enabled", false, function(state)
    print(state)
end)
```

---

# Botão de minimizar

Você pode adicionar um botão flutuante para minimizar a UI:

```lua
UI.AddMinimizeButton()
```

Também dá para configurar:

```lua
UI.AddMinimizeButton({
    Image = "rbxassetid://7733960981",
    Size = 50,
    ImageSize = 28
})
```

---

# Themes

A UI já possui temas.

Para usar um tema:

```lua
UI.SetTheme("Neon")
```

Para ver os temas disponíveis:

```lua
print(UI.GetAllThemes())
```

Você também pode criar seu próprio tema:

```lua
UI.RegisterTheme("MeuTema", {
    Background = Color3.fromRGB(20, 20, 20),
    Button = Color3.fromRGB(30, 30, 30),
    Text = Color3.fromRGB(255, 255, 255),
    Accent = Color3.fromRGB(0, 170, 255)
})
```

Depois:

```lua
UI.SetTheme("MeuTema")
```

---

# Settings Tab

A biblioteca possui uma tab de Settings separada.

Loadstring:

```lua
local SettingsTab = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/cubodegelo1116/ui/refs/heads/main/ui3settingtab"
))()
```

Use a Settings Tab junto com a UI3 para adicionar as funções de configuração disponíveis nela.

---

# Exemplo completo

Se você só quer fazer uma UI simples, pode começar com isso:

```lua
local UI = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/cubodegelo1116/ui/refs/heads/main/ui3"
))()

local Window = UI.CreateWindow("Meu Hub", "by PDDev")

local Main = Window:CreateTab("Main")

Main:AddParagraph(
    "Bem-vindo",
    "Essa é minha primeira UI usando a UI3."
)

Main:AddButton("Testar", function()
    print("Funcionou!")
end)

Main:AddToggle("Enabled", false, function(state)
    print("Enabled:", state)
end)

Main:AddSlider("Speed", 16, 100, 16, function(value)
    print("Speed:", value)
end)

Main:AddDropdown(
    "Mode",
    {"Normal", "Fast", "Extreme"},
    function(value)
        print("Mode:", value)
    end
)

Main:AddTextBox("Digite algo", function(text)
    print("Texto:", text)
end)

Main:AddCooldownButton("Execute", 3, function()
    print("Executado!")
end)

UI.AddMinimizeButton()
```


Esse já fica bem mais "README de dev": simples, sem enrolação e com o cara conseguindo montar uma UI inteira só copiando os exemplos.
```

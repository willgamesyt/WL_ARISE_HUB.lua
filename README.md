-- WL ARISE HUB | by willgamesyt
-- Estilo Solo Leveling com IA, Auto Farm, Raids, ESP, etc.

local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/shlexware/Orion/main/source"))()
local Window = OrionLib:MakeWindow({
    Name = "WL ARISE HUB | by willgamesyt",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "WLAriseCrossover"
})

-- Tela de Carregamento
local LoadingScreen = Instance.new("ScreenGui", game.CoreGui)
local Frame = Instance.new("Frame", LoadingScreen)
Frame.Size = UDim2.new(0, 400, 0, 200)
Frame.Position = UDim2.new(0.5, -200, 0.5, -100)
Frame.BackgroundTransparency = 0.2
Frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
local Label = Instance.new("TextLabel", Frame)
Label.Size = UDim2.new(1, 0, 1, 0)
Label.Text = "Carregando WL ARISE HUB..."
Label.TextColor3 = Color3.fromRGB(255, 255, 255)
Label.BackgroundTransparency = 1
Label.Font = Enum.Font.GothamBold
Label.TextSize = 22
wait(2)
LoadingScreen:Destroy()

-- Funções auxiliares
local function Notify(title, text)
    OrionLib:MakeNotification({Name = title, Content = text, Time = 3})
end

-- [1] Aba Farm / Raid Winter
local FarmTab = Window:MakeTab({Name = "Farm/Raid Winter ❄️", Icon = "", PremiumOnly = false})
FarmTab:AddToggle({
    Name = "Auto Click (Potente)",
    Default = false,
    Callback = function(v)
        getgenv().AutoClick = v
        while getgenv().AutoClick and wait(0.1) do
            pcall(function()
                mouse1click()
            end)
        end
    end
})
FarmTab:AddDropdown({
    Name = "Selecionar Ilha para Farm",
    Options = {"Ilha do Gelo", "Ilha da Lava", "Ilha Sombria"},
    Callback = function(option)
        getgenv().IslandChoice = option
    end
})
FarmTab:AddDropdown({
    Name = "NPCs para atacar",
    Options = {"Pequeno", "Grande"},
    Callback = function(option)
        getgenv().NPCType = option
    end
})
FarmTab:AddToggle({
    Name = "Farmar Dinheiro",
    Default = false,
    Callback = function(v)
        getgenv().FarmMoney = v
        -- lógica de farm seria colocada aqui
    end
})
FarmTab:AddToggle({
    Name = "Detectar Raid do Gelo e ir automaticamente",
    Default = false,
    Callback = function(v)
        getgenv().AutoIceRaid = v
    end
})
FarmTab:AddDropdown({
    Name = "Ao obter sombra:",
    Options = {"ARISE", "Distribuir"},
    Callback = function(v)
        getgenv().ShadowOption = v
    end
})

-- [2] Aba Vender / Trocar
local TradeTab = Window:MakeTab({Name = "Vender/Trocar 💀", Icon = "", PremiumOnly = false})
TradeTab:AddDropdown({
    Name = "Selecionar Rank da Sombra para Vender",
    Options = {"E", "D", "C", "B", "A", "S"},
    Callback = function(rank)
        getgenv().SellShadowRank = rank
    end
})
TradeTab:AddButton({
    Name = "Vender Sombras Selecionadas",
    Callback = function()
        -- lógica de venda
    end
})
TradeTab:AddDropdown({
    Name = "Trocar Pó por Rank",
    Options = {"Comum", "Raro", "Lendário"},
    Callback = function(r)
        getgenv().DustTrade = r
    end
})

-- [3] Aba Raids
local RaidTab = Window:MakeTab({Name = "Raids 🏰", Icon = "", PremiumOnly = false})
RaidTab:AddDropdown({
    Name = "Selecionar Rank da Raid",
    Options = {"E", "D", "C", "B", "A", "S", "SS"},
    Callback = function(rank)
        getgenv().RaidRank = rank
    end
})
RaidTab:AddToggle({
    Name = "Farmar qualquer Raid no mapa",
    Default = false,
    Callback = function(v)
        getgenv().AutoAnyRaid = v
    end
})
RaidTab:AddToggle({
    Name = "Farmar Castelo Infernal",
    Default = false,
    Callback = function(v)
        getgenv().InfernalCastle = v
    end
})
RaidTab:AddToggle({
    Name = "Fazer Raid do Beru",
    Default = false,
    Callback = function(v)
        getgenv().BeruRaid = v
    end
})

-- [4] Aba Teleporte
local TeleportTab = Window:MakeTab({Name = "Teleporte 🌍", Icon = "", PremiumOnly = false})
TeleportTab:AddDropdown({
    Name = "Ir para ilha:",
    Options = {"Gelo", "Lava", "Sombra", "Raids", "Castelo"},
    Callback = function(option)
        -- lógica de teleporte
    end
})

-- [5] Aba Configurações
local SettingsTab = Window:MakeTab({Name = "Configurações ⚙️", Icon = "", PremiumOnly = false})
SettingsTab:AddButton({Name = "Resetar Script", Callback = function() OrionLib:Destroy() end})
SettingsTab:AddButton({Name = "Salvar Configuração", Callback = function() OrionLib:SaveConfig() end})
SettingsTab:AddToggle({Name = "Boost de FPS", Default = false, Callback = function() -- código FPS end})
SettingsTab:AddToggle({Name = "Ativar RTX + Anti Lag", Default = false, Callback = function() -- gráfico top end})

-- [6] Aba ESP
local ESPTab = Window:MakeTab({Name = "ESP 👁️", Icon = "", PremiumOnly = false})
ESPTab:AddToggle({Name = "ESP para Jogadores", Default = false, Callback = function() end})
ESPTab:AddToggle({Name = "ESP para Ilhas", Default = false, Callback = function() end})
ESPTab:AddToggle({Name = "ESP para Montarias", Default = false, Callback = function() end})

-- [7] Aba IA Assistente
local IATab = Window:MakeTab({Name = "IA Assistente 🤖", Icon = "", PremiumOnly = false})
IATab:AddTextbox({
    Name = "Pergunte algo sobre o jogo:",
    Default = "",
    TextDisappear = false,
    Callback = function(input)
        Notify("IA diz:", "Essa parte ainda está em construção, mas aqui virá uma resposta sobre ARISE CROSSOVER!")
    end
})

-- Script Proteções ativas automaticamente
getgenv().AntiLag = true
getgenv().AntiAFK = true
getgenv().AntiBan = true
getgenv().AntiBug = true
getgenv().AntiDetect = true

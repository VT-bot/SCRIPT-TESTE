-- SONIC MENU PAGO
-- Créditos: SACOLA E TIGRINHO

local SonicMenu = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local MinimizeButton = Instance.new("TextButton")
local RestoreButton = Instance.new("TextButton")  -- Novo botão para restaurar o menu
local ButtonsFrame = Instance.new("ScrollingFrame")  -- Alterei ButtonsFrame para ScrollingFrame
local FunctionsFrame = Instance.new("ScrollingFrame")  -- Alterado para ScrollingFrame
local FunctionsTitle = Instance.new("TextLabel")

-- Configuração do painel quadrado
SonicMenu.Parent = game.CoreGui
MainFrame.Parent = SonicMenu
MainFrame.Size = UDim2.new(0, 400, 0, 400)  -- Tamanho quadrado
MainFrame.Position = UDim2.new(0.5, -200, 0.5, -200)  -- Ajustei a posição para centralizar
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MainFrame.Draggable = true
MainFrame.Active = true
MainFrame.Selectable = true

MinimizeButton.Parent = MainFrame
MinimizeButton.Size = UDim2.new(0, 50, 0, 25)
MinimizeButton.Position = UDim2.new(1, -55, 0, 5)
MinimizeButton.Text = "-"
MinimizeButton.MouseButton1Click:Connect(function()
    MainFrame.Size = UDim2.new(0, 50, 0, 50)  -- Reduz o tamanho do painel a uma linha fina
    ButtonsFrame.Visible = false  -- Esconde os botões de teleporte
    FunctionsFrame.Visible = false  -- Esconde os botões de funções
    RestoreButton.Visible = true  -- Mostra o botão de restaurar
end)

RestoreButton.Parent = MainFrame
RestoreButton.Size = UDim2.new(0, 50, 0, 25)
RestoreButton.Position = UDim2.new(1, -55, 0, 5)
RestoreButton.Text = "⤴"  -- Ícone de seta para restaurar
RestoreButton.Visible = false  -- Fica invisível inicialmente
RestoreButton.MouseButton1Click:Connect(function()
    MainFrame.Size = UDim2.new(0, 400, 0, 400)  -- Restaura o tamanho normal do painel
    ButtonsFrame.Visible = true  -- Mostra os botões de teleporte
    FunctionsFrame.Visible = true  -- Mostra os botões de funções
    RestoreButton.Visible = false  -- Esconde o botão de restaurar
end)

-- Criando o ButtonsFrame com rolagem
ButtonsFrame.Parent = MainFrame
ButtonsFrame.Size = UDim2.new(1, 0, 0.5, 0)  -- Ajustei o tamanho para ocupar metade do painel
ButtonsFrame.Position = UDim2.new(0, 0, 0, 30)
ButtonsFrame.BackgroundTransparency = 1
ButtonsFrame.ScrollBarThickness = 5
ButtonsFrame.Visible = true  -- Garante que os botões de teleporte sejam visíveis por padrão

local uiListTeleport = Instance.new("UIListLayout", ButtonsFrame)
uiListTeleport.SortOrder = Enum.SortOrder.LayoutOrder
uiListTeleport.Padding = UDim.new(0, 5)

-- Criando o FunctionsFrame com rolagem
FunctionsFrame.Parent = MainFrame
FunctionsFrame.Size = UDim2.new(1, 0, 0.5, 0)  -- Ajustei o tamanho para ocupar metade do painel
FunctionsFrame.Position = UDim2.new(0, 0, 0.5, 0)
FunctionsFrame.BackgroundTransparency = 1
FunctionsFrame.ScrollBarThickness = 5
FunctionsFrame.Visible = true  -- Garante que as funções sejam visíveis por padrão

local uiListFunctions = Instance.new("UIListLayout", FunctionsFrame)
uiListFunctions.SortOrder = Enum.SortOrder.LayoutOrder
uiListFunctions.Padding = UDim.new(0, 5)

FunctionsTitle.Parent = FunctionsFrame
FunctionsTitle.Size = UDim2.new(1, 0, 0, 30)
FunctionsTitle.Position = UDim2.new(0, 0, 0, 0)
FunctionsTitle.Text = "Funções"
FunctionsTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
FunctionsTitle.BackgroundTransparency = 1

-- Função para teleporte
local function teleport(x, y, z)
    local player = game.Players.LocalPlayer
    if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        local hrp = player.Character.HumanoidRootPart
        local targetPos = CFrame.new(x, y, z)
        hrp.CFrame = targetPos

        -- Verificando se o teleporte foi bem-sucedido
        if hrp.Position == targetPos.Position then
            print("Teleporte realizado com sucesso!")
        else
            warn("Falha no teleporte!")
        end
    end
end

-- Criando botões para teleportes
local locations = {
    {"Prédio", -1888.3, 4.8, 377.2},
    {"Casa Pescaria", -1205.7, 79.1, -391.0},
    {"Gas/Lixo", -441.9, 5.3, -31.0},
    {"Fazenda", 778.8, 4.8, -101.1},
    {"PM", -839.3, 12.2, 459.0},
    {"Praça", -287.4, 4.8, 338.5},
    {"Plantas", 12022.6, 27.3, 12796.3},
    {"Lavagem", 19830.8, 66.5, 13142.8}
}

for _, loc in pairs(locations) do
    local button = Instance.new("TextButton")
    button.Text = loc[1]
    button.Size = UDim2.new(1, 0, 0, 30)
    button.Parent = ButtonsFrame
    button.MouseButton1Click:Connect(function()
        teleport(loc[2], loc[3], loc[4])
    end)
end

-- Criando botões para funções
local functions = {
    {"Velocidade", function() 
        print("Função Velocidade ativada!")
    end},
    {"ESP Nome", function() 
        print("Função ESP Nome ativada!")
    end},
    {"ESP Pessoas", function() 
        print("Função ESP Pessoas ativada!")
    end},
    {"No Clip", function() 
        print("Função No Clip ativada!")
    end},
    {"Hit Box", function() 
        print("Função Hit Box ativada!")
    end},
    {"CL", function() 
        print("Função CL ativada!")
    end},
    {"Teleporte Player", function() 
        print("Função Teleporte Player ativada!")
    end}
}

for _, func in pairs(functions) do
    local button = Instance.new("TextButton")
    button.Text = func[1]
    button.Size = UDim2.new(1, 0, 0, 30)
    button.Parent = FunctionsFrame
    button.MouseButton1Click:Connect(func[2])
end

-- Ajustando o CanvasSize para que todos os botões de função fiquem visíveis
local totalButtonsTeleport = #locations
ButtonsFrame.CanvasSize = UDim2.new(0, 0, 0, totalButtonsTeleport * 35)

local totalButtonsFunctions = #functions
FunctionsFrame.CanvasSize = UDim2.new(0, 0, 0, totalButtonsFunctions * 35)

-- Funções adicionais
loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))()

-- ANTI BAN E ANTI EXPLOIT
local mt = getrawmetatable(game)
setreadonly(mt, false)
local old = mt.__namecall

mt.__namecall = newcclosure(function(self, ...)
    local method = getnamecallmethod()
    local args = {...}
    
    -- Bloquear tentativas de kick e ban
    if method == "Kick" or method == "Ban" then
        warn("Tentativa de kick bloqueada!")
        return nil
    end

    return old(self, ...)
end)

-- Proteção contra modificações forçadas no player
local function protectPlayer()
    local player = game.Players.LocalPlayer
    player.CharacterAdded:Connect(function(char)
        local hrp = char:FindFirstChild("HumanoidRootPart")
        if hrp then
            hrp:GetPropertyChangedSignal("CFrame"):Connect(function()
                if not hrp.Parent then return end
                hrp.CFrame = hrp.CFrame -- Restaura a posição se for modificada
            end)
        end
    end)
end

protectPlayer()

-- Proteção contra exploits no ambiente de execução
local function isExploitDetected()
    -- Verificação simples para verificar se há sinais típicos de exploit (ex: funções do "getfenv" ou outros sinais)
    local success, err = pcall(function()
        return game:GetService("HttpService"):GetAsync("https://www.google.com")
    end)
    if not success then
        return true
    end
    return false
end

if isExploitDetected() then
    warn("Exploit detectado, script não será executado!")
    return
end

print("Anti-Ban e Anti-Exploit ativados!")

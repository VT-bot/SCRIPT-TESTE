-- SONIC MENU PAGO
-- Créditos: SACOLA E TIGRINHO

local SonicMenu = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local MinimizeButton = Instance.new("TextButton")
local RestoreButton = Instance.new("TextButton")
local ButtonsFrame = Instance.new("ScrollingFrame")
local FunctionsFrame = Instance.new("ScrollingFrame")
local FunctionsTitle = Instance.new("TextLabel")

-- Configuração do painel principal
SonicMenu.Parent = game.CoreGui
MainFrame.Parent = SonicMenu
MainFrame.Size = UDim2.new(0, 450, 0, 500)
MainFrame.Position = UDim2.new(0.5, -225, 0.5, -250)
MainFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
MainFrame.BorderSizePixel = 2
MainFrame.Draggable = true
MainFrame.Active = true
MainFrame.Selectable = true
MainFrame.BackgroundTransparency = 0.2

-- Botão Minimizar
MinimizeButton.Parent = MainFrame
MinimizeButton.Size = UDim2.new(0, 50, 0, 25)
MinimizeButton.Position = UDim2.new(1, -55, 0, 5)
MinimizeButton.Text = "-"
MinimizeButton.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
MinimizeButton.MouseButton1Click:Connect(function()
    MainFrame.Size = UDim2.new(0, 50, 0, 50)
    ButtonsFrame.Visible = false
    FunctionsFrame.Visible = false
    RestoreButton.Visible = true
end)

-- Botão Restaurar
RestoreButton.Parent = MainFrame
RestoreButton.Size = UDim2.new(0, 50, 0, 25)
RestoreButton.Position = UDim2.new(1, -55, 0, 5)
RestoreButton.Text = "⤴"
RestoreButton.Visible = false
RestoreButton.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
RestoreButton.MouseButton1Click:Connect(function()
    MainFrame.Size = UDim2.new(0, 450, 0, 500)
    ButtonsFrame.Visible = true
    FunctionsFrame.Visible = true
    RestoreButton.Visible = false
end)

-- Configuração do painel de botões
ButtonsFrame.Parent = MainFrame
ButtonsFrame.Size = UDim2.new(1, 0, 0.5, -10)
ButtonsFrame.Position = UDim2.new(0, 0, 0, 40)
ButtonsFrame.BackgroundTransparency = 1
ButtonsFrame.ScrollBarThickness = 5

-- Layout dos botões
local uiListTeleport = Instance.new("UIListLayout", ButtonsFrame)
uiListTeleport.SortOrder = Enum.SortOrder.LayoutOrder
uiListTeleport.Padding = UDim.new(0, 5)

-- Configuração do painel de funções
FunctionsFrame.Parent = MainFrame
FunctionsFrame.Size = UDim2.new(1, 0, 0.5, -10)
FunctionsFrame.Position = UDim2.new(0, 0, 0.5, 0)
FunctionsFrame.BackgroundTransparency = 1
FunctionsFrame.ScrollBarThickness = 5

-- Layout das funções
local uiListFunctions = Instance.new("UIListLayout", FunctionsFrame)
uiListFunctions.SortOrder = Enum.SortOrder.LayoutOrder
uiListFunctions.Padding = UDim.new(0, 5)

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
    button.Size = UDim2.new(1, 0, 0, 40)
    button.Parent = ButtonsFrame
    button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.MouseButton1Click:Connect(function()
        local player = game.Players.LocalPlayer
        if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(loc[2], loc[3], loc[4])
        end
    end)
end

-- Criando botões para funções
local functions = {
    {"Velocidade", function() print("Velocidade ativada!") end},
    {"ESP Nome", function() print("ESP Nome ativada!") end},
    {"ESP Pessoas", function() print("ESP Pessoas ativada!") end},
    {"No Clip", function() print("No Clip ativado!") end},
    {"Hit Box", function() print("Hit Box ativado!") end},
    {"CL", function() print("CL ativado!") end},
    {"Teleporte Player", function() print("Teleporte Player ativado!") end}
}

for _, func in pairs(functions) do
    local button = Instance.new("TextButton")
    button.Text = func[1]
    button.Size = UDim2.new(1, 0, 0, 40)
    button.Parent = FunctionsFrame
    button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.MouseButton1Click:Connect(func[2])
end

-- Ajustando a rolagem
ButtonsFrame.CanvasSize = UDim2.new(0, 0, 0, #locations * 45)
FunctionsFrame.CanvasSize = UDim2.new(0, 0, 0, #functions * 45)

print("Menu organizado e estilizado com sucesso!")

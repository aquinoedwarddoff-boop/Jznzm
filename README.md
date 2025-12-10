-- Script GUI com Abas para Roblox
-- Cole este script no StarterGui ou StarterPlayerScripts

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Criar ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "TabSystem"
screenGui.ResetOnSpawn = false
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = playerGui

-- Frame Principal
local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 500, 0, 400)
mainFrame.Position = UDim2.new(0.5, -250, 0.5, -200)
mainFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Parent = screenGui

-- Arredondar cantos
local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 12)
mainCorner.Parent = mainFrame

-- Título
local title = Instance.new("TextLabel")
title.Name = "Title"
title.Size = UDim2.new(1, 0, 0, 40)
title.BackgroundColor3 = Color3.fromRGB(45, 45, 55)
title.BorderSizePixel = 0
title.Font = Enum.Font.GothamBold
title.Text = "🎮 MEU SCRIPT ÉPICO"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.TextSize = 18
title.Parent = mainFrame

local titleCorner = Instance.new("UICorner")
titleCorner.CornerRadius = UDim.new(0, 12)
titleCorner.Parent = title

-- Botão Fechar
local closeBtn = Instance.new("TextButton")
closeBtn.Name = "CloseButton"
closeBtn.Size = UDim2.new(0, 30, 0, 30)
closeBtn.Position = UDim2.new(1, -35, 0, 5)
closeBtn.BackgroundColor3 = Color3.fromRGB(220, 50, 50)
closeBtn.BorderSizePixel = 0
closeBtn.Font = Enum.Font.GothamBold
closeBtn.Text = "X"
closeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
closeBtn.TextSize = 16
closeBtn.Parent = title

local closeBtnCorner = Instance.new("UICorner")
closeBtnCorner.CornerRadius = UDim.new(0, 8)
closeBtnCorner.Parent = closeBtn

closeBtn.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)

-- Container das Abas
local tabContainer = Instance.new("Frame")
tabContainer.Name = "TabContainer"
tabContainer.Size = UDim2.new(1, -20, 0, 45)
tabContainer.Position = UDim2.new(0, 10, 0, 50)
tabContainer.BackgroundTransparency = 1
tabContainer.Parent = mainFrame

local tabLayout = Instance.new("UIListLayout")
tabLayout.FillDirection = Enum.FillDirection.Horizontal
tabLayout.HorizontalAlignment = Enum.HorizontalAlignment.Left
tabLayout.Padding = UDim.new(0, 5)
tabLayout.Parent = tabContainer

-- Container do Conteúdo
local contentContainer = Instance.new("Frame")
contentContainer.Name = "ContentContainer"
contentContainer.Size = UDim2.new(1, -20, 1, -115)
contentContainer.Position = UDim2.new(0, 10, 0, 105)
contentContainer.BackgroundColor3 = Color3.fromRGB(45, 45, 55)
contentContainer.BorderSizePixel = 0
contentContainer.Parent = mainFrame

local contentCorner = Instance.new("UICorner")
contentCorner.CornerRadius = UDim.new(0, 10)
contentCorner.Parent = contentContainer

-- Função para criar Aba
local function createTab(name, icon)
    local tab = Instance.new("TextButton")
    tab.Name = name .. "Tab"
    tab.Size = UDim2.new(0, 110, 0, 35)
    tab.BackgroundColor3 = Color3.fromRGB(55, 55, 65)
    tab.BorderSizePixel = 0
    tab.Font = Enum.Font.GothamSemibold
    tab.Text = icon .. " " .. name
    tab.TextColor3 = Color3.fromRGB(200, 200, 200)
    tab.TextSize = 14
    tab.Parent = tabContainer
    
    local tabCorner = Instance.new("UICorner")
    tabCorner.CornerRadius = UDim.new(0, 8)
    tabCorner.Parent = tab
    
    return tab
end

-- Função para criar Conteúdo
local function createContent(name)
    local content = Instance.new("ScrollingFrame")
    content.Name = name .. "Content"
    content.Size = UDim2.new(1, 0, 1, 0)
    content.BackgroundTransparency = 1
    content.BorderSizePixel = 0
    content.ScrollBarThickness = 6
    content.Visible = false
    content.Parent = contentContainer
    
    local contentLayout = Instance.new("UIListLayout")
    contentLayout.Padding = UDim.new(0, 8)
    contentLayout.Parent = content
    
    return content
end

-- Criar Abas
local homeTab = createTab("Home", "🏠")
local playerTab = createTab("Player", "👤")
local gameTab = createTab("Game", "🎮")
local miscTab = createTab("Misc", "⚙️")

-- Criar Conteúdos
local homeContent = createContent("Home")
local playerContent = createContent("Player")
local gameContent = createContent("Game")
local miscContent = createContent("Misc")

-- Função para criar Botão
local function createButton(parent, text, callback)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -20, 0, 35)
    btn.BackgroundColor3 = Color3.fromRGB(70, 130, 255)
    btn.BorderSizePixel = 0
    btn.Font = Enum.Font.Gotham
    btn.Text = text
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.TextSize = 14
    btn.Parent = parent
    
    local btnCorner = Instance.new("UICorner")
    btnCorner.CornerRadius = UDim.new(0, 8)
    btnCorner.Parent = btn
    
    btn.MouseButton1Click:Connect(callback)
    
    return btn
end

-- Adicionar padding aos conteúdos
for _, content in pairs({homeContent, playerContent, gameContent, miscContent}) do
    local padding = Instance.new("UIPadding")
    padding.PaddingTop = UDim.new(0, 10)
    padding.PaddingLeft = UDim.new(0, 10)
    padding.PaddingRight = UDim.new(0, 10)
    padding.Parent = content
end

-- Conteúdo Home
createButton(homeContent, "✨ Bem-vindo ao Script!", function()
    print("Script carregado com sucesso!")
end)

-- Conteúdo Player
createButton(playerContent, "⚡ Speed Boost", function()
    player.Character.Humanoid.WalkSpeed = 50
end)

createButton(playerContent, "🦘 Jump Boost", function()
    player.Character.Humanoid.JumpPower = 100
end)

createButton(playerContent, "🔄 Reset Stats", function()
    player.Character.Humanoid.WalkSpeed = 16
    player.Character.Humanoid.JumpPower = 50
end)

-- Conteúdo Game
createButton(gameContent, "💰 Farm Coins (exemplo)", function()
    print("Iniciando farm de coins...")
end)

createButton(gameContent, "📦 Teleport to Spawn", function()
    if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        player.Character.HumanoidRootPart.CFrame = CFrame.new(0, 50, 0)
    end
end)

-- Conteúdo Misc
createButton(miscContent, "🌙 Toggle UI", function()
    mainFrame.Visible = not mainFrame.Visible
end)

createButton(miscContent, "❌ Destroy Script", function()
    screenGui:Destroy()
end)

-- Sistema de Troca de Abas
local function switchTab(selectedTab, selectedContent)
    for _, tab in pairs(tabContainer:GetChildren()) do
        if tab:IsA("TextButton") then
            tab.BackgroundColor3 = Color3.fromRGB(55, 55, 65)
            tab.TextColor3 = Color3.fromRGB(200, 200, 200)
        end
    end
    
    for _, content in pairs(contentContainer:GetChildren()) do
        if content:IsA("ScrollingFrame") then
            content.Visible = false
        end
    end
    
    selectedTab.BackgroundColor3 = Color3.fromRGB(70, 130, 255)
    selectedTab.TextColor3 = Color3.fromRGB(255, 255, 255)
    selectedContent.Visible = true
end

-- Conectar eventos das abas
homeTab.MouseButton1Click:Connect(function() switchTab(homeTab, homeContent) end)
playerTab.MouseButton1Click:Connect(function() switchTab(playerTab, playerContent) end)
gameTab.MouseButton1Click:Connect(function() switchTab(gameTab, gameContent) end)
miscTab.MouseButton1Click:Connect(function() switchTab(miscTab, miscContent) end)

-- Ativar primeira aba
switchTab(homeTab, homeContent)

print("🎮 Script carregado! Pressione a GUI para usar.")

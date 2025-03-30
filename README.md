-- Bazuka Hub

local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local TabHolder = Instance.new("Frame")
local HomeTab = Instance.new("TextButton")
local TeleportTab = Instance.new("TextButton")
local WeaponsTab = Instance.new("TextButton")
local VehiclesTab = Instance.new("TextButton")
local CloseButton = Instance.new("TextButton")
local HomeFrame = Instance.new("Frame")
local TeleportFrame = Instance.new("Frame")
local WeaponsFrame = Instance.new("Frame")
local VehiclesFrame = Instance.new("Frame")

ScreenGui.Parent = game.CoreGui
ScreenGui.Name = "Bazuka Hub"
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

MainFrame.Parent = ScreenGui
MainFrame.Size = UDim2.new(0, 500, 0, 350)
MainFrame.Position = UDim2.new(0.5, -250, 0.5, -175)
MainFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
MainFrame.BorderColor3 = Color3.fromRGB(255, 255, 255)
MainFrame.BorderSizePixel = 2
MainFrame.Active = true
MainFrame.Draggable = true

TabHolder.Parent = MainFrame
TabHolder.Size = UDim2.new(1, 0, 0, 40)
TabHolder.Position = UDim2.new(0, 0, 0, 0)
TabHolder.BackgroundColor3 = Color3.fromRGB(30, 30, 30)

local function createTabButton(name, posX)
    local button = Instance.new("TextButton")
    button.Parent = TabHolder
    button.Size = UDim2.new(0, 120, 0, 40)
    button.Position = UDim2.new(0, posX, 0, 0)
    button.Text = name
    button.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.BorderSizePixel = 0
    return button
end

HomeTab = createTabButton("🏠 Home", 0)
TeleportTab = createTabButton("🚀 Teleport", 120)
WeaponsTab = createTabButton("🔫 Armas", 240)
VehiclesTab = createTabButton("🚗 Veículos", 360)

CloseButton.Parent = MainFrame
CloseButton.Size = UDim2.new(0, 80, 0, 30)
CloseButton.Position = UDim2.new(1, -90, 0, 10)
CloseButton.Text = "Fechar"
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.BorderSizePixel = 0
CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

local function switchTab(tab)
    HomeFrame.Visible = false
    TeleportFrame.Visible = false
    WeaponsFrame.Visible = false
    VehiclesFrame.Visible = false
    if tab == "Home" then
        HomeFrame.Visible = true
    elseif tab == "Teleport" then
        TeleportFrame.Visible = true
    elseif tab == "Weapons" then
        WeaponsFrame.Visible = true
    elseif tab == "Vehicles" then
        VehiclesFrame.Visible = true
    end
end

HomeFrame.Parent = MainFrame
HomeFrame.Size = UDim2.new(1, 0, 1, -40)
HomeFrame.Position = UDim2.new(0, 0, 0, 40)
HomeFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
HomeFrame.Visible = true

TeleportFrame.Parent = MainFrame
TeleportFrame.Size = UDim2.new(1, 0, 1, -40)
TeleportFrame.Position = UDim2.new(0, 0, 0, 40)
TeleportFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
TeleportFrame.Visible = false

WeaponsFrame.Parent = MainFrame
WeaponsFrame.Size = UDim2.new(1, 0, 1, -40)
WeaponsFrame.Position = UDim2.new(0, 0, 0, 40)
WeaponsFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
WeaponsFrame.Visible = false

VehiclesFrame.Parent = MainFrame
VehiclesFrame.Size = UDim2.new(1, 0, 1, -40)
VehiclesFrame.Position = UDim2.new(0, 0, 0, 40)
VehiclesFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
VehiclesFrame.Visible = false

HomeTab.MouseButton1Click:Connect(function()
    switchTab("Home")
end)
TeleportTab.MouseButton1Click:Connect(function()
    switchTab("Teleport")
end)
WeaponsTab.MouseButton1Click:Connect(function()
    switchTab("Weapons")
end)
VehiclesTab.MouseButton1Click:Connect(function()
    switchTab("Vehicles")
end)

local function activateKillAura()
    print("Kill Aura ativado!")
end
local function deactivateKillAura()
    print("Kill Aura desativado!")
end

local function activateESP()
    print("ESP ativado!")
end
local function deactivateESP()
    print("ESP desativado!")
end

local function activateNoclip()
    print("Noclip ativado!")
end
local function deactivateNoclip()
    print("Noclip desativado!")
end

local function teleportToPlayer(playerName)
    print("Teleportando até " .. playerName)
end

local function pullPlayer(playerName)
    print("Puxando jogador " .. playerName)
end

local function giveGun(gunName)
    print("Pegando arma: " .. gunName)
end

local function pullCar()
    print("Puxando carros próximos...")
end

local function giveCard()
    print("Pegando cartão de desbloqueio de portas...")
end

local killAuraButton = Instance.new("TextButton")
killAuraButton.Parent = HomeFrame
killAuraButton.Size = UDim2.new(0, 200, 0, 40)
killAuraButton.Position = UDim2.new(0, 10, 0, 10)
killAuraButton.Text = "Kill Aura"
killAuraButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
killAuraButton.TextColor3 = Color3.fromRGB(255, 255, 255)
killAuraButton.MouseButton1Click:Connect(function()
    activateKillAura()
end)

local espButton = Instance.new("TextButton")
espButton.Parent = HomeFrame
espButton.Size = UDim2.new(0, 200, 0, 40)
espButton.Position = UDim2.new(0, 10, 0, 60)
espButton.Text = "ESP"
espButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
espButton.TextColor3 = Color3.fromRGB(255, 255, 255)

local noclipButton = Instance.new("TextButton")
noclipButton.Parent = HomeFrame
noclipButton.Size = UDim2.new(0, 200, 0, 40)
noclipButton.Position = UDim2.new(0, 10, 0, 110)
noclipButton.Text = "Noclip"
noclipButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
noclipButton.TextColor3 = Color3.fromRGB(255, 255, 255)

local gunButton = Instance.new("TextButton")
gunButton.Parent = WeaponsFrame
gunButton.Size = UDim2.new(0, 200, 0, 40)
gunButton.Position = UDim2.new(0, 10, 0, 10)
gunButton.Text = "AK-47"
gunButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
gunButton.TextColor3 = Color3.fromRGB(255, 255, 255)
gunButton.MouseButton1Click:Connect(function()
    giveGun("AK-47")
end)

local teleportButton = Instance.new("TextButton")
teleportButton.Parent = TeleportFrame
teleportButton.Size = UDim2.new(0, 200, 0, 40)
teleportButton.Position = UDim2.new(0, 10, 0, 10)
teleportButton.Text = "Teleportar"
teleportButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
teleportButton.TextColor3 = Color3.fromRGB(255, 255, 255)
teleportButton.MouseButton1Click:Connect(function()
    teleportToPlayer("JogadorExemplo")
end)

local vehicleButton = Instance.new("TextButton")
vehicleButton.Parent = VehiclesFrame
vehicleButton.Size = UDim2.new(0, 200, 0, 40)
vehicleButton.Position = UDim2.new(0, 10, 0, 10)
vehicleButton.Text = "Puxar Carro"
vehicleButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
vehicleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
vehicleButton.MouseButton1Click:Connect(function()
    pullCar()
end)

local cardButton = Instance.new("TextButton")
cardButton.Parent = HomeFrame
cardButton.Size = UDim2.new(0, 200, 0, 40)
cardButton.Position = UDim2.new(0, 10, 0, 160)
cardButton.Text = "Pegar Cartão"
cardButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
cardButton.TextColor3 = Color3.fromRGB(255, 255, 255)
cardButton.MouseButton1Click:Connect(function()
    giveCard()
end)

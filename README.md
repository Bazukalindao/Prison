-- Bazuka Hub

local player = game.Players.LocalPlayer
local mouse = player:GetMouse()

local function activateKillAura()
    while true do
        for _, target in pairs(game.Players:GetPlayers()) do
            if target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
                local targetPos = target.Character.HumanoidRootPart.Position
                if (player.Character.HumanoidRootPart.Position - targetPos).Magnitude < 10 then
                    print("Kill Aura ativado!")
                end
            end
        end
        wait(1)
    end
end

local function activateESP()
    for _, target in pairs(game.Players:GetPlayers()) do
        if target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
            local espPart = Instance.new("BillboardGui")
            espPart.Adornee = target.Character.HumanoidRootPart
            espPart.Parent = target.Character
            espPart.Size = UDim2.new(0, 200, 0, 50)
            espPart.StudsOffset = Vector3.new(0, 2, 0)
            local textLabel = Instance.new("TextLabel")
            textLabel.Parent = espPart
            textLabel.Text = target.Name
            textLabel.TextColor3 = Color3.fromRGB(255, 0, 0)
            textLabel.BackgroundTransparency = 1
        end
    end
end

local function activateNoclip()
    local character = player.Character
    local humanoid = character:FindFirstChildOfClass("Humanoid")
    humanoid.PlatformStand = true
    character:WaitForChild("HumanoidRootPart").CFrame = character.HumanoidRootPart.CFrame + Vector3.new(0, 5, 0)
end

local function giveCard()
    local card = game.ReplicatedStorage:WaitForChild("Card")
    local clone = card:Clone()
    clone.Parent = player.Backpack
    print("Cartão de desbloqueio obtido!")
end

local function teleportToPlayer(playerName)
    for _, target in pairs(game.Players:GetPlayers()) do
        if target.Name == playerName then
            player.Character:WaitForChild("HumanoidRootPart").CFrame = target.Character.HumanoidRootPart.CFrame
            print("Teleportado até " .. playerName)
        end
    end
end

local function pullPlayer(playerName)
    for _, target in pairs(game.Players:GetPlayers()) do
        if target.Name == playerName then
            local targetPosition = target.Character.HumanoidRootPart.Position
            player.Character.HumanoidRootPart.CFrame = CFrame.new(targetPosition)
            print("Puxando jogador " .. playerName)
        end
    end
end

local function makeDraggable(frame)
    local dragToggle = nil
    local dragSpeed = 0.25
    local dragInput, dragStart, startPos

    frame.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragToggle = true
            dragStart = input.Position
            startPos = frame.Position
            input.Changed:Connect(function()
                if dragToggle then
                    local delta = input.Position - dragStart
                    frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
                end
            end)
        end
    end)

    frame.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragToggle = false
        end
    end)
end

local function createPanel()
    local panel = Instance.new("Frame")
    panel.Size = UDim2.new(0, 300, 0, 400)
    panel.Position = UDim2.new(0.5, -150, 0.5, -200)  -- Centralizando o painel
    panel.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    panel.BackgroundTransparency = 0.5
    panel.Parent = player:WaitForChild("PlayerGui")  -- Usando PlayerGui em vez de CoreGui
    panel.Visible = true
    makeDraggable(panel)

    local toggleButton = Instance.new("TextButton")
    toggleButton.Text = "+"
    toggleButton.Size = UDim2.new(0, 30, 0, 30)
    toggleButton.Position = UDim2.new(0, 270, 0, 10)
    toggleButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
    toggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    toggleButton.Parent = panel

    local function closePanel()
        panel.Visible = false
        toggleButton.Text = "+"
    end

    local function openPanel()
        panel.Visible = true
        toggleButton.Text = "−"
    end

    toggleButton.MouseButton1Click:Connect(function()
        if panel.Visible then
            closePanel()
        else
            openPanel()
        end
    end)

    local function createButton(name, position, size, callback)
        local button = Instance.new("TextButton")
        button.Text = name
        button.Size = size
        button.Position = position
        button.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
        button.TextColor3 = Color3.fromRGB(255, 255, 255)
        button.Parent = panel
        button.MouseButton1Click:Connect(callback)
        return button
    end

    createButton("Kill Aura", UDim2.new(0, 50, 0, 50), UDim2.new(0, 200, 0, 50), function()
        activateKillAura()
    end)

    createButton("ESP", UDim2.new(0, 50, 0, 110), UDim2.new(0, 200, 0, 50), function()
        activateESP()
    end)

    createButton("Noclip", UDim2.new(0, 50, 0, 170), UDim2.new(0, 200, 0, 50), function()
        activateNoclip()
    end)

    createButton("Cartão", UDim2.new(0, 50, 0, 230), UDim2.new(0, 200, 0, 50), function()
        giveCard()
    end)

    createButton("Teleportar", UDim2.new(0, 50, 0, 290), UDim2.new(0, 200, 0, 50), function()
        teleportToPlayer("NomeDoJogador")
    end)

    createButton("Puxar", UDim2.new(0, 50, 0, 350), UDim2.new(0, 200, 0, 50), function()
        pullPlayer("NomeDoJogador")
    end)
end

local function showNotification()
    local notification = Instance.new("Frame")
    notification.Size = UDim2.new(0, 300, 0, 50)
    notification.Position = UDim2.new(0.5, -150, 0, 10)
    notification.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    notification.BackgroundTransparency = 0.7
    notification.Parent = player:WaitForChild("PlayerGui")  -- Usando PlayerGui

    local textLabel = Instance.new("TextLabel")
    textLabel.Text = "Bazuka Hub"
    textLabel.Size = UDim2.new(1, 0, 1, 0)
    textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    textLabel.BackgroundTransparency = 1
    textLabel.Parent = notification

    wait(2)
    notification:Destroy()
end

showNotification()
createPanel()

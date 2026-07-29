--[[
	WARNING: Heads up! This script has not been verified by ScriptBlox. Use at your own risk!
]]
-- IGUINHO HUB☠ - Modern Sidebar UI (Version 2.5 - Com Teleporte)

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local CoreGui = game:GetService("CoreGui")
local UserInputService = game:GetService("UserInputService")
local LocalPlayer = Players.LocalPlayer
local Camera = workspace.CurrentCamera

local Config = {
    AimPlayerEnabled = false,
    AimNPCEnabled = false,
    ESPPlayerEnabled = false,
    ESPNPCEnabled = false,
    ESPTracerPlayer = false,
    ESPTracerNPC = false,
    HitboxPlayerEnabled = false,
    HitboxNPCEnabled = false,
    HitboxSize = 5,
    SpeedEnabled = false,
    SpeedValue = 20,
    InfiniteJumpEnabled = false,
    NoclipEnabled = false,
    MaxDistance = 40,
    AimPart = "Head",
    Smoothing = 4,
    SelectedTeleportPlayer = nil
}

-- Limpa versões anteriores para evitar conflitos na tela
pcall(function()
    if CoreGui:FindFirstChild("IguinhoMobileHub") then
        CoreGui.IguinhoMobileHub:Destroy()
    end
end)

local espPlayerLines = {}
local espNPCLines = {}
local espPlayerTracers = {}
local espNPCTracers = {}
local originalSizes = {}

-- Criando a ScreenGui Principal Otimizada para Mobile
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "IguinhoMobileHub"
ScreenGui.Parent = CoreGui
ScreenGui.ResetOnSpawn = false

-- Botão Flutuante (Bolinha) Principal com a imagem e borda RGB
local ToggleBtn = Instance.new("ImageButton")
ToggleBtn.Parent = ScreenGui
ToggleBtn.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
ToggleBtn.Position = UDim2.new(0.02, 0, 0.4, 0)
ToggleBtn.Size = UDim2.new(0, 55, 0, 55)
ToggleBtn.Image = "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTUsYGSyeryGfSm0Mve1pIiDKOPtAJO1URGAegpau6eJ6a58rJ8H7T-IsUJ&s=10"
ToggleBtn.ScaleType = Enum.ScaleType.Crop
ToggleBtn.Active = true
ToggleBtn.Draggable = true

local UICornerBtn = Instance.new("UICorner")
UICornerBtn.CornerRadius = UDim.new(1, 0)
UICornerBtn.Parent = ToggleBtn

local UIStrokeBtn = Instance.new("UIStroke")
UIStrokeBtn.Parent = ToggleBtn
UIStrokeBtn.Thickness = 2.5
UIStrokeBtn.Color = Color3.fromRGB(255, 255, 255)

task.spawn(function()
    local h = 0
    while ToggleBtn and ToggleBtn.Parent do
        h = (h + 1) % 360
        UIStrokeBtn.Color = Color3.fromHSV(h / 360, 1, 1)
        task.wait(0.02)
    end
end)

-- Janela Principal do Menu
local MainFrame = Instance.new("Frame")
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(13, 13, 15)
MainFrame.Position = UDim2.new(0.12, 0, 0.1, 0)
MainFrame.Size = UDim2.new(0, 460, 0, 310)
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Visible = true

local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 12)
MainCorner.Parent = MainFrame

local MainStroke = Instance.new("UIStroke")
MainStroke.Parent = MainFrame
MainStroke.Thickness = 1.5
MainStroke.Color = Color3.fromRGB(45, 45, 55)

-- Cabeçalho com Versão 2.5
local LeftHeader = Instance.new("Frame")
LeftHeader.Parent = MainFrame
LeftHeader.BackgroundTransparency = 1
LeftHeader.Position = UDim2.new(0, 12, 0, 10)
LeftHeader.Size = UDim2.new(0, 135, 0, 40)

local TitleLabel = Instance.new("TextLabel")
TitleLabel.Parent = LeftHeader
TitleLabel.BackgroundTransparency = 1
TitleLabel.Size = UDim2.new(1, 0, 0, 20)
TitleLabel.Font = Enum.Font.SourceSansBold
TitleLabel.Text = "IGUINHO HUB☠"
TitleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TitleLabel.TextSize = 13
TitleLabel.TextXAlignment = Enum.TextXAlignment.Left

task.spawn(function()
    local h = 0
    while TitleLabel and TitleLabel.Parent do
        h = (h + 2) % 360
        TitleLabel.TextColor3 = Color3.fromHSV(h / 360, 1, 1)
        task.wait(0.02)
    end
end)

local SubTitleLabel = Instance.new("TextLabel")
SubTitleLabel.Parent = LeftHeader
SubTitleLabel.BackgroundTransparency = 1
SubTitleLabel.Position = UDim2.new(0, 0, 0, 18)
SubTitleLabel.Size = UDim2.new(1, 0, 0, 15)
SubTitleLabel.Font = Enum.Font.SourceSans
SubTitleLabel.Text = "version 2.5 [beta]"
SubTitleLabel.TextColor3 = Color3.fromRGB(0, 229, 255)
SubTitleLabel.TextSize = 11
SubTitleLabel.TextXAlignment = Enum.TextXAlignment.Left

-- Sidebar
local Sidebar = Instance.new("ScrollingFrame")
Sidebar.Parent = MainFrame
Sidebar.BackgroundTransparency = 1
Sidebar.Position = UDim2.new(0, 10, 0, 55)
Sidebar.Size = UDim2.new(0, 140, 0, 245)
Sidebar.CanvasSize = UDim2.new(0, 0, 0, 0)
Sidebar.ScrollBarThickness = 2
Sidebar.ScrollingEnabled = false

local SidebarLayout = Instance.new("UIListLayout")
SidebarLayout.Parent = Sidebar
SidebarLayout.SortOrder = Enum.SortOrder.LayoutOrder
SidebarLayout.Padding = UDim.new(0, 4)

-- Content Container
local ContentContainer = Instance.new("Frame")
ContentContainer.Parent = MainFrame
ContentContainer.BackgroundColor3 = Color3.fromRGB(18, 18, 22)
ContentContainer.Position = UDim2.new(0, 155, 0, 12)
ContentContainer.Size = UDim2.new(0, 293, 0, 286)

local ContentCorner = Instance.new("UICorner")
ContentCorner.CornerRadius = UDim.new(0, 8)
ContentCorner.Parent = ContentContainer

local ContentStroke = Instance.new("UIStroke")
ContentStroke.Parent = ContentContainer
ContentStroke.Thickness = 1
ContentStroke.Color = Color3.fromRGB(35, 35, 45)

local Pages = {}
local TabButtons = {}

local function CreatePage(name)
    local page = Instance.new("ScrollingFrame")
    page.Name = name .. "Page"
    page.Parent = ContentContainer
    page.BackgroundTransparency = 1
    page.Position = UDim2.new(0, 10, 0, 10)
    page.Size = UDim2.new(1, -20, 1, -20)
    page.CanvasSize = UDim2.new(0, 0, 0, 0)
    page.ScrollBarThickness = 3
    page.Visible = false

    local layout = Instance.new("UIListLayout")
    layout.Parent = page
    layout.SortOrder = Enum.SortOrder.LayoutOrder
    layout.Padding = UDim.new(0, 8)

    layout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
        page.CanvasSize = UDim2.new(0, 0, 0, layout.AbsoluteContentSize.Y + 10)
    end)

    Pages[name] = page
    return page
end

local function CreateTab(name)
    local btn = Instance.new("TextButton")
    btn.Parent = Sidebar
    btn.BackgroundTransparency = 1
    btn.Size = UDim2.new(1, 0, 0, 30)
    btn.Font = Enum.Font.SourceSansBold
    btn.Text = "  " .. name
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.TextSize, btn.TextXAlignment = 12, Enum.TextXAlignment.Left

    task.spawn(function()
        local h = math.random()
        while btn and btn.Parent do
            h = (h + 0.005) % 1
            btn.TextColor3 = Color3.fromHSV(h, 1, 1)
            task.wait(0.02)
        end
    end)

    local page = CreatePage(name)

    btn.MouseButton1Click:Connect(function()
        for _, p in pairs(Pages) do p.Visible = false end
        for _, b in pairs(TabButtons) do b.BackgroundTransparency = 1 end
        page.Visible = true
        btn.BackgroundTransparency = 0.5
    end)

    table.insert(TabButtons, btn)
    return page
end

CreateTab("AIMBOT")
CreateTab("PLAYER ESP")
CreateTab("HITBOX")
CreateTab("BRING")
CreateTab("TELEPORT")
CreateTab("OTHER")

Pages["AIMBOT"].Visible = true
TabButtons[1].BackgroundTransparency = 0.5

local function CreateToggleInPage(page, titleText, descColor, defaultState, callback)
    local card = Instance.new("Frame")
    card.Parent = page
    card.BackgroundColor3 = Color3.fromRGB(24, 24, 30)
    card.Size = UDim2.new(1, 0, 0, 42)

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 6)
    corner.Parent = card

    local stroke = Instance.new("UIStroke")
    stroke.Parent = card
    stroke.Thickness = 1
    stroke.Color = Color3.fromRGB(40, 40, 50)

    local label = Instance.new("TextLabel")
    label.Parent = card
    label.BackgroundTransparency = 1
    label.Position = UDim2.new(0, 10, 0, 0)
    label.Size = UDim2.new(1, -55, 1, 0)
    label.Font = Enum.Font.SourceSansBold
    label.Text = titleText
    label.TextColor3 = descColor
    label.TextSize = 12
    label.TextXAlignment = Enum.TextXAlignment.Left

    local switchBtn = Instance.new("TextButton")
    switchBtn.Parent = card
    switchBtn.AnchorPoint = Vector2.new(1, 0.5)
    switchBtn.Position = UDim2.new(1, -10, 0.5, 0)
    switchBtn.Size = UDim2.new(0, 36, 0, 20)
    switchBtn.Text = ""

    local switchCorner = Instance.new("UICorner")
    switchCorner.CornerRadius = UDim.new(1, 0)
    switchCorner.Parent = switchBtn

    local circle = Instance.new("Frame")
    circle.Parent = switchBtn
    circle.Size = UDim2.new(0, 16, 0, 16)
    circle.AnchorPoint = Vector2.new(0, 0.5)
    circle.Position = UDim2.new(0, 2, 0.5, 0)

    local circleCorner = Instance.new("UICorner")
    circleCorner.CornerRadius = UDim.new(1, 0)
    circleCorner.Parent = circle

    local state = defaultState
    local function updateVisual(anim)
        if state then
            switchBtn.BackgroundColor3 = Color3.fromRGB(0, 160, 255)
            circle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
            if anim then
                circle:TweenPosition(UDim2.new(1, -18, 0.5, 0), Enum.EasingDirection.Out, Enum.EasingStyle.Quad, 0.15, true)
            else
                circle.Position = UDim2.new(1, -18, 0.5, 0)
            end
        else
            switchBtn.BackgroundColor3 = Color3.fromRGB(45, 45, 55)
            circle.BackgroundColor3 = Color3.fromRGB(160, 160, 170)
            if anim then
                circle:TweenPosition(UDim2.new(0, 2, 0.5, 0), Enum.EasingDirection.Out, Enum.EasingStyle.Quad, 0.15, true)
            else
                circle.Position = UDim2.new(0, 2, 0.5, 0)
            end
        end
    end
    updateVisual(false)

    switchBtn.MouseButton1Click:Connect(function()
        state = not state
        updateVisual(true)
        callback(state)
    end)
end

local function CreateTextBoxInPage(page, titleText, descColor, defaultValue, callback)
    local card = Instance.new("Frame")
    card.Parent = page
    card.BackgroundColor3 = Color3.fromRGB(24, 24, 30)
    card.Size = UDim2.new(1, 0, 0, 42)

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 6)
    corner.Parent = card

    local stroke = Instance.new("UIStroke")
    stroke.Parent = card
    stroke.Thickness = 1
    stroke.Color = Color3.fromRGB(40, 40, 50)

    local label = Instance.new("TextLabel")
    label.Parent = card
    label.BackgroundTransparency = 1
    label.Position = UDim2.new(0, 10, 0, 0)
    label.Size = UDim2.new(1, -65, 1, 0)
    label.Font = Enum.Font.SourceSansBold
    label.Text = titleText
    label.TextColor3 = descColor
    label.TextSize = 12
    label.TextXAlignment = Enum.TextXAlignment.Left

    local textBox = Instance.new("TextBox")
    textBox.Parent = card
    textBox.AnchorPoint = Vector2.new(1, 0.5)
    textBox.Position = UDim2.new(1, -10, 0.5, 0)
    textBox.Size = UDim2.new(0, 50, 0, 24)
    textBox.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
    textBox.Font = Enum.Font.SourceSansBold
    textBox.Text = tostring(defaultValue)
    textBox.TextColor3 = Color3.fromRGB(255, 255, 255)
    textBox.TextSize = 13

    local tbCorner = Instance.new("UICorner")
    tbCorner.CornerRadius = UDim.new(0, 4)
    tbCorner.Parent = textBox

    textBox.FocusLost:Connect(function(enterPressed)
        local val = tonumber(textBox.Text)
        if val then
            callback(val)
        else
            textBox.Text = tostring(defaultValue)
        end
    end)
end

CreateToggleInPage(Pages["AIMBOT"], "Aim Assist (Players)", Color3.fromRGB(255, 100, 120), false, function(state)
    Config.AimPlayerEnabled = state
end)

CreateToggleInPage(Pages["AIMBOT"], "Aim Assist (NPCs)", Color3.fromRGB(255, 150, 100), false, function(state)
    Config.AimNPCEnabled = state
end)

CreateToggleInPage(Pages["PLAYER ESP"], "ESP Line (Players)", Color3.fromRGB(255, 255, 255), false, function(state)
    Config.ESPPlayerEnabled = state
    if not state then
        for _, line in pairs(espPlayerLines) do if line then line:Remove() end end
        espPlayerLines = {}
    end
end)

CreateToggleInPage(Pages["PLAYER ESP"], "ESP Tracer Skeleton (Players)", Color3.fromRGB(240, 240, 240), false, function(state)
    Config.ESPTracerPlayer = state
    if not state then
        for _, lines in pairs(espPlayerTracers) do 
            for _, l in pairs(lines) do if l then l:Remove() end end
        end
        espPlayerTracers = {}
    end
end)

CreateToggleInPage(Pages["PLAYER ESP"], "ESP Line (NPCs)", Color3.fromRGB(255, 50, 50), false, function(state)
    Config.ESPNPCEnabled = state
    if not state then
        for _, line in pairs(espNPCLines) do if line then line:Remove() end end
        espNPCLines = {}
    end
end)

CreateToggleInPage(Pages["PLAYER ESP"], "ESP Tracer Skeleton (NPCs)", Color3.fromRGB(255, 80, 80), false, function(state)
    Config.ESPTracerNPC = state
    if not state then
        for _, lines in pairs(espNPCTracers) do 
            for _, l in pairs(lines) do if l then l:Remove() end end
        end
        espNPCTracers = {}
    end
end)

CreateToggleInPage(Pages["HITBOX"], "Hitbox Expander (Players)", Color3.fromRGB(100, 200, 255), false, function(state)
    Config.HitboxPlayerEnabled = state
end)

CreateToggleInPage(Pages["HITBOX"], "Hitbox Expander (NPCs)", Color3.fromRGB(255, 200, 100), false, function(state)
    Config.HitboxNPCEnabled = state
end)

CreateTextBoxInPage(Pages["HITBOX"], "Adjust Hitbox Size", Color3.fromRGB(255, 255, 255), Config.HitboxSize, function(val)
    Config.HitboxSize = val
end)

local bringPlayersActive = false
local bringNPCsActive = false

CreateToggleInPage(Pages["BRING"], "Bring All Players", Color3.fromRGB(100, 255, 150), false, function(state)
    bringPlayersActive = state
end)

CreateToggleInPage(Pages["BRING"], "Bring All NPCs", Color3.fromRGB(255, 100, 200), false, function(state)
    bringNPCsActive = state
end)

-- ABA DE TELEPORT RECRIADA
local tpCard = Instance.new("Frame")
tpCard.Parent = Pages["TELEPORT"]
tpCard.BackgroundColor3 = Color3.fromRGB(24, 24, 30)
tpCard.Size = UDim2.new(1, 0, 0, 110)

local tpCardCorner = Instance.new("UICorner")
tpCardCorner.CornerRadius = UDim.new(0, 6)
tpCardCorner.Parent = tpCard

local tpCardStroke = Instance.new("UIStroke")
tpCardStroke.Parent = tpCard
tpCardStroke.Thickness = 1
tpCardStroke.Color = Color3.fromRGB(40, 40, 50)

local tpLabel = Instance.new("TextLabel")
tpLabel.Parent = tpCard
tpLabel.BackgroundTransparency = 1
tpLabel.Position = UDim2.new(0, 10, 0, 5)
tpLabel.Size = UDim2.new(1, -20, 0, 20)
tpLabel.Font = Enum.Font.SourceSansBold
tpLabel.Text = "Teleport to Player (Selecione abaixo):"
tpLabel.TextColor3 = Color3.fromRGB(0, 229, 255)
tpLabel.TextSize = 12
tpLabel.TextXAlignment = Enum.TextXAlignment.Left

local reloadBtn = Instance.new("TextButton")
reloadBtn.Parent = tpCard
reloadBtn.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
reloadBtn.Position = UDim2.new(0, 10, 0, 30)
reloadBtn.Size = UDim2.new(0, 120, 0, 24)
reloadBtn.Font = Enum.Font.SourceSansBold
reloadBtn.Text = "🔄 Recarregar Lista"
reloadBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
reloadBtn.TextSize = 11

local reloadCorner = Instance.new("UICorner")
reloadCorner.CornerRadius = UDim.new(0, 4)
reloadCorner.Parent = reloadBtn

local playerListScroll = Instance.new("ScrollingFrame")
playerListScroll.Parent = tpCard
playerListScroll.BackgroundColor3 = Color3.fromRGB(18, 18, 22)
playerListScroll.Position = UDim2.new(0, 10, 0, 60)
playerListScroll.Size = UDim2.new(1, -120, 0, 40)
playerListScroll.CanvasSize = UDim2.new(0, 0, 0, 0)
playerListScroll.ScrollBarThickness = 2

local listLayout = Instance.new("UIListLayout")
listLayout.Parent = playerListScroll
listLayout.SortOrder = Enum.SortOrder.LayoutOrder
listLayout.Padding = UDim.new(0, 2)

local function populatePlayerList()
    for _, child in ipairs(playerListScroll:GetChildren()) do
        if child:IsA("TextButton") then
            child:Destroy()
        end
    end

    for _, p in ipairs(Players:GetPlayers()) do
        if p ~= LocalPlayer then
            local pBtn = Instance.new("TextButton")
            pBtn.Parent = playerListScroll
            pBtn.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
            pBtn.Size = UDim2.new(1, 0, 0, 22)
            pBtn.Font = Enum.Font.SourceSans
            pBtn.Text = "  " .. p.Name
            pBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
            pBtn.TextSize, pBtn.TextXAlignment = 11, Enum.TextXAlignment.Left

            local btnCorner = Instance.new("UICorner")
            btnCorner.CornerRadius = UDim.new(0, 3)
            btnCorner.Parent = pBtn

            pBtn.MouseButton1Click:Connect(function()
                Config.SelectedTeleportPlayer = p
                tpLabel.Text = "Alvo: " .. p.Name
            end)
        end
    end
    playerListScroll.CanvasSize = UDim2.new(0, 0, 0, listLayout.AbsoluteContentSize.Y)
end

reloadBtn.MouseButton1Click:Connect(populatePlayerList)
task.spawn(populatePlayerList)

local execTpBtn = Instance.new("TextButton")
execTpBtn.Parent = tpCard
execTpBtn.BackgroundColor3 = Color3.fromRGB(0, 160, 255)
execTpBtn.Position = UDim2.new(1, -100, 0, 30)
execTpBtn.Size = UDim2.new(0, 90, 0, 70)
execTpBtn.Font = Enum.Font.SourceSansBold
execTpBtn.Text = "TELEPORT\nTO PLAYER"
execTpBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
execTpBtn.TextSize = 12

local execCorner = Instance.new("UICorner")
execCorner.CornerRadius = UDim.new(0, 6)
execCorner.Parent = execTpBtn

execTpBtn.MouseButton1Click:Connect(function()
    pcall(function()
        if Config.SelectedTeleportPlayer and Config.SelectedTeleportPlayer.Character then
            local targetRoot = Config.SelectedTeleportPlayer.Character:FindFirstChild("HumanoidRootPart")
            local myRoot = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
            if targetRoot and myRoot then
                myRoot.CFrame = targetRoot.CFrame * CFrame.new(0, 0, 3)
                myRoot.Velocity = Vector3.new(0, 0, 0)
                myRoot.RotVelocity = Vector3.new(0, 0, 0)
            end
        end
    end)
end)

CreateToggleInPage(Pages["OTHER"], "Speed Boost (WalkSpeed)", Color3.fromRGB(255, 170, 0), false, function(state)
    Config.SpeedEnabled = state
end)

CreateTextBoxInPage(Pages["OTHER"], "Adjust WalkSpeed Value", Color3.fromRGB(255, 200, 100), Config.SpeedValue, function(val)
    Config.SpeedValue = val
end)

CreateToggleInPage(Pages["OTHER"], "Infinite Jump (Pulo Infinito)", Color3.fromRGB(0, 229, 255), false, function(state)
    Config.InfiniteJumpEnabled = state
end)

CreateToggleInPage(Pages["OTHER"], "Noclip (Atravessar Paredes)", Color3.fromRGB(255, 100, 255), false, function(state)
    Config.NoclipEnabled = state
end)

ToggleBtn.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)

UserInputService.JumpRequest:Connect(function()
    if Config.InfiniteJumpEnabled and LocalPlayer.Character then
        local root = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        if root then
            root.Velocity = Vector3.new(root.Velocity.X, 35, root.Velocity.Z)
        end
    end
end)

local function IsPlayer(model)
    for _, p in ipairs(Players:GetPlayers()) do
        if p.Character == model then
            return true
        end
    end
    return false
end

local function GetClosestTarget(checkNPCs)
    local closestTarget = nil
    local shortestDistance = Config.MaxDistance
    local localChar = LocalPlayer.Character
    if not localChar or not localChar:FindFirstChild("HumanoidRootPart") then return nil end

    if not checkNPCs then
        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and player.Character then
                local humanoid = player.Character:FindFirstChildOfClass("Humanoid")
                local part = player.Character:FindFirstChild(Config.AimPart)
                if humanoid and humanoid.Health > 0 and part then
                    local distance = (localChar.HumanoidRootPart.Position - part.Position).Magnitude
                    if distance < shortestDistance then
                        shortestDistance = distance
                        closestTarget = player.Character
                    end
                end
            end
        end
    else
        for _, obj in ipairs(workspace:GetDescendants()) do
            if obj:IsA("Model") and obj:FindFirstChildOfClass("Humanoid") and obj:FindFirstChild(Config.AimPart) then
                if not IsPlayer(obj) then
                    local humanoid = obj:FindFirstChildOfClass("Humanoid")
                    local part = obj:FindFirstChild(Config.AimPart)
                    if humanoid and humanoid.Health > 0 and part then
                        local distance = (localChar.HumanoidRootPart.Position - part.Position).Magnitude
                        if distance < shortestDistance then
                            shortestDistance = distance
                            closestTarget = obj
                        end
                    end
                end
            end
        end
    end

    return closestTarget
end

local function updateTracerSkeleton(char, tracerTable, color)
    if not char or not char:FindFirstChild("Head") or not char:FindFirstChild("HumanoidRootPart") then
        if tracerTable[char] then
            for _, l in pairs(tracerTable[char]) do if l then l:Remove() end end
            tracerTable[char] = nil
        end
        return
    end

    local parts = {
        Head = char:FindFirstChild("Head"),
        Torso = char:FindFirstChild("UpperTorso") or char:FindFirstChild("Torso"),
        LeftArm = char:FindFirstChild("LeftUpperArm") or char:FindFirstChild("Left Arm"),
        RightArm = char:FindFirstChild("RightUpperArm") or char:FindFirstChild("Right Arm"),
        LeftLeg = char:FindFirstChild("LeftUpperLeg") or char:FindFirstChild("Left Leg"),
        RightLeg = char:FindFirstChild("RightUpperLeg") or char:FindFirstChild("Right Leg"),
    }

    if not parts.Head or not parts.Torso then return end

    if not tracerTable[char] then
        tracerTable[char] = {
            HeadToTorso = Drawing.new("Line"),
            TorsoToLeftArm = Drawing.new("Line"),
            TorsoToRightArm = Drawing.new("Line"),
            TorsoToLeftLeg = Drawing.new("Line"),
            TorsoToRightLeg = Drawing.new("Line"),
        }
        for _, l in pairs(tracerTable[char]) do
            l.Thickness = 1.5
            l.Color = color
            l.Transparency = 0.8
        end
    end

    local t = tracerTable[char]
    local headPos, hOn = Camera:WorldToViewportPoint(parts.Head.Position)
    local torsoPos, tOn = Camera:WorldToViewportPoint(parts.Torso.Position)

    if hOn and tOn then
        t.HeadToTorso.From = Vector2.new(headPos.X, headPos.Y)
        t.HeadToTorso.To = Vector2.new(torsoPos.X, torsoPos.Y)
        t.HeadToTorso.Visible = true
    else
        t.HeadToTorso.Visible = false
    end

    local function linkPart(lineObj, pPart)
        if pPart and tOn then
            local pPos, pOn = Camera:WorldToViewportPoint(pPart.Position)
            if pOn then
                lineObj.From = Vector2.new(torsoPos.X, torsoPos.Y)
                lineObj.To = Vector2.new(pPos.X, pPos.Y)
                lineObj.Visible = true
                return
            end
        end
        lineObj.Visible = false
    end

    linkPart(t.TorsoToLeftArm, parts.LeftArm)
    linkPart(t.TorsoToRightArm, parts.RightArm)
    linkPart(t.TorsoToLeftLeg, parts.LeftLeg)
    linkPart(t.TorsoToRightLeg, parts.RightLeg)
end

RunService.RenderStepped:Connect(function()
    pcall(function()
        local myRoot = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")

        if Config.NoclipEnabled and LocalPlayer.Character then
            for _, part in ipairs(LocalPlayer.Character:GetDescendants()) do
                if part:IsA("BasePart") then
                    part.CanCollide = false
                end
            end
        end

        if Config.SpeedEnabled and LocalPlayer.Character then
            local hum = LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
            if hum then
                hum.WalkSpeed = Config.SpeedValue
            end
        end

        if bringPlayersActive and myRoot then
            for _, p in ipairs(Players:GetPlayers()) do
                if p ~= LocalPlayer and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
                    local pRoot = p.Character.HumanoidRootPart
                    pRoot.CFrame = myRoot.CFrame * CFrame.new(0, 0, -3)
                    pRoot.Velocity = Vector3.new(0, 0, 0)
                    for _, part in ipairs(p.Character:GetDescendants()) do
                        if part:IsA("BasePart") then
                            part.CanCollide = false
                        end
                    end
                end
            end
        end

        if bringNPCsActive and myRoot then
            for _, obj in ipairs(workspace:GetDescendants()) do
                if obj:IsA("Model") and obj:FindFirstChildOfClass("Humanoid") and obj:FindFirstChild("HumanoidRootPart") then
                    if not IsPlayer(obj) then
                        local npcRoot = obj.HumanoidRootPart
                        npcRoot.CFrame = myRoot.CFrame * CFrame.new(0, 0, -3)
                        npcRoot.Velocity = Vector3.new(0, 0, 0)
                        for _, part in ipairs(obj:GetDescendants()) do
                            if part:IsA("BasePart") then
                                part.CanCollide = false
                            end
                        end
                    end
                end
            end
        end

        if Config.AimPlayerEnabled or Config.AimNPCEnabled then
            local targetChar = nil
            if Config.AimPlayerEnabled then targetChar = GetClosestTarget(false) end
            if not targetChar and Config.AimNPCEnabled then targetChar = GetClosestTarget(true) end

            if targetChar and targetChar:FindFirstChild(Config.AimPart) then
                local targetPart = targetChar[Config.AimPart]
                local currentCFrame = Camera.CFrame
                local targetCFrame = CFrame.new(currentCFrame.Position, targetPart.Position)
                Camera.CFrame = currentCFrame:Lerp(targetCFrame, 1 / Config.Smoothing)
            end
        end

        -- Hitbox Expander (Transparência antiga)
        local function manageHitbox(model, enabled)
            local part = model:FindFirstChild("HumanoidRootPart") or model:FindFirstChild("Head")
            if part then
                if not originalSizes[part] then
                    originalSizes[part] = part.Size
                end
                if enabled then
                    part.Size = Vector3.new(Config.HitboxSize, Config.HitboxSize, Config.HitboxSize)
                    part.Transparency = 0.7
                    part.CanCollide = false
                else
                    part.Size = originalSizes[part]
                    part.Transparency = 0
                end
            end
        end

        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and player.Character then
                manageHitbox(player.Character, Config.HitboxPlayerEnabled)
            end
        end

        if Config.HitboxNPCEnabled then
            for _, obj in ipairs(workspace:GetDescendants()) do
                if obj:IsA("Model") and obj:FindFirstChildOfClass("Humanoid") and not IsPlayer(obj) then
                    manageHitbox(obj, true)
                end
            end
        end

        if Config.ESPPlayerEnabled then
            local activePlayers = {}
            for _, player in ipairs(Players:GetPlayers()) do
                if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                    local humanoid = player.Character:FindFirstChildOfClass("Humanoid")
                    if humanoid and humanoid.Health > 0 then
                        local hrp = player.Character.HumanoidRootPart
                        local vector, onScreen = Camera:WorldToViewportPoint(hrp.Position)
                        local line = espPlayerLines[player]
                        if not line then
                            line = Drawing.new("Line")
                            line.Thickness = 1.5
                            line.Color = Color3.fromRGB(255, 255, 255)
                            line.Transparency = 0.8
                            espPlayerLines[player] = line
                        end
                        if onScreen then
                            line.From = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y)
                            line.To = Vector2.new(vector.X, vector.Y)
                            line.Visible = true
                        else
                            line.Visible = false
                        end
                        activePlayers[player] = true
                    end
                end
            end
            for player, line in pairs(espPlayerLines) do
                if not activePlayers[player] then if line then line:Remove() end espPlayerLines[player] = nil end
            end
        else
            for _, line in pairs(espPlayerLines) do if line then line:Remove() end end
            espPlayerLines = {}
        end

        if Config.ESPNPCEnabled then
            local activeNPCs = {}
            for _, obj in ipairs(workspace:GetDescendants()) do
                if obj:IsA("Model") and obj:FindFirstChildOfClass("Humanoid") and obj:FindFirstChild("HumanoidRootPart") then
                    if not IsPlayer(obj) then
                        local humanoid = obj:FindFirstChildOfClass("Humanoid")
                        if humanoid and humanoid.Health > 0 then
                            local hrp = obj.HumanoidRootPart
                            local vector, onScreen = Camera:WorldToViewportPoint(hrp.Position)
                            local line = espNPCLines[obj]
                            if not line then
                                line = Drawing.new("Line")
                                line.Thickness = 1.5
                                line.Color = Color3.fromRGB(255, 0, 0)
                                line.Transparency = 0.8
                                espNPCLines[obj] = line
                            end
                            if onScreen then
                                line.From = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y)
                                line.To = Vector2.new(vector.X, vector.Y)
                                line.Visible = true
                            else
                                line.Visible = false
                            end
                            activeNPCs[obj] = true
                        end
                    end
                end
            end
            for obj, line in pairs(espNPCLines) do
                if not activeNPCs[obj] then if line then line:Remove() end espNPCLines[obj] = nil end
            end
        else
            for _, line in pairs(espNPCLines) do if line then line:Remove() end end
            espNPCLines = {}
        end

        if Config.ESPTracerPlayer then
            local activeTracers = {}
            for _, player in ipairs(Players:GetPlayers()) do
                if player ~= LocalPlayer and player.Character then
                    updateTracerSkeleton(player.Character, espPlayerTracers, Color3.fromRGB(255, 255, 255))
                    activeTracers[player.Character] = true
                end
            end
            for char, lines in pairs(espPlayerTracers) do
                if not activeTracers[char] then
                    for _, l in pairs(lines) do if l then l:Remove() end end
                    espPlayerTracers[char] = nil
                end
            end
        else
            for _, lines in pairs(espPlayerTracers) do
                for _, l in pairs(lines) do if l then l:Remove() end end
            end
            espPlayerTracers = {}
        end

        if Config.ESPTracerNPC then
            local activeNPCTracers = {}
            for _, obj in ipairs(workspace:GetDescendants()) do
                if obj:IsA("Model") and obj:FindFirstChildOfClass("Humanoid") and not IsPlayer(obj) then
                    updateTracerSkeleton(obj, espNPCTracers, Color3.fromRGB(255, 0, 0))
                    activeNPCTracers[obj] = true
                end
            end
            for obj, lines in pairs(espNPCTracers) do
                if not activeNPCTracers[obj] then
                    for _, l in pairs(lines) do if l then l:Remove() end end
                    espNPCTracers[obj] = nil
                end
            end
        else
            for _, lines in pairs(espNPCTracers) do
                for _, l in pairs(lines) do if l then l:Remove() end end
            end
            espNPCTracers = {}
        end
    end)
end)

local plr = game.Players.LocalPlayer
local RS = game:GetService("ReplicatedStorage")
local TweenService = game:GetService("TweenService")
local VirtualUser = game:GetService("VirtualUser")
local UIS = game:GetService("UserInputService")
local Lighting = game:GetService("Lighting")
local RunService = game:GetService("RunService")
local Players = game:GetService("Players")

-- VARIABLES PARA STATS
local rebirthsGanados = 0
local rebirthAnterior = 0
local antiAfkStart = tick()

-- NUEVAS STATS PARA x3 TODOS
local tandasAll3 = 0
local abiertosAll3 = 0

-- TABLAS PARA GUARDAR VALORES ORIGINALES
local originalSettings = {}
local changedObjects = {}

-- VARIABLES PARA LOCK POS
local lockPos = false
local savedCFrame = nil
local lockLoop = nil

-- ANTI AFK
pcall(function()
    plr.Idled:Connect(function()
        VirtualUser:CaptureController()
        VirtualUser:ClickButton2(Vector2.new())
    end)
    task.spawn(function()
        while true do
            task.wait(30)
            VirtualUser:CaptureController()
            VirtualUser:ClickButton2(Vector2.new())
        end
    end)
end)

local gui = Instance.new("ScreenGui")
gui.Name = "DarkHubV18"
gui.ResetOnSpawn = false
gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
gui.Parent = plr:WaitForChild("PlayerGui")
gui.DisplayOrder = 999

-- FONDO PRINCIPAL - PEQUEÑA
local main = Instance.new("Frame", gui)
main.Size = UDim2.new(0, 306, 0, 362)
main.Position = UDim2.new(0.5, -153, 0.5, -181)
main.BackgroundColor3 = Color3.fromRGB(5,0,12)
main.BorderSizePixel = 0
main.Visible = false
main.ClipsDescendants = true
main.Active = true
Instance.new("UICorner", main).CornerRadius = UDim.new(0,16)

-- HACER PANEL ARRASTRABLE
local dragging = false
local dragStart = nil
local startPos = nil
main.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = main.Position
    end
end)
main.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement and dragging then
        local delta = input.Position - dragStart
        main.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)
main.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then dragging = false end
end)

local shadow = Instance.new("ImageLabel", main)
shadow.Size = UDim2.new(1,20,1,20)
shadow.Position = UDim2.new(0,-10,0,-10)
shadow.BackgroundTransparency = 1
shadow.Image = "rbxassetid://1316045217"
shadow.ImageColor3 = Color3.fromRGB(200,0,255)
shadow.ImageTransparency = 0.5
shadow.ScaleType = Enum.ScaleType.Slice
shadow.SliceCenter = Rect.new(10,10,118,118)
shadow.ZIndex = 0

-- FONDO
local bg = Instance.new("ImageLabel", main)
bg.Size = UDim2.new(1,0,1,0)
bg.BackgroundTransparency = 1
bg.Image = "rbxassetid://952798937837694"
bg.ImageTransparency = 0.2
bg.ScaleType = Enum.ScaleType.Crop
bg.ZIndex = 1

local gradient = Instance.new("UIGradient", main)
gradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(25,0,50)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(60,15,90))
}
gradient.Rotation = 45

local stroke = Instance.new("UIStroke", main)
stroke.Color = Color3.fromRGB(230,80,255)
stroke.Thickness = 3
stroke.Transparency = 0.1

-- TITULO
local title = Instance.new("TextLabel", main)
title.Size = UDim2.new(1,0,0,32)
title.Text = "✨ DARK HUB VOID V18.0 ✨"
title.TextColor3 = Color3.fromRGB(255,150,255)
title.BackgroundTransparency = 1
title.Font = Enum.Font.SourceSansBold
title.TextSize = 15
title.ZIndex = 2

local subtitle = Instance.new("TextLabel", main)
subtitle.Size = UDim2.new(1,0,0,14)
subtitle.Position = UDim2.new(0,0,0,30)
subtitle.Text = "🔮 Welcome "..plr.Name.." | 👑 Anti-AFK ON"
subtitle.TextColor3 = Color3.fromRGB(200,160,255)
subtitle.BackgroundTransparency = 1
subtitle.Font = Enum.Font.GothamSemibold
subtitle.TextSize = 10
subtitle.ZIndex = 2

-- TABS
local tabFrame = Instance.new("Frame", main)
tabFrame.Size = UDim2.new(1,-18,0,36)
tabFrame.Position = UDim2.new(0,9,0,48)
tabFrame.BackgroundColor3 = Color3.fromRGB(15,0,30)
tabFrame.BackgroundTransparency = 0.1
tabFrame.BorderSizePixel = 0
tabFrame.ZIndex = 2
Instance.new("UICorner", tabFrame).CornerRadius = UDim.new(0,12)
local layout = Instance.new("UIListLayout", tabFrame)
layout.Padding = UDim.new(0,6)
layout.FillDirection = Enum.FillDirection.Horizontal
layout.HorizontalAlignment = Enum.HorizontalAlignment.Center

local pages = {}
local tabData = {
    {"💠", "Crystals"},
    {"⚡", "Farm"},
    {"🌌", "Teleport"},
    {"📈", "Stats"}
}

for i, data in ipairs(tabData) do
    local icon, tabName = data[1], data[2]
    local tabBtn = Instance.new("TextButton", tabFrame)
    tabBtn.Size = UDim2.new(0, 72, 1, -6)
    tabBtn.Text = icon.." "..tabName
    tabBtn.BackgroundColor3 = i == 1 and Color3.fromRGB(180,0,255) or Color3.fromRGB(25,10,40)
    tabBtn.TextColor3 = Color3.fromRGB(230,150,255)
    tabBtn.Font = Enum.Font.GothamBold
    tabBtn.TextSize = 10
    tabBtn.ZIndex = 2
    Instance.new("UICorner", tabBtn).CornerRadius = UDim.new(0,10)
    local tabStroke = Instance.new("UIStroke", tabBtn)
    tabStroke.Color = Color3.fromRGB(200,0,255)
    tabStroke.Thickness = 2
    tabStroke.Transparency = i == 1 and 0 or 0.4

    local page = Instance.new("ScrollingFrame", main)
    page.Size = UDim2.new(1,-18,1,-90)
    page.Position = UDim2.new(0,9,0,90)
    page.BackgroundTransparency = 1
    page.ScrollBarThickness = 4
    page.ScrollBarImageColor3 = Color3.fromRGB(230,80,255)
    page.Visible = tabName == "Crystals"
    page.ZIndex = 2
    pages[tabName] = page

    tabBtn.MouseButton1Click:Connect(function()
        for _,p in pairs(pages) do p.Visible = false end
        for _,b in pairs(tabFrame:GetChildren()) do
            if b:IsA("TextButton") then
                TweenService:Create(b, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(25,10,40)}):Play()
                b.TextColor3 = Color3.fromRGB(230,150,255)
                b:FindFirstChild("UIStroke").Transparency = 0.4
            end
        end
        page.Visible = true
        TweenService:Create(tabBtn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(180,0,255)}):Play()
        tabBtn.TextColor3 = Color3.fromRGB(255,255,255)
        tabBtn:FindFirstChild("UIStroke").Transparency = 0
    end)
end

-- BOTON
local btn = Instance.new("ImageButton", gui)
btn.Size = UDim2.new(0,48,0,48)
btn.Position = UDim2.new(0,18,0,18)
btn.Image = "rbxassetid://6031094674"
btn.ImageColor3 = Color3.fromRGB(255,255,255)
btn.BackgroundColor3 = Color3.fromRGB(190,0,255)
btn.Draggable = true
btn.ZIndex = 3
Instance.new("UICorner", btn).CornerRadius = UDim.new(1,0)
local strokeBtn = Instance.new("UIStroke", btn)
strokeBtn.Color = Color3.fromRGB(230,80,255)
strokeBtn.Thickness = 4
local gradientBtn = Instance.new("UIGradient", btn)
gradientBtn.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(255,0,255)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(180,0,255)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(120,0,200))
}
gradientBtn.Rotation = 45

local isOpen = false
btn.MouseButton1Click:Connect(function()
    isOpen = not isOpen
    main.Visible = isOpen
    TweenService:Create(stroke, TweenInfo.new(0.3), {Color = isOpen and Color3.fromRGB(230,80,255) or Color3.fromRGB(190,0,255)}):Play()
end)

task.spawn(function()
	while true do
		TweenService:Create(btn, TweenInfo.new(3, Enum.EasingStyle.Linear), {Rotation = 360}):Play()
		task.wait(3)
		btn.Rotation = 0
	end
end)

-- FUNCIONES
local function CreateToggle(parent, text, posY, callback)
    local frame = Instance.new("Frame", parent)
    frame.Size = UDim2.new(1,-8,0,32)
    frame.Position = UDim2.new(0,4,0,posY)
    frame.BackgroundColor3 = Color3.fromRGB(25,10,40)
    frame.BorderSizePixel = 0
    frame.ZIndex = 2
    Instance.new("UICorner", frame).CornerRadius = UDim.new(0,9)
    Instance.new("UIStroke", frame).Color = Color3.fromRGB(120,0,180)
    local label = Instance.new("TextLabel", frame)
    label.Size = UDim2.new(1,-40,1,0)
    label.Position = UDim2.new(0,7,0,0)
    label.Text = text
    label.BackgroundTransparency = 1
    label.TextColor3 = Color3.fromRGB(240,200,255)
    label.Font = Enum.Font.GothamBold
    label.TextSize = 10
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.ZIndex = 2
    local b = Instance.new("TextButton", frame)
    b.Size = UDim2.new(0,30,0,16)
    b.Position = UDim2.new(1,-34,0.5,-8)
    b.Text = ""
    b.BackgroundColor3 = Color3.fromRGB(50,50,50)
    b.ZIndex = 2
    Instance.new("UICorner", b).CornerRadius = UDim.new(1,0)
    local circle = Instance.new("Frame", b)
    circle.Size = UDim2.new(0,12,0,12)
    circle.Position = UDim2.new(0,2,0,2)
    circle.BackgroundColor3 = Color3.fromRGB(220,220,220)
    circle.ZIndex = 3
    Instance.new("UICorner", circle).CornerRadius = UDim.new(1,0)
    local state = false
    b.MouseButton1Click:Connect(function()
        state = not state
        TweenService:Create(b, TweenInfo.new(0.2), {BackgroundColor3 = state and Color3.fromRGB(180,0,255) or Color3.fromRGB(50,50,50)}):Play()
        TweenService:Create(circle, TweenInfo.new(0.2), {Position = state and UDim2.new(0,16,0,2) or UDim2.new(0,2,0,2)}):Play()
        callback(state)
    end)
end

local function CreateButton(parent, text, posY, callback)
    local b = Instance.new("TextButton", parent)
    b.Size = UDim2.new(1,-8,0,30)
    b.Position = UDim2.new(0,4,0,posY)
    b.Text = text
    b.BackgroundColor3 = Color3.fromRGB(40,0,80)
    b.TextColor3 = Color3.fromRGB(230,150,255)
    b.Font = Enum.Font.GothamBold
    b.TextSize = 12
    b.ZIndex = 2
    Instance.new("UICorner", b).CornerRadius = UDim.new(0,10)
    local s = Instance.new("UIStroke", b)
    s.Color = Color3.fromRGB(200,0,255)
    s.Thickness = 2
    s.Transparency = 0.3
    b.MouseButton1Click:Connect(function()
        TweenService:Create(b, TweenInfo.new(0.1), {Size = UDim2.new(1,-12,0,26)}):Play()
        task.wait(0.1)
        TweenService:Create(b, TweenInfo.new(0.1), {Size = UDim2.new(1,-8,0,30)}):Play()
        callback()
    end)
end

local function CreateLabel(parent, text, posY, color)
    local l = Instance.new("TextLabel", parent)
    l.Size = UDim2.new(1,-8,0,18)
    l.Position = UDim2.new(0,4,0,posY)
    l.Text = text
    l.BackgroundTransparency = 1
    l.TextColor3 = color or Color3.fromRGB(230,150,255)
    l.Font = Enum.Font.GothamBold
    l.TextSize = 12
    l.TextXAlignment = Enum.TextXAlignment.Left
    l.ZIndex = 2
    return l
end

-- CRYSTALS
CreateLabel(pages["Crystals"], "💎 CRISTALES DIVINOS", 4)
local autoEltrax = false
CreateToggle(pages["Crystals"], "Auto Eltrax Crystal", 24, function(state)
    autoEltrax = state
    task.spawn(function()
        while autoEltrax do
            pcall(function() RS:WaitForChild("rEvents"):WaitForChild("openCrystalRemote"):InvokeServer("openCrystal", "Eltrax Crystal") end)
            task.wait(0.3)
        end
    end)
end)

local autoMasters = false
CreateToggle(pages["Crystals"], "Auto Masters Crystal", 60, function(state)
    autoMasters = state
    task.spawn(function()
        while autoMasters do
            pcall(function()
                local args = {[1] = "openCrystal",[2] = "Insufficient Masters Crystal"}
                RS:WaitForChild("rEvents"):WaitForChild("openCrystalRemote"):InvokeServer(unpack(args))
            end)
            task.wait(0.3)
        end
    end)
end)

local autoWeakness = false
CreateToggle(pages["Crystals"], "Auto Weakness Crystal", 96, function(state)
    autoWeakness = state
    task.spawn(function()
        while autoWeakness do
            pcall(function() RS:WaitForChild("rEvents"):WaitForChild("openCrystalRemote"):InvokeServer("openCrystal", "Weakness Crystal") end)
            task.wait(0.3)
        end
    end)
end)

-- AUTO SPACE CRYSTAL
local autoSpace = false
CreateToggle(pages["Crystals"], "Auto Space Crystal", 132, function(state)
    autoSpace = state
    task.spawn(function()
        while autoSpace do
            pcall(function()
                local args = {[1] = "openCrystal",[2] = "True Space Crystal"}
                RS:WaitForChild("rEvents"):WaitForChild("openCrystalRemote"):InvokeServer(unpack(args))
            end)
            task.wait(0.3)
        end
    end)
end)

-- NUEVO LOST CRYSTAL 🔥
local autoLost = false
CreateToggle(pages["Crystals"], "Auto Lost Crystal", 168, function(state)
    autoLost = state
    task.spawn(function()
        while autoLost do
            pcall(function()
                local args = {[1] = "openCrystal",[2] = "Lost Crystal"}
                RS:WaitForChild("rEvents"):WaitForChild("openCrystalRemote"):InvokeServer(unpack(args))
            end)
            task.wait(0.3)
        end
    end)
end)

local autoOpenAll3 = false
CreateToggle(pages["Crystals"], "3 en 3 Eltrax Crystal", 204, function(state)
    autoOpenAll3 = state
    task.spawn(function()
        while autoOpenAll3 do
            pcall(function() RS:WaitForChild("rEvents"):WaitForChild("openCrystalRemote"):InvokeServer("openCrystal", "Eltrax Crystal") end)
            pcall(function() RS:WaitForChild("rEvents"):WaitForChild("openCrystalRemote"):InvokeServer("openCrystal", "Masters Crystal") end)
            pcall(function() RS:WaitForChild("rEvents"):WaitForChild("openCrystalRemote"):InvokeServer("openCrystal", "Weakness Crystal") end)
            tandasAll3 = tandasAll3 + 1
            abiertosAll3 = abiertosAll3 + 3
            task.wait(0.1)
        end
    end)
end)

-- NUEVO 3 EN 3 SPACE CRYSTAL 🔥
local autoOpenSpace3 = false
CreateToggle(pages["Crystals"], "3 en 3 Space Crystal", 240, function(state)
    autoOpenSpace3 = state
    task.spawn(function()
        while autoOpenSpace3 do
            pcall(function()
                local args = {[1] = "openCrystal",[2] = "True Space Crystal"}
                RS:WaitForChild("rEvents"):WaitForChild("openCrystalRemote"):InvokeServer(unpack(args))
            end)
            pcall(function()
                local args = {[1] = "openCrystal",[2] = "True Space Crystal"}
                RS:WaitForChild("rEvents"):WaitForChild("openCrystalRemote"):InvokeServer(unpack(args))
            end)
            pcall(function()
                local args = {[1] = "openCrystal",[2] = "True Space Crystal"}
                RS:WaitForChild("rEvents"):WaitForChild("openCrystalRemote"):InvokeServer(unpack(args))
            end)
            tandasAll3 = tandasAll3 + 1
            abiertosAll3 = abiertosAll3 + 3
            task.wait(0.1)
        end
    end)
end)

CreateLabel(pages["Crystals"], "🐾 EVOLUCIONAR PETS", 276, Color3.fromRGB(230,150,255))
local autoEvolve = false
CreateToggle(pages["Crystals"], "Auto Evolve All", 294, function(state)
    autoEvolve = state
    task.spawn(function()
        while autoEvolve do
            pcall(function() RS:WaitForChild("rEvents"):WaitForChild("petEvolveEvent"):FireServer("evolveAll") end)
            task.wait(1)
        end
    end)
end)
CreateButton(pages["Crystals"], "✨ Evolucionar Todos ✨", 330, function() pcall(function() RS:WaitForChild("rEvents"):WaitForChild("petEvolveEvent"):FireServer("evolveAll") end) end)

-- FARM - LOCK POSITION DEFINITIVO
CreateLabel(pages["Farm"], "💪 ZONA DE FARMEO", 4)
local autoLift = false
CreateToggle(pages["Farm"], "Auto Lift", 24, function(state)
    autoLift = state
    pcall(function() plr:WaitForChild("muscleEvent"):FireServer("toggleAutoLift") end)
end)

CreateToggle(pages["Farm"], "Bloquear Posicion", 60, function(state)
    lockPos = state
    local char = plr.Character or plr.CharacterAdded:Wait()
    local hrp = char:WaitForChild("HumanoidRootPart")
    local humanoid = char:WaitForChild("Humanoid")

    if state then
        savedCFrame = hrp.CFrame
        humanoid:SetStateEnabled(Enum.HumanoidStateType.FallingDown, false)
        humanoid:SetStateEnabled(Enum.HumanoidStateType.Ragdoll, false)
        humanoid:SetStateEnabled(Enum.HumanoidStateType.GettingUp, false)

        lockLoop = RunService.Heartbeat:Connect(function()
            if plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
                local hrp = plr.Character.HumanoidRootPart
                hrp.CFrame = savedCFrame
                hrp.AssemblyLinearVelocity = Vector3.new(0,0,0)
                hrp.AssemblyAngularVelocity = Vector3.new(0,0,0)
            end
        end)

        plr.CharacterAdded:Connect(function(char)
            task.wait(0.5)
            if lockPos then
                local hrp = char:WaitForChild("HumanoidRootPart")
                local humanoid = char:WaitForChild("Humanoid")
                savedCFrame = hrp.CFrame
                humanoid:SetStateEnabled(Enum.HumanoidStateType.FallingDown, false)
                humanoid:SetStateEnabled(Enum.HumanoidStateType.Ragdoll, false)
            end
        end)
    else
        if lockLoop then lockLoop:Disconnect() end
        lockLoop = nil
        if plr.Character and plr.Character:FindFirstChild("Humanoid") then
            local humanoid = plr.Character.Humanoid
            humanoid:SetStateEnabled(Enum.HumanoidStateType.FallingDown, true)
            humanoid:SetStateEnabled(Enum.HumanoidStateType.Ragdoll, true)
            humanoid:SetStateEnabled(Enum.HumanoidStateType.GettingUp, true)
        end
    end
end)

-- AUTO GOLPEAR NUEVO 🔥
local autoHit = false
CreateToggle(pages["Farm"], "Auto Golpear", 96, function(state)
    autoHit = state
    task.spawn(function()
        while autoHit do
            pcall(function()
                -- OPCION 1: Click automatico - sirve para la mayoria
                VirtualUser:CaptureController()
                VirtualUser:Button1Down(Vector2.new())
                task.wait(0.05)
                VirtualUser:Button1Up(Vector2.new())

                -- OPCION 2: Si el juego usa Remote para golpear descomenta esta linea
                -- RS:WaitForChild("rEvents"):WaitForChild("hitRemote"):FireServer()
            end)
            task.wait(0.1) -- Velocidad del golpe. Bajala para mas rapido
        end
    end)
end)

CreateLabel(pages["Farm"], "⚡ ASCENSION DIVINA", 132, Color3.fromRGB(230,150,255))
local autoAscend = false
CreateToggle(pages["Farm"], "Auto Ascender", 150, function(state)
    autoAscend = state
    task.spawn(function()
        while autoAscend do
            pcall(function() RS:WaitForChild("rEvents"):WaitForChild("ascensionRemote"):InvokeServer("ascensionRequest") end)
            task.wait(5)
        end
    end)
end)
CreateButton(pages["Farm"], "🚀 Ascender Ahora 🚀", 186, function() pcall(function() RS:WaitForChild("rEvents"):WaitForChild("ascensionRemote"):InvokeServer("ascensionRequest") end) end)

-- TELEPORT
CreateLabel(pages["Teleport"], "🌍 TP ZONAS", 4)
local zones = {
    ["👑 Rey"] = CFrame.new(-8589, 17, -5682),
    ["🏆 Leyendas"] = CFrame.new(4571, 991, -3896),
    ["✨ Divina"] = CFrame.new(-1051, 26, -3130),
    ["🚀 Espacio"] = CFrame.new(-195, 52529, -747),
    ["⚔️ Guerreros"] = CFrame.new(-4146, 7, 1625),
}
local y = 24
for name,cf in pairs(zones) do
    CreateButton(pages["Teleport"], "TP "..name, y, function()
        local char = plr.Character or plr.CharacterAdded:Wait()
        char:WaitForChild("HumanoidRootPart").CFrame = cf
    end)
    y = y + 34
end

CreateLabel(pages["Teleport"], "💠 TP CRISTALES", y + 4, Color3.fromRGB(230,150,255))
y = y + 24
local crystalZones = {
    ["👑 Cristal Master"] = CFrame.new(-887, 7, -132),
    ["☠️ Cristal Debilidad"] = CFrame.new(-79, 3, 1870),
    ["💎 Cristal Eltrax"] = CFrame.new(-205, 7, -626),
    ["🌀 Cristal Lost"] = CFrame.new(-56377, 9, 26937),
    ["🚀 Cristal Space"] = CFrame.new(-610, 6, -564),
}
for name,cf in pairs(crystalZones) do
    CreateButton(pages["Teleport"], name, y, function()
        local char = plr.Character or plr.CharacterAdded:Wait()
        char:WaitForChild("HumanoidRootPart").CFrame = cf
    end)
    y = y + 34
end

-- STATS
CreateLabel(pages["Stats"], "📊 ESTADISTICAS EN VIVO", 4)
local fuerzaLabel = CreateLabel(pages["Stats"], "💪 Fuerza = Cargando...", 24, Color3.fromRGB(255,255,255))
local rebirthLabel = CreateLabel(pages["Stats"], "🔄 Rebirth = Cargando...", 44, Color3.fromRGB(255,255,255))
local ganadosLabel = CreateLabel(pages["Stats"], "✨ Rebirths Ganados = 0", 64, Color3.fromRGB(120,255,140))
local antiAfkTimerLabel = CreateLabel(pages["Stats"], "⏰ Anti-AFK Activo: 00:00:00", 84, Color3.fromRGB(120,200,255))

-- CREDITOS
CreateLabel(pages["Stats"], "👑 CREADOR DEL SCRIP: SEBASTIAN_87798", 104, Color3.fromRGB(255,215,0))

CreateLabel(pages["Stats"], "📦 AUTO x3 TODOS", 124, Color3.fromRGB(255,180,255))
local tandasAll3Label = CreateLabel(pages["Stats"], "📦 Tandas x3: 0", 142, Color3.fromRGB(100,200,255))
local abiertosAll3Label = CreateLabel(pages["Stats"], "💎 Abiertos: 0", 160, Color3.fromRGB(255,215,0))

-- FPS BOOST ULTRA ARREGLADO
local fpsBoostOn = false
CreateToggle(pages["Stats"], "🚀 FPS BOOST ULTRA", 178, function(state)
    fpsBoostOn = state
    if state then
        originalSettings.Lighting = {}
        for _,v in pairs(Lighting:GetChildren()) do
            if v:IsA("PostEffect") then
                originalSettings.Lighting[v.Name] = v.Enabled
                v.Enabled = false
            end
        end
        originalSettings.FogEnd = Lighting.FogEnd
        originalSettings.Brightness = Lighting.Brightness
        originalSettings.Quality = settings().Rendering.QualityLevel
        Lighting.FogEnd = 100000
        Lighting.Brightness = 1
        settings().Rendering.QualityLevel = 1
        for _,v in pairs(workspace:GetDescendants()) do
            if v:IsA("ParticleEmitter") or v:IsA("Trail") then
                table.insert(changedObjects, {obj = v, prop = "Enabled", val = v.Enabled})
                v.Enabled = false
            elseif v:IsA("Decal") or v:IsA("Texture") then
                table.insert(changedObjects, {obj = v, prop = "Transparency", val = v.Transparency})
                v.Transparency = 1
            elseif v:IsA("BasePart") and v.Name ~= "HumanoidRootPart" then
                table.insert(changedObjects, {obj = v, prop = "Material", val = v.Material})
                table.insert(changedObjects, {obj = v, prop = "CastShadow", val = v.CastShadow})
                v.Material = Enum.Material.Plastic
                v.CastShadow = false
            end
        end
        print("[FPS BOOST] Activado - 0 LAG ✅")
    else
        for _,data in pairs(changedObjects) do
            pcall(function() data.obj[data.prop] = data.val end)
        end
        table.clear(changedObjects)
        for name,val in pairs(originalSettings.Lighting or {}) do
            local obj = Lighting:FindFirstChild(name)
            if obj then obj.Enabled = val end
        end
        Lighting.FogEnd = originalSettings.FogEnd or 1000
        Lighting.Brightness = originalSettings.Brightness or 1
        settings().Rendering.QualityLevel = originalSettings.Quality or 10
        print("[FPS BOOST] Desactivado - Todo restaurado ✅")
    end
end)

-- FORMATO
local suffixes = {"", "K", "M", "B", "T", "Qa", "Qi", "Sx", "Sp", "Oc", "No", "Dc"}
local function FormatNum(num)
    num = tonumber(num) or 0
    if num < 1000 then return string.format("%.2f", num) end
    local tier = math.floor(math.log(num) / math.log(1000))
    tier = math.clamp(tier, 0, #suffixes - 1)
    local scaled = num / (1000 ^ tier)
    return string.format("%.2f%s", scaled, suffixes[tier + 1])
end

local function FormatTime(seconds)
    local h = math.floor(seconds / 3600)
    local m = math.floor((seconds % 3600) / 60)
    local s = math.floor(seconds % 60)
    return string.format("%02d:%02d:%02d", h, m, s)
end

task.spawn(function()
    while true do
        task.wait(0.05)
        pcall(function()
            local leaderstats = plr:FindFirstChild("leaderstats")
            if leaderstats then
                local fuerza = leaderstats:FindFirstChild("Strength") or leaderstats:FindFirstChild("Muscle") or leaderstats:FindFirstChild("SP")
                local rebirth = leaderstats:FindFirstChild("Rebirths")
                if fuerza then fuerzaLabel.Text = "💪 Fuerza = "..FormatNum(fuerza.Value) end
                if rebirth then
                    rebirthLabel.Text = "🔄 Rebirth = "..FormatNum(rebirth.Value)
                    if rebirthAnterior == 0 then rebirthAnterior = rebirth.Value
                    elseif rebirth.Value > rebirthAnterior then
                        local ganado = rebirth.Value - rebirthAnterior
                        rebirthsGanados = rebirthsGanados + ganado
                        rebirthAnterior = rebirth.Value
                    end
                    ganadosLabel.Text = "✨ Rebirths Ganados = "..FormatNum(rebirthsGanados)
                end
            end
            local tiempoActivo = tick() - antiAfkStart
            antiAfkTimerLabel.Text = "⏰ Anti-AFK Activo: "..FormatTime(tiempoActivo)
            tandasAll3Label.Text = "📦 Tandas x3: "..tandasAll3
            abiertosAll3Label.Text = "💎 Abiertos: "..abiertosAll3
        end)
    end
end)

print("[DARK HUB V18.0] Cargado - FPS BOOST ULTRA 💜")

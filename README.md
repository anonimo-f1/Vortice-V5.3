-- =============================================
-- VÓRTICE V5.3 - PROTEGIDO COM SENHA
-- CRIADO POR: ANONIMO F
-- SENHA: anonimo2025
-- NÃO TENTE ROUBAR
-- =============================================

local AUTHOR = "ANONIMO F"
local VERSION = "V5.3"
local YOUTUBE = "https://youtube.com/@anonimof-v7e"
local INSTAGRAM = "https://www.instagram.com/darkff300"
local CORRECT_PASSWORD = "anonimo2025"
local MAX_ATTEMPTS = 3
local attempts = 0

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local player = Players.LocalPlayer

-- =============================================
-- TELA DE SENHA (BLOQUEIA TUDO)
-- =============================================

local PasswordGui = Instance.new("ScreenGui")
PasswordGui.Name = "VorticePasswordLock"
PasswordGui.Parent = player:WaitForChild("PlayerGui")
PasswordGui.ResetOnSpawn = false

local LockFrame = Instance.new("Frame")
LockFrame.Size = UDim2.new(1, 0, 1, 0)
LockFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
LockFrame.Parent = PasswordGui

local LockTitle = Instance.new("TextLabel")
LockTitle.Size = UDim2.new(0.6, 0, 0.2, 0)
LockTitle.Position = UDim2.new(0.2, 0, 0.2, 0)
LockTitle.BackgroundTransparency = 1
LockTitle.Text = "VÓRTICE " .. VERSION
LockTitle.TextColor3 = Color3.fromRGB(0, 255, 0)
LockTitle.Font = Enum.Font.Arcade
LockTitle.TextScaled = true
LockTitle.Parent = LockFrame

local AuthorLabel = Instance.new("TextLabel")
AuthorLabel.Size = UDim2.new(0.6, 0, 0.1, 0)
AuthorLabel.Position = UDim2.new(0.2, 0, 0.35, 0)
AuthorLabel.BackgroundTransparency = 1
AuthorLabel.Text = "POR: " .. AUTHOR
AuthorLabel.TextColor3 = Color3.fromRGB(100, 255, 100)
AuthorLabel.Font = Enum.Font.SourceSansBold
AuthorLabel.TextScaled = true
AuthorLabel.Parent = LockFrame

local PasswordBox = Instance.new("TextBox")
PasswordBox.Size = UDim2.new(0.6, 0, 0.1, 0)
PasswordBox.Position = UDim2.new(0.2, 0, 0.5, 0)
PasswordBox.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
PasswordBox.BorderColor3 = Color3.fromRGB(0, 255, 0)
PasswordBox.BorderSizePixel = 2
PasswordBox.PlaceholderText = "Digite a senha..."
PasswordBox.Text = ""
PasswordBox.TextColor3 = Color3.fromRGB(0, 255, 0)
PasswordBox.Font = Enum.Font.Code
PasswordBox.TextScaled = true
PasswordBox.ClearTextOnFocus = false
PasswordBox.Parent = LockFrame

local AttemptsLabel = Instance.new("TextLabel")
AttemptsLabel.Size = UDim2.new(0.6, 0, 0.08, 0)
AttemptsLabel.Position = UDim2.new(0.2, 0, 0.62, 0)
AttemptsLabel.BackgroundTransparency = 1
AttemptsLabel.Text = "Tentativas: 0/" .. MAX_ATTEMPTS
AttemptsLabel.TextColor3 = Color3.fromRGB(255, 255, 0)
AttemptsLabel.Font = Enum.Font.SourceSans
AttemptsLabel.TextScaled = true
AttemptsLabel.Parent = LockFrame

local StatusLabel = Instance.new("TextLabel")
StatusLabel.Size = UDim2.new(0.6, 0, 0.08, 0)
StatusLabel.Position = UDim2.new(0.2, 0, 0.7, 0)
StatusLabel.BackgroundTransparency = 1
StatusLabel.Text = ""
StatusLabel.TextColor3 = Color3.fromRGB(255, 0, 0)
StatusLabel.Font = Enum.Font.SourceSansBold
StatusLabel.TextScaled = true
StatusLabel.Parent = LockFrame

-- Som de erro
local errorSound = Instance.new("Sound")
errorSound.SoundId = "rbxassetid://5583566146"
errorSound.Volume = 0.8
errorSound.Parent = PasswordGui

-- =============================================
-- SCRIPT PRINCIPAL (FUNCIONALIDADES COMPLETAS)
-- =============================================

local function loadMainScript()
    local TweenService = game:GetService("TweenService")
    local Players = game:GetService("Players")
    local RunService = game:GetService("RunService")
    local player = Players.LocalPlayer
    local humanoid = nil
    local speedEnabled = false
    local targetSpeed = 35

    local ScreenGui = Instance.new("ScreenGui")
    ScreenGui.Name = "Vórtice"
    ScreenGui.Parent = player:WaitForChild("PlayerGui")
    ScreenGui.ResetOnSpawn = false

    local MainFrame = Instance.new("Frame")
    MainFrame.Name = "MainFrame"
    MainFrame.Parent = ScreenGui
    MainFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    MainFrame.BorderSizePixel = 0
    MainFrame.Position = UDim2.new(0.4, 0, 0.4, 0)
    MainFrame.Size = UDim2.new(0, 250, 0, 380)
    MainFrame.Active = true
    MainFrame.Draggable = true

    -- 🎨 EFEITO COLORIDO MAIS RÁPIDO - CORRIGIDO
    local colorTransitionConnection
    local function startColorTransition()
        local colors = {
            Color3.fromRGB(255, 0, 0),      -- Vermelho
            Color3.fromRGB(255, 128, 0),    -- Laranja
            Color3.fromRGB(255, 255, 0),    -- Amarelo
            Color3.fromRGB(0, 255, 0),      -- Verde
            Color3.fromRGB(0, 255, 255),    -- Ciano
            Color3.fromRGB(0, 0, 255),      -- Azul
            Color3.fromRGB(255, 0, 255),    -- Magenta
            Color3.fromRGB(255, 0, 128)     -- Rosa
        }
        
        local currentIndex = 1
        colorTransitionConnection = RunService.Heartbeat:Connect(function()
            currentIndex = currentIndex + 0.03 -- 🚀 MAIS RÁPIDO AGORA
            if currentIndex >= #colors + 1 then
                currentIndex = 1
            end
            
            local index1 = math.floor(currentIndex)
            local index2 = (index1 % #colors) + 1
            local alpha = currentIndex - index1
            
            if colors[index1] and colors[index2] then
                MainFrame.BackgroundColor3 = colors[index1]:Lerp(colors[index2], alpha)
            end
        end)
    end

    -- INTERFACE COMPLETA
    local TitleBar = Instance.new("Frame")
    TitleBar.Name = "TitleBar"
    TitleBar.Parent = MainFrame
    TitleBar.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    TitleBar.Size = UDim2.new(1, 0, 0, 30)

    local Title = Instance.new("TextLabel")
    Title.Parent = TitleBar
    Title.BackgroundTransparency = 1
    Title.Size = UDim2.new(1, 0, 1, 0)
    Title.Font = Enum.Font.SourceSansBold
    Title.Text = "VÓRTICE"
    Title.TextColor3 = Color3.fromRGB(0, 255, 0)
    Title.TextSize = 18

    local VersionLabel = Instance.new("TextLabel")
    VersionLabel.Parent = MainFrame
    VersionLabel.BackgroundTransparency = 1
    VersionLabel.Position = UDim2.new(0, 0, 0, 30)
    VersionLabel.Size = UDim2.new(1, 0, 0, 20)
    VersionLabel.Font = Enum.Font.SourceSans
    VersionLabel.Text = "versão V5.3"
    VersionLabel.TextColor3 = Color3.fromRGB(100, 255, 100)
    VersionLabel.TextSize = 14

    local StatusLabel = Instance.new("TextLabel")
    StatusLabel.Parent = MainFrame
    StatusLabel.BackgroundTransparency = 1
    StatusLabel.Position = UDim2.new(0, 0, 0, 50)
    StatusLabel.Size = UDim2.new(1, 0, 0, 20)
    StatusLabel.Font = Enum.Font.SourceSans
    StatusLabel.Text = "DESLIGADO"
    StatusLabel.TextColor3 = Color3.fromRGB(255, 0, 0)
    StatusLabel.TextSize = 16

    local MinimizeButton = Instance.new("TextButton")
    MinimizeButton.Parent = TitleBar
    MinimizeButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    MinimizeButton.Position = UDim2.new(1, -60, 0, 0)
    MinimizeButton.Size = UDim2.new(0, 30, 0, 30)
    MinimizeButton.Font = Enum.Font.SourceSansBold
    MinimizeButton.Text = "-"
    MinimizeButton.TextColor3 = Color3.fromRGB(255, 255, 0)
    MinimizeButton.TextSize = 20

    local CloseButton = Instance.new("TextButton")
    CloseButton.Parent = TitleBar
    CloseButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    CloseButton.Position = UDim2.new(1, -30, 0, 0)
    CloseButton.Size = UDim2.new(0, 30, 0, 30)
    CloseButton.Font = Enum.Font.SourceSansBold
    CloseButton.Text = "X"
    CloseButton.TextColor3 = Color3.fromRGB(255, 0, 0)
    CloseButton.TextSize = 20

    local ESPButton = Instance.new("TextButton")
    ESPButton.Name = "ESPButton"
    ESPButton.Parent = MainFrame
    ESPButton.BackgroundColor3 = Color3.fromRGB(255, 100, 100)
    ESPButton.Position = UDim2.new(0.1, 0, 0.25, 0)
    ESPButton.Size = UDim2.new(0.8, 0, 0, 40)
    ESPButton.Font = Enum.Font.SourceSansBold
    ESPButton.Text = "ESP ULTRA"
    ESPButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    ESPButton.TextSize = 20

    local SpeedFrame = Instance.new("Frame")
    SpeedFrame.Parent = MainFrame
    SpeedFrame.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    SpeedFrame.Position = UDim2.new(0.1, 0, 0.45, 0)
    SpeedFrame.Size = UDim2.new(0.8, 0, 0, 60)
    SpeedFrame.BorderSizePixel = 1
    SpeedFrame.BorderColor3 = Color3.fromRGB(150, 150, 150)

    local SpeedLabel = Instance.new("TextLabel")
    SpeedLabel.Parent = SpeedFrame
    SpeedLabel.BackgroundTransparency = 1
    SpeedLabel.Size = UDim2.new(1, 0, 0, 20)
    SpeedLabel.Position = UDim2.new(0, 0, 0, 0)
    SpeedLabel.Font = Enum.Font.SourceSans
    SpeedLabel.Text = "Velocidade:"
    SpeedLabel.TextColor3 = Color3.fromRGB(100, 100, 100)
    SpeedLabel.TextSize = 14

    local SpeedBox = Instance.new("TextBox")
    SpeedBox.Parent = SpeedFrame
    SpeedBox.BackgroundColor3 = Color3.fromRGB(240, 240, 240)
    SpeedBox.Position = UDim2.new(0.1, 0, 0.35, 0)
    SpeedBox.Size = UDim2.new(0.8, 0, 0, 25)
    SpeedBox.Font = Enum.Font.SourceSans
    SpeedBox.Text = "35"
    SpeedBox.TextColor3 = Color3.fromRGB(0, 0, 0)
    SpeedBox.PlaceholderText = "1 - 99999"
    SpeedBox.TextSize = 16

    local ApplySpeedButton = Instance.new("TextButton")
    ApplySpeedButton.Parent = SpeedFrame
    ApplySpeedButton.BackgroundColor3 = Color3.fromRGB(0, 120, 255)
    ApplySpeedButton.Position = UDim2.new(0.1, 0, 0.7, 0)
    ApplySpeedButton.Size = UDim2.new(0.8, 0, 0, 20)
    ApplySpeedButton.Font = Enum.Font.SourceSansBold
    ApplySpeedButton.Text = "Aplicar Speed"
    ApplySpeedButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    ApplySpeedButton.TextSize = 14

    -- ✅ BOTÕES DE CRÉDITOS E REDES SOCIAIS (AGORA VISÍVEIS)
    local CreditsButton = Instance.new("TextButton")
    CreditsButton.Parent = MainFrame
    CreditsButton.BackgroundColor3 = Color3.fromRGB(200, 200, 200)
    CreditsButton.Position = UDim2.new(0.1, 0, 0.65, 0)
    CreditsButton.Size = UDim2.new(0.8, 0, 0, 30)
    CreditsButton.Font = Enum.Font.SourceSansBold
    CreditsButton.Text = "FEITO POR"
    CreditsButton.TextColor3 = Color3.fromRGB(255, 255, 0)
    CreditsButton.TextSize = 18
    CreditsButton.Visible = true

    local YouTubeButton = Instance.new("TextButton")
    YouTubeButton.Parent = MainFrame
    YouTubeButton.BackgroundColor3 = Color3.fromRGB(200, 200, 200)
    YouTubeButton.Position = UDim2.new(0.1, 0, 0.75, 0)
    YouTubeButton.Size = UDim2.new(0.8, 0, 0, 30)
    YouTubeButton.Font = Enum.Font.SourceSansBold
    YouTubeButton.Text = "YouTube"
    YouTubeButton.TextColor3 = Color3.fromRGB(255, 0, 0)
    YouTubeButton.TextSize = 18
    YouTubeButton.Visible = true

    local InstagramButton = Instance.new("TextButton")
    InstagramButton.Parent = MainFrame
    InstagramButton.BackgroundColor3 = Color3.fromRGB(200, 200, 200)
    InstagramButton.Position = UDim2.new(0.1, 0, 0.85, 0)
    InstagramButton.Size = UDim2.new(0.8, 0, 0, 30)
    InstagramButton.Font = Enum.Font.SourceSansBold
    InstagramButton.Text = "Instagram"
    InstagramButton.TextColor3 = Color3.fromRGB(255, 100, 180)
    InstagramButton.TextSize = 18
    InstagramButton.Visible = true

    -- ✅ LABEL PARA MOSTRAR "ANONIMO F"
    local CreditLabel = Instance.new("TextLabel")
    CreditLabel.Parent = MainFrame
    CreditLabel.BackgroundTransparency = 1
    CreditLabel.Position = UDim2.new(0.1, 0, 0.65, 0)
    CreditLabel.Size = UDim2.new(0.8, 0, 0, 30)
    CreditLabel.Font = Enum.Font.SourceSansBold
    CreditLabel.Text = ""
    CreditLabel.TextSize = 18
    CreditLabel.Visible = false

    -- FUNÇÃO HOVER EFFECT
    local function hoverEffect(button, normal, hover)
        normal = normal or Color3.fromRGB(200, 200, 200)
        hover = hover or Color3.fromRGB(220, 220, 220)
        button.MouseEnter:Connect(function() button.BackgroundColor3 = hover end)
        button.MouseLeave:Connect(function() button.BackgroundColor3 = normal end)
    end

    -- APLICA HOVER NOS BOTÕES
    for _, btn in {ESPButton, CreditsButton, YouTubeButton, InstagramButton, ApplySpeedButton, MinimizeButton, CloseButton} do
        hoverEffect(btn)
    end

    -- ✅ FUNCIONALIDADE ESP (COMPLETA)
    local espEnabled = false
    local originalColors = {}
    local coloredParts = {}
    local espLoop = nil
    local descendantConnection = nil

    local function isGlassPart(part)
        if not part:IsA("BasePart") then return false end
        if part.Transparency >= 1 then return false end
        if part.Size.Magnitude < 1 then return false end
        if part.Material == Enum.Material.ForceField then return false end
        return true
    end

    local function applyColor(part, isUnsafe)
        if not part or not part.Parent or coloredParts[part] then return end
        originalColors[part] = originalColors[part] or part.Color
        part.Color = isUnsafe and Color3.fromRGB(255, 0, 0) or Color3.fromRGB(0, 255, 0)
        coloredParts[part] = true
    end

    local function resetColors()
        for part, _ in pairs(coloredParts) do
            if part and part.Parent and originalColors[part] then
                part.Color = originalColors[part]
            end
        end
        coloredParts = {}
        originalColors = {}
    end

    local function scanAndColor()
        for _, part in workspace:GetDescendants() do
            if isGlassPart(part) then
                applyColor(part, part.CanCollide == false)
            end
        end
    end

    local function startESP()
        if espEnabled then return end
        resetColors()

        espEnabled = true
        StatusLabel.Text = "LIGADO (ULTRA)"
        StatusLabel.TextColor3 = Color3.fromRGB(0, 255, 0)
        ESPButton.Text = "DESATIVAR"

        scanAndColor()
        espLoop = RunService.Heartbeat:Connect(scanAndColor)

        descendantConnection = workspace.DescendantAdded:Connect(function(desc)
            if espEnabled and desc:IsA("BasePart") then
                task.defer(function()
                    if desc and desc.Parent and isGlassPart(desc) then
                        applyColor(desc, desc.CanCollide == false)
                    end
                end)
            end
        end)
    end

    local function stopESP()
        if not espEnabled then return end
        if espLoop then espLoop:Disconnect() end
        if descendantConnection then descendantConnection:Disconnect() end
        espLoop = nil
        descendantConnection = nil
        resetColors()
        espEnabled = false
        StatusLabel.Text = "DESLIGADO"
        StatusLabel.TextColor3 = Color3.fromRGB(255, 0, 0)
        ESPButton.Text = "ESP ULTRA"
    end

    ESPButton.MouseButton1Click:Connect(function()
        if espEnabled then stopESP() else startESP() end
    end)

    -- =============================================
    -- ✅ SISTEMA DE SPEED AUTOMÁTICO CORRIGIDO
    -- =============================================

    local speedMonitorConnection = nil

    -- ✅ FUNÇÃO MELHORADA PARA APLICAR SPEED
    local function applySpeed()
        local char = player.Character
        if not char then 
            print("❌ Character não encontrado")
            return false 
        end
        
        humanoid = char:FindFirstChildOfClass("Humanoid")
        if not humanoid then 
            print("❌ Humanoid não encontrado")
            return false 
        end

        local speed = tonumber(SpeedBox.Text) or targetSpeed
        if speed and speed >= 1 and speed <= 99999 then
            humanoid.WalkSpeed = speed
            targetSpeed = speed
            speedEnabled = true
            
            ApplySpeedButton.Text = "Speed: " .. speed
            task.delay(2, function()
                if ApplySpeedButton and ApplySpeedButton.Text == "Speed: " .. speed then
                    ApplySpeedButton.Text = "Aplicar Speed"
                end
            end)
            
            print("✅ Speed aplicado: " .. speed)
            return true
        else
            SpeedBox.Text = tostring(targetSpeed)
            return false
        end
    end

    -- ✅ SISTEMA DE AUTO-REAPLICAÇÃO QUANDO MORRE/RESPAWNA
    local function setupAutoRespawnSpeed()
        -- Remove conexão anterior se existir
        if speedMonitorConnection then
            speedMonitorConnection:Disconnect()
        end

        -- Aplica speed quando o character spawna
        speedMonitorConnection = player.CharacterAdded:Connect(function(char)
            print("🔄 Character respawnou, reaplicando speed...")
            task.wait(1.5) -- Espera o character carregar completamente
            
            local newHumanoid = char:FindFirstChildOfClass("Humanoid")
            if newHumanoid and speedEnabled then
                newHumanoid.WalkSpeed = targetSpeed
                humanoid = newHumanoid
                print("✅ Speed reaplicado automaticamente: " .. targetSpeed)
                
                -- Monitora se o humanoid morre novamente
                if humanoid then
                    humanoid.Died:Connect(function()
                        print("💀 Character morreu, aguardando respawn...")
                        task.wait(2)
                        setupAutoRespawnSpeed() -- Reconecta o sistema
                    end)
                end
            end
        end)

        -- Aplica speed no character atual se existir
        if player.Character then
            task.wait(2)
            humanoid = player.Character:FindFirstChildOfClass("Humanoid")
            if humanoid and speedEnabled then
                humanoid.WalkSpeed = targetSpeed
                print("✅ Speed aplicado no character atual: " .. targetSpeed)
                
                -- Monitora morte do character atual
                if humanoid then
                    humanoid.Died:Connect(function()
                        print("💀 Character morreu, aguardando respawn...")
                        task.wait(2)
                        setupAutoRespawnSpeed() -- Reconecta o sistema
                    end)
                end
            end
        end
    end

    -- ✅ BOTÃO APLICAR SPEED ATUALIZADO
    ApplySpeedButton.MouseButton1Click:Connect(function()
        if applySpeed() then
            setupAutoRespawnSpeed() -- Garante que o sistema de auto-reapply está ativo
        end
    end)

    -- ✅ BOTÃO "FEITO POR" FUNCIONAL
    local rainbowColors = {
        Color3.fromRGB(255, 0, 0),
        Color3.fromRGB(255, 127, 0),
        Color3.fromRGB(255, 255, 0),
        Color3.fromRGB(0, 255, 0),
        Color3.fromRGB(0, 0, 255),
        Color3.fromRGB(75, 0, 130),
        Color3.fromRGB(148, 0, 211)
    }

    CreditsButton.MouseButton1Click:Connect(function()
        CreditLabel.Text = "ANONIMO F"
        CreditLabel.Visible = true
        CreditsButton.Visible = false

        CreditLabel.TextTransparency = 1
        TweenService:Create(CreditLabel, TweenInfo.new(0.5), {TextTransparency = 0}):Play()

        local colorIndex = 1
        local colorConnection
        colorConnection = RunService.Heartbeat:Connect(function()
            if not CreditLabel.Visible then
                colorConnection:Disconnect()
                return
            end
            CreditLabel.TextColor3 = rainbowColors[colorIndex]
            colorIndex = (colorIndex % #rainbowColors) + 1
        end)

        task.delay(3, function()
            colorConnection:Disconnect()
            TweenService:Create(CreditLabel, TweenInfo.new(0.5), {TextTransparency = 1}):Play()
            task.delay(0.5, function()
                CreditLabel.Visible = false
                CreditsButton.Visible = true
            end)
        end)
    end)

    -- ✅ BOTÕES YOUTUBE E INSTAGRAM FUNCIONAIS
    YouTubeButton.MouseButton1Click:Connect(function()
        if setclipboard then 
            setclipboard("https://youtube.com/@anonimof-v7e?si=RDRBEenCu1UVUgBN")
        end
        local oldText = YouTubeButton.Text
        YouTubeButton.Text = "COPIADO!"
        task.wait(1.5)
        YouTubeButton.Text = oldText
    end)

    InstagramButton.MouseButton1Click:Connect(function()
        if setclipboard then 
            setclipboard("https://www.instagram.com/darkff300?igsh=MW1id3pxYmVzZTQ4cA==")
        end
        local oldText = InstagramButton.Text
        InstagramButton.Text = "COPIADO!"
        task.wait(1.5)
        InstagramButton.Text = oldText
    end)

    -- ✅ BOTÕES MINIMIZAR E FECHAR
    CloseButton.MouseButton1Click:Connect(function()
        stopESP()
        if humanoid then humanoid.WalkSpeed = 16 end
        if colorTransitionConnection then
            colorTransitionConnection:Disconnect()
        end
        if speedMonitorConnection then
            speedMonitorConnection:Disconnect()
        end
        ScreenGui:Destroy()
    end)

    MinimizeButton.MouseButton1Click:Connect(function()
        local full = UDim2.new(0, 250, 0, 380)
        local mini = UDim2.new(0, 250, 0, 30)
        if MainFrame.Size == full then
            MainFrame:TweenSize(mini, "Out", "Sine", 0.3, true)
            for _, v in MainFrame:GetChildren() do
                if v ~= TitleBar then v.Visible = false end
            end
        else
            MainFrame:TweenSize(full, "Out", "Sine", 0.3, true)
            for _, v in MainFrame:GetChildren() do
                v.Visible = true
            end
        end
    end)

    -- 🎨 INICIA O EFEITO COLORIDO
    startColorTransition()

    ScreenGui.Enabled = true

    -- ✅ MARCA D'ÁGUA
    local Watermark = Instance.new("ScreenGui")
    Watermark.Name = "VorticeWatermark"
    Watermark.Parent = player.PlayerGui
    Watermark.ResetOnSpawn = false

    local WatermarkFrame = Instance.new("Frame")
    WatermarkFrame.Size = UDim2.new(0, 300, 0, 60)
    WatermarkFrame.Position = UDim2.new(0, 10, 0, 10)
    WatermarkFrame.BackgroundTransparency = 0.3
    WatermarkFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    WatermarkFrame.BorderSizePixel = 2
    WatermarkFrame.BorderColor3 = Color3.fromRGB(0, 255, 0)
    WatermarkFrame.Parent = Watermark

    local WatermarkText = Instance.new("TextLabel")
    WatermarkText.Size = UDim2.new(1, 0, 1, 0)
    WatermarkText.BackgroundTransparency = 1
    WatermarkText.Text = AUTHOR .. " - " .. VERSION
    WatermarkText.TextColor3 = Color3.fromRGB(0, 255, 0)
    WatermarkText.Font = Enum.Font.Code
    WatermarkText.TextSize = 16
    WatermarkText.TextStrokeTransparency = 0.7
    WatermarkText.Parent = WatermarkFrame

    print("========================================")
    print("     VÓRTICE " .. VERSION .. " - LIBERADO")
    print("     SISTEMA DE SPEED AUTOMÁTICO ATIVO!")
    print("     TODAS FUNÇÕES ATIVAS!")
    print("========================================")
end

-- =============================================
-- VERIFICAÇÃO DA SENHA
-- =============================================

PasswordBox.FocusLost:Connect(function(enter)
    if not enter then return end
    attempts += 1
    AttemptsLabel.Text = "Tentativas: " .. attempts .. "/" .. MAX_ATTEMPTS

    if PasswordBox.Text == CORRECT_PASSWORD then
        StatusLabel.Text = "ACESSO LIBERADO!"
        StatusLabel.TextColor3 = Color3.fromRGB(0, 255, 0)
        task.wait(1)
        PasswordGui:Destroy()
        loadMainScript()
    else
        StatusLabel.Text = "SENHA INCORRETA!"
        errorSound:Play()
        LockFrame.BackgroundColor3 = Color3.fromRGB(100, 0, 0)
        task.delay(0.5, function()
            LockFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
        end)

        if attempts >= MAX_ATTEMPTS then
            StatusLabel.Text = "BLOQUEADO!"
            StatusLabel.TextColor3 = Color3.fromRGB(255, 0, 0)

            spawn(function()
                while true do
                    LockFrame.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
                    task.wait(0.3)
                    LockFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
                    task.wait(0.3)
                end
            end)
        end
    end
end)

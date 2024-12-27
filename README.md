-- Criação da GUI
local ScreenGui = Instance.new("ScreenGui")
local ToggleButton = Instance.new("TextButton")

-- Propriedades da GUI
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

ToggleButton.Parent = ScreenGui
ToggleButton.Size = UDim2.new(0, 200, 0, 50)
ToggleButton.Position = UDim2.new(0.5, -100, 0.5, -25)
ToggleButton.Text = "Ativar Wallhop"
ToggleButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
ToggleButton.TextSize = 20

-- Variável de controle
local isWallhopActive = false

-- Função do movimento Wallhop
local function performWallhop()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoid = character:WaitForChild("Humanoid")
    local rootPart = character:WaitForChild("HumanoidRootPart")

    -- Ação repetitiva para wallhop
    while isWallhopActive do
        wait(0.1) -- Ajuste a frequência conforme necessário
        humanoid:ChangeState(Enum.HumanoidStateType.Jumping) -- Força o pulo
        wait(0.05)
        rootPart.Velocity = Vector3.new(0, 50, 0) -- Simula o flick no ar
    end
end

-- Toggle do botão
ToggleButton.MouseButton1Click:Connect(function()
    isWallhopActive = not isWallhopActive
    if isWallhopActive then
        ToggleButton.Text = "Desativar Wallhop"
        ToggleButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
        performWallhop()
    else
        ToggleButton.Text = "Ativar Wallhop"
        ToggleButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
    end
end)

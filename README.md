local player = game.Players.LocalPlayer
local mouse = player:GetMouse()
local uis = game:GetService("UserInputService")

-- Create ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = player:WaitForChild("PlayerGui")
screenGui.Name = "AdvantageGui"
screenGui.Enabled = false

-- Create Frame
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 200, 0, 100)
frame.Position = UDim2.new(0.5, -100, 0.5, -50)
frame.BackgroundColor3 = Color3.new(0.1, 0.1, 0.1)
frame.BorderSizePixel = 0
frame.Parent = screenGui

-- Create Speed Boost Button
local speedButton = Instance.new("TextButton")
speedButton.Size = UDim2.new(1, 0, 0.5, 0)
speedButton.Position = UDim2.new(0, 0, 0, 0)
speedButton.BackgroundColor3 = Color3.new(0.2, 0.2, 0.8)
speedButton.Text = "Speed Boost"
speedButton.Parent = frame

-- Create Extra Health Button
local healthButton = Instance.new("TextButton")
healthButton.Size = UDim2.new(1, 0, 0.5, 0)
healthButton.Position = UDim2.new(0, 0, 0.5, 0)
healthButton.BackgroundColor3 = Color3.new(0.8, 0.2, 0.2)
healthButton.Text = "Extra Health"
healthButton.Parent = frame

-- Speed Boost Function
local function giveSpeedBoost()
    local character = player.Character or player.CharacterAdded:Wait()
    if character then
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid.WalkSpeed = humanoid.WalkSpeed * 2
            wait(10) -- Boost duration
            humanoid.WalkSpeed = humanoid.WalkSpeed / 2
        end
    end
end

-- Extra Health Function
local function giveExtraHealth()
    local character = player.Character or player.CharacterAdded:Wait()
    if character then
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid.MaxHealth = humanoid.MaxHealth + 50
            humanoid.Health = humanoid.MaxHealth
        end
    end
end

-- Button Click Events
speedButton.MouseButton1Click:Connect(giveSpeedBoost)
healthButton.MouseButton1Click:Connect(giveExtraHealth)

-- Key Press Event
uis.InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.G then
        screenGui.Enabled = not screenGui.Enabled
    end
end)

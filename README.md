-- Create the GUI
local TeleportGui = Instance.new("ScreenGui")
TeleportGui.Name = "TeleportGui"
TeleportGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0, 300, 0, 150)
Frame.Position = UDim2.new(0.5, -150, 0.5, -75)
Frame.BackgroundColor3 = Color3.new(1, 1, 1)
Frame.Active = true
Frame.Draggable = true -- Allow the GUI to be moved
Frame.Parent = TeleportGui

local CloseButton = Instance.new("TextButton")
CloseButton.Size = UDim2.new(0, 20, 0, 20)
CloseButton.Position = UDim2.new(1, -25, 0, 5)
CloseButton.Text = "X"
CloseButton.Parent = Frame

local PlayerLabel = Instance.new("TextLabel")
PlayerLabel.Size = UDim2.new(0, 100, 0, 25)
PlayerLabel.Position = UDim2.new(0, 10, 0, 10)
PlayerLabel.Text = "Player Name:"
PlayerLabel.Parent = Frame

local PlayerTextBox = Instance.new("TextBox")
PlayerTextBox.Size = UDim2.new(0, 200, 0, 25)
PlayerTextBox.Position = UDim2.new(0.5, -100, 0, 50) -- Adjusted position
PlayerTextBox.Parent = Frame

local TeleportButton = Instance.new("TextButton")
TeleportButton.Size = UDim2.new(0, 100, 0, 30)
TeleportButton.Position = UDim2.new(0.5, -50, 0, 100)
TeleportButton.Text = "Teleport"
TeleportButton.Parent = Frame

-- Close the GUI when the close button is clicked
CloseButton.MouseButton1Click:Connect(function()
    TeleportGui:Destroy()
end)

-- Teleport function
local function teleportToPlayer(playerName)
    local player = game.Players:FindFirstChild(playerName)
    if player then
        local character = player.Character
        if character then
            local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")
            if humanoidRootPart then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = humanoidRootPart.CFrame
            end
        end
    else
        print("Player not found.")
    end
end

-- Teleport local player to inputted player's location
TeleportButton.MouseButton1Click:Connect(function()
    local playerName = PlayerTextBox.Text
    if playerName ~= "" then
        teleportToPlayer(playerName)
    else
        print("Please enter a player name.")
    end
end)

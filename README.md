-- Hide the Invite Friend bar visually (mobile fix)
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Create the cover GUI
local coverGui = Instance.new("ScreenGui")
coverGui.Name = "InviteBarCover"
coverGui.IgnoreGuiInset = true
coverGui.ResetOnSpawn = false
coverGui.Parent = playerGui

-- Create the frame that will cover the Invite Friend bar
local coverFrame = Instance.new("Frame")
coverFrame.Name = "CoverFrame"
coverFrame.Parent = coverGui
coverFrame.AnchorPoint = Vector2.new(0.5, 0)
coverFrame.Position = UDim2.new(0.5, 0, 0, 0) -- top of the screen
coverFrame.Size = UDim2.new(1, 0, 0, 45) -- adjust height if needed
coverFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0) -- black cover
coverFrame.BackgroundTransparency = 0.4 -- 0 = solid black, 1 = fully invisible
coverFrame.BorderSizePixel = 0

-- Auto adjust for device screen size
local function adjustForScreen()
	local screenSize = workspace.CurrentCamera.ViewportSize
	if screenSize.Y > 700 then
		coverFrame.Size = UDim2.new(1, 0, 0, 50) -- taller phones
	else
		coverFrame.Size = UDim2.new(1, 0, 0, 40) -- smaller screens
	end
end

workspace.CurrentCamera:GetPropertyChangedSignal("ViewportSize"):Connect(adjustForScreen)
adjustForScreen()

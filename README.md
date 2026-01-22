-------------------------------------------------
-- BOTÃO MOBILE (AIMBOT)
-------------------------------------------------
local mobileAiming = false

local mobileGui = Instance.new("ScreenGui")
mobileGui.Name = "MobileAimButton"
mobileGui.ResetOnSpawn = false
mobileGui.Parent = player:WaitForChild("PlayerGui")

local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 70, 0, 70) -- tamanho médio
button.Position = UDim2.new(0.85, 0, 0.6, 0)
button.BackgroundColor3 = Color3.fromRGB(180, 50, 50) -- vermelho (OFF)
button.Text = "A"
button.TextColor3 = Color3.fromRGB(255,255,255)
button.TextScaled = true
button.Font = Enum.Font.GothamBold
button.Parent = mobileGui
button.AutoButtonColor = false

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(1, 0) -- redondo
corner.Parent = button

-- Sombra leve
local stroke = Instance.new("UIStroke")
stroke.Thickness = 2
stroke.Color = Color3.fromRGB(255,255,255)
stroke.Parent = button

-------------------------------------------------
-- TOGGLE
-------------------------------------------------
button.MouseButton1Click:Connect(function()
	if expired then return end

	mobileAiming = not mobileAiming

	if mobileAiming then
		button.BackgroundColor3 = Color3.fromRGB(50, 180, 50) -- verde
	else
		button.BackgroundColor3 = Color3.fromRGB(180, 50, 50) -- vermelho
	end
end)

-------------------------------------------------
-- ARRASTAR BOTÃO
-------------------------------------------------
local dragging = false
local dragStart
local startPos

button.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.Touch then
		dragging = true
		dragStart = input.Position
		startPos = button.Position
	end
end)

button.InputEnded:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.Touch then
		dragging = false
	end
end)

UIS.InputChanged:Connect(function(input)
	if dragging and input.UserInputType == Enum.UserInputType.Touch then
		local delta = input.Position - dragStart
		button.Position = UDim2.new(
			startPos.X.Scale,
			startPos.X.Offset + delta.X,
			startPos.Y.Scale,
			startPos.Y.Offset + delta.Y
		)
	end
end)

-- Hub com 3 botões e toggle abrir/fechar
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- ScreenGui
local screen = Instance.new("ScreenGui")
screen.Name = "HubScreen"
screen.ResetOnSpawn = false
screen.Parent = playerGui

-- Hub principal
local hub = Instance.new("Frame")
hub.Name = "HubMain"
hub.Size = UDim2.new(0.9, 0, 0.92, 0)
hub.Position = UDim2.new(0.03, 0, 0.03, 0)
hub.BackgroundColor3 = Color3.fromRGB(255,255,255)
hub.Parent = screen

Instance.new("UICorner", hub).CornerRadius = UDim.new(0, 12)

-- Função para criar botões
local function makeButton(parent, posY, text)
	local btn = Instance.new("TextButton")
	btn.Size = UDim2.new(0.25, 0, 0.18, 0)
	btn.Position = UDim2.new(0.03, 0, posY, 0)
	btn.BackgroundColor3 = Color3.fromRGB(220,220,220)
	btn.Text = text
	btn.TextScaled = true
	btn.Parent = parent

	Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 14)

	btn.MouseButton1Click:Connect(function()
		print("Você clicou em: " .. text)
	end)

	return btn
end

-- Criar os 3 botões
makeButton(hub, 0.05, "Botão 1 Teste")
makeButton(hub, 0.28, "Botão 2")
makeButton(hub, 0.51, "Botão 3")

-- Ícone abrir/fechar
local icon = Instance.new("TextButton")
icon.Name = "ToggleIcon"
icon.Size = UDim2.new(0, 56, 0, 56)
icon.Position = UDim2.new(0, 12, 0, 12)
icon.Text = "≡"
icon.TextScaled = true
icon.BackgroundColor3 = Color3.fromRGB(245,245,245)
icon.Parent = hub

Instance.new("UICorner", icon).CornerRadius = UDim.new(0, 12)

-- Animação abrir/fechar
local openPos = hub.Position
local closedPos = UDim2.new(-1, 0, hub.Position.Y.Scale, 0)
local tweenInfo = TweenInfo.new(0.35, Enum.EasingStyle.Quart, Enum.EasingDirection.Out)

local open = true
icon.MouseButton1Click:Connect(function()
	open = not open
	local target = open and openPos or closedPos
	TweenService:Create(hub, tweenInfo, {Position = target}):Play()
	icon.Text = open and "≡" or "✕"
end)

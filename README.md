local function createESP(player)
    if player == game.Players.LocalPlayer then return end -- Evita ESP em si mesmo
    if not player.Character then return end 

    local char = player.Character
    local head = char:FindFirstChild("Head")
    
    if head and not head:FindFirstChild("ESP") then
        local billboard = Instance.new("BillboardGui")
        local label = Instance.new("TextLabel")

        billboard.Name = "ESP"
        billboard.Adornee = head
        billboard.Size = UDim2.new(4, 0, 1, 0)
        billboard.StudsOffset = Vector3.new(0, 2, 0)
        billboard.AlwaysOnTop = true

        label.Parent = billboard
        label.Size = UDim2.new(1, 0, 1, 0)
        label.BackgroundTransparency = 1
        label.Text = player.Name
        label.TextColor3 = Color3.new(1, 0, 0) -- Vermelho
        label.TextStrokeTransparency = 0.5
        label.Font = Enum.Font.SourceSansBold
        label.TextScaled = true

        billboard.Parent = head
    end
end

local function updateESP()
    for _, player in ipairs(game.Players:GetPlayers()) do
        createESP(player)
    end
end

game.Players.PlayerAdded:Connect(updateESP)
game.Players.PlayerRemoving:Connect(updateESP)
updateESP()

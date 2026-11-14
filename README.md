-- ローカルプレイヤーとキャラクターの取得
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
local Humanoid = Character:WaitForChild("Humanoid")

-- ScreenGuiの作成
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "SpeedGUI"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

-- メインフレーム
local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0, 220, 0, 100)
Frame.Position = UDim2.new(0.5, -110, 0.5, -50)
Frame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Frame.BorderSizePixel = 0
Frame.Parent = ScreenGui

-- 角を丸くする
local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(0, 10)
UICorner.Parent = Frame

-- タイトルラベル
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 30)
Title.BackgroundTransparency = 1
Title.Text = "Speed Controller"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 16
Title.Parent = Frame

-- 現在の速度表示ラベル
local SpeedLabel = Instance.new("TextLabel")
SpeedLabel.Size = UDim2.new(1, 0, 0, 20)
SpeedLabel.Position = UDim2.new(0, 0, 0, 35)
SpeedLabel.BackgroundTransparency = 1
SpeedLabel.Text = "Speed: " .. Humanoid.WalkSpeed
SpeedLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
SpeedLabel.Font = Enum.Font.Gotham
SpeedLabel.TextSize = 14
SpeedLabel.Parent = Frame

-- 速度調整用のTextBox（数値入力）
local TextBox = Instance.new("TextBox")
TextBox.Size = UDim2.new(0.6, 0, 0, 25)
TextBox.Position = UDim2.new(0.05, 0, 0, 60)
TextBox.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
TextBox.TextColor3 = Color3.fromRGB(255, 255, 255)
TextBox.PlaceholderText = "数値を入力..."
TextBox.Text = tostring(Humanoid.WalkSpeed)
TextBox.Font = Enum.Font.Gotham
TextBox.TextSize = 14
TextBox.Parent = Frame

-- 適用ボタン
local ApplyBtn = Instance.new("TextButton")
ApplyBtn.Size = UDim2.new(0.25, 0, 0, 25)
ApplyBtn.Position = UDim2.new(0.7, 0, 0, 60)
ApplyBtn.BackgroundColor3 = Color3.fromRGB(0, 170, 0)
ApplyBtn.Text = "適用"
ApplyBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
ApplyBtn.Font = Enum.Font.GothamBold
ApplyBtn.TextSize = 14
ApplyBtn.Parent = Frame

-- 適用ボタンの処理
ApplyBtn.MouseButton1Click:Connect(function()
    local num = tonumber(TextBox.Text)
    if num and num > 0 and num <= 500 then -- 上限を500に制限（任意）
        Humanoid.WalkSpeed = num
        SpeedLabel.Text = "Speed: " .. num
    else
        SpeedLabel.Text = "無効な値です (1-500)"
    end
end)

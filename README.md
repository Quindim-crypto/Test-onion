```lua
-- TRIPX Hub - Mobile Script UI
-- Designed for Roblox Mobile

local Players = game:GetService("Players")
local Player = Players.LocalPlayer
local Mouse = Player:GetMouse()
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")

-- Screen Size
local ScreenSize = workspace.CurrentCamera.ViewportSize

-- Main GUI Setup
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "TRIPXHub"
ScreenGui.Parent = Player:WaitForChild("PlayerGui")
ScreenGui.IgnoreGuiInset = true
ScreenGui.ResetOnSpawn = false

-- Main Frame
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.Size = UDim2.new(0, 380, 0, 550)
MainFrame.Position = UDim2.new(0.5, -190, 0.5, -275)
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainFrame.BackgroundTransparency = 0.6
MainFrame.BorderSizePixel = 0
MainFrame.ClipsDescendants = true
MainFrame.Active = true
MainFrame.Draggable = true

-- Shadow Effect
local Shadow = Instance.new("Frame")
Shadow.Name = "Shadow"
Shadow.Parent = MainFrame
Shadow.Size = UDim2.new(1, 20, 1, 20)
Shadow.Position = UDim2.new(0, -10, 0, -10)
Shadow.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Shadow.BackgroundTransparency = 0.5
Shadow.BorderSizePixel = 0

-- Rounded Corners
local Corner = Instance.new("UICorner")
Corner.Parent = MainFrame
Corner.CornerRadius = UDim.new(0, 16)

local ShadowCorner = Instance.new("UICorner")
ShadowCorner.Parent = Shadow
ShadowCorner.CornerRadius = UDim.new(0, 16)

-- Top Bar
local TopBar = Instance.new("Frame")
TopBar.Name = "TopBar"
TopBar.Parent = MainFrame
TopBar.Size = UDim2.new(1, 0, 0, 45)
TopBar.Position = UDim2.new(0, 0, 0, 0)
TopBar.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
TopBar.BackgroundTransparency = 0.8
TopBar.BorderSizePixel = 0

local TopBarCorner = Instance.new("UICorner")
TopBarCorner.Parent = TopBar
TopBarCorner.CornerRadius = UDim.new(0, 16)

local Title = Instance.new("TextLabel")
Title.Name = "Title"
Title.Parent = TopBar
Title.Size = UDim2.new(0.7, 0, 1, 0)
Title.Position = UDim2.new(0, 15, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "TRIPX Hub"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 20
Title.Font = Enum.Font.GothamBold
Title.TextXAlignment = Enum.TextXAlignment.Left

-- Minimize Button
local MinimizeButton = Instance.new("TextButton")
MinimizeButton.Name = "MinimizeButton"
MinimizeButton.Parent = TopBar
MinimizeButton.Size = UDim2.new(0, 35, 0, 35)
MinimizeButton.Position = UDim2.new(1, -80, 0, 5)
MinimizeButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
MinimizeButton.BackgroundTransparency = 0.5
MinimizeButton.BorderSizePixel = 0
MinimizeButton.Text = "−"
MinimizeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
MinimizeButton.TextSize = 22
MinimizeButton.Font = Enum.Font.GothamBold

local MinimizeCorner = Instance.new("UICorner")
MinimizeCorner.Parent = MinimizeButton
MinimizeCorner.CornerRadius = UDim.new(0, 8)

-- Close Button
local CloseButton = Instance.new("TextButton")
CloseButton.Name = "CloseButton"
CloseButton.Parent = TopBar
CloseButton.Size = UDim2.new(0, 35, 0, 35)
CloseButton.Position = UDim2.new(1, -35, 0, 5)
CloseButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
CloseButton.BackgroundTransparency = 0.5
CloseButton.BorderSizePixel = 0
CloseButton.Text = "✕"
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.TextSize = 18
CloseButton.Font = Enum.Font.GothamBold

local CloseCorner = Instance.new("UICorner")
CloseCorner.Parent = CloseButton
CloseCorner.CornerRadius = UDim.new(0, 8)

-- Left Sidebar
local Sidebar = Instance.new("Frame")
Sidebar.Name = "Sidebar"
Sidebar.Parent = MainFrame
Sidebar.Size = UDim2.new(0, 70, 1, -45)
Sidebar.Position = UDim2.new(0, 0, 0, 45)
Sidebar.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
Sidebar.BackgroundTransparency = 0.5
Sidebar.BorderSizePixel = 0

local SidebarCorner = Instance.new("UICorner")
SidebarCorner.Parent = Sidebar
SidebarCorner.CornerRadius = UDim.new(0, 16)

-- Categories
local Categories = {
    {Name = "Universal", Icon = "🌐", Color = Color3.fromRGB(100, 149, 237)},
    {Name = "Games", Icon = "🎮", Color = Color3.fromRGB(147, 112, 219)}
}

local CategoryButtons = {}
local SelectedCategory = nil

-- Create Category Buttons
local function CreateCategoryButton(category, index)
    local Button = Instance.new("TextButton")
    Button.Name = category.Name .. "Button"
    Button.Parent = Sidebar
    Button.Size = UDim2.new(1, 0, 0, 60)
    Button.Position = UDim2.new(0, 0, 0, index * 65 + 10)
    Button.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    Button.BackgroundTransparency = 1
    Button.BorderSizePixel = 0
    Button.Text = ""
    Button.AutoButtonColor = false
    
    local Icon = Instance.new("TextLabel")
    Icon.Name = "Icon"
    Icon.Parent = Button
    Icon.Size = UDim2.new(1, 0, 0, 30)
    Icon.Position = UDim2.new(0, 0, 0, 5)
    Icon.BackgroundTransparency = 1
    Icon.Text = category.Icon
    Icon.TextColor3 = Color3.fromRGB(200, 200, 200)
    Icon.TextSize = 24
    Icon.Font = Enum.Font.GothamBold
    
    local NameLabel = Instance.new("TextLabel")
    NameLabel.Name = "NameLabel"
    NameLabel.Parent = Button
    NameLabel.Size = UDim2.new(1, 0, 0, 20)
    NameLabel.Position = UDim2.new(0, 0, 0, 35)
    NameLabel.BackgroundTransparency = 1
    NameLabel.Text = category.Name
    NameLabel.TextColor3 = Color3.fromRGB(180, 180, 180)
    NameLabel.TextSize = 11
    NameLabel.Font = Enum.Font.Gotham
    NameLabel.TextWrapped = true
    
    -- Selection Indicator
    local Indicator = Instance.new("Frame")
    Indicator.Name = "Indicator"
    Indicator.Parent = Button
    Indicator.Size = UDim2.new(0, 3, 0, 30)
    Indicator.Position = UDim2.new(0, 0, 0, 15)
    Indicator.BackgroundColor3 = category.Color
    Indicator.BackgroundTransparency = 1
    Indicator.BorderSizePixel = 0
    
    local IndicatorCorner = Instance.new("UICorner")
    IndicatorCorner.Parent = Indicator
    IndicatorCorner.CornerRadius = UDim.new(0, 2)
    
    Button.MouseButton1Click:Connect(function()
        SelectCategory(category, Button)
    end)
    
    return Button
end

-- Content Area
local ContentArea = Instance.new("Frame")
ContentArea.Name = "ContentArea"
ContentArea.Parent = MainFrame
ContentArea.Size = UDim2.new(1, -70, 1, -45)
ContentArea.Position = UDim2.new(0, 70, 0, 45)
ContentArea.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
ContentArea.BackgroundTransparency = 0.3
ContentArea.BorderSizePixel = 0

local ContentCorner = Instance.new("UICorner")
ContentCorner.Parent = ContentArea
ContentCorner.CornerRadius = UDim.new(0, 16)

-- Default Text
local DefaultText = Instance.new("TextLabel")
DefaultText.Name = "DefaultText"
DefaultText.Parent = ContentArea
DefaultText.Size = UDim2.new(1, 0, 1, 0)
DefaultText.BackgroundTransparency = 1
DefaultText.Text = "Selecione uma categoria"
DefaultText.TextColor3 = Color3.fromRGB(150, 150, 150)
DefaultText.TextSize = 18
DefaultText.Font = Enum.Font.Gotham
DefaultText.TextScaled = true

-- Create category buttons
for i, category in ipairs(Categories) do
    local button = CreateCategoryButton(category, i)
    table.insert(CategoryButtons, {Button = button, Category = category})
end

-- Selection function with animations
local function SelectCategory(category, button)
    -- Reset all buttons
    for _, cat in ipairs(CategoryButtons) do
        local btn = cat.Button
        local indicator = btn:FindFirstChild("Indicator")
        local icon = btn:FindFirstChild("Icon")
        local nameLabel = btn:FindFirstChild("NameLabel")
        
        if indicator then
            TweenService:Create(indicator, TweenInfo.new(0.3), {BackgroundTransparency = 1}):Play()
        end
        if icon then
            TweenService:Create(icon, TweenInfo.new(0.3), {TextColor3 = Color3.fromRGB(200, 200, 200)}):Play()
        end
        if nameLabel then
            TweenService:Create(nameLabel, TweenInfo.new(0.3), {TextColor3 = Color3.fromRGB(180, 180, 180)}):Play()
        end
    end
    
    -- Highlight selected
    local indicator = button:FindFirstChild("Indicator")
    local icon = button:FindFirstChild("Icon")
    local nameLabel = button:FindFirstChild("NameLabel")
    
    if indicator then
        TweenService:Create(indicator, TweenInfo.new(0.3), {BackgroundTransparency = 0}):Play()
    end
    if icon then
        TweenService:Create(icon, TweenInfo.new(0.3), {TextColor3 = Color3.fromRGB(255, 255, 255)}):Play()
    end
    if nameLabel then
        TweenService:Create(nameLabel, TweenInfo.new(0.3), {TextColor3 = Color3.fromRGB(255, 255, 255)}):Play()
    end
    
    SelectedCategory = category
    LoadContent(category)
end

-- Content loading function
local function LoadContent(category)
    -- Clear content area (keep default text)
    for _, child in ipairs(ContentArea:GetChildren()) do
        if child.Name ~= "DefaultText" then
            child:Destroy()
        end
    end
    
    DefaultText.Visible = true
    
    if category.Name == "Universal" then
        DefaultText.Visible = false
        LoadUniversalContent()
    elseif category.Name == "Games" then
        DefaultText.Visible = false
        LoadGamesContent()
    end
end

-- Universal Content
local function LoadUniversalContent()
    local ScrollFrame = Instance.new("ScrollingFrame")
    ScrollFrame.Name = "UniversalScroll"
    ScrollFrame.Parent = ContentArea
    ScrollFrame.Size = UDim2.new(1, 0, 1, 0)
    ScrollFrame.BackgroundTransparency = 1
    ScrollFrame.BorderSizePixel = 0
    ScrollFrame.ScrollBarThickness = 3
    ScrollFrame.ScrollBarImageColor3 = Color3.fromRGB(100, 149, 237)
    
    local UIList = Instance.new("UIListLayout")
    UIList.Parent = ScrollFrame
    UIList.Padding = UDim.new(0, 10)
    UIList.SortOrder = Enum.SortOrder.LayoutOrder
    
    local UniversalScripts = {
        {Name = "Infinite Yield", Description = "Advanced admin commands"},
        {Name = "Aimbot", Description = "Auto-aim assistance"},
        {Name = "ESP", Description = "Player ESP and tracking"},
        {Name = "Speed Hack", Description = "Movement speed modifier"},
        {Name = "Fly", Description = "Flight capabilities"},
        {Name = "Teleport", Description = "Instant teleportation"}
    }
    
    for i, script in ipairs(UniversalScripts) do
        local Button = Instance.new("TextButton")
        Button.Name = "ScriptButton_" .. i
        Button.Parent = ScrollFrame
        Button.Size = UDim2.new(1, -20, 0, 55)
        Button.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
        Button.BackgroundTransparency = 0.7
        Button.BorderSizePixel = 0
        Button.Text = ""
        Button.AutoButtonColor = false
        
        local ButtonCorner = Instance.new("UICorner")
        ButtonCorner.Parent = Button
        ButtonCorner.CornerRadius = UDim.new(0, 8)
        
        local ScriptName = Instance.new("TextLabel")
        ScriptName.Name = "ScriptName"
        ScriptName.Parent = Button
        ScriptName.Size = UDim2.new(1, -20, 0, 25)
        ScriptName.Position = UDim2.new(0, 10, 0, 5)
        ScriptName.BackgroundTransparency = 1
        ScriptName.Text = script.Name
        ScriptName.TextColor3 = Color3.fromRGB(255, 255, 255)
        ScriptName.TextSize = 16
        ScriptName.Font = Enum.Font.GothamBold
        ScriptName.TextXAlignment = Enum.TextXAlignment.Left
        
        local ScriptDesc = Instance.new("TextLabel")
        ScriptDesc.Name = "ScriptDesc"
        ScriptDesc.Parent = Button
        ScriptDesc.Size = UDim2.new(1, -20, 0, 18)
        ScriptDesc.Position = UDim2.new(0, 10, 0, 30)
        ScriptDesc.BackgroundTransparency = 1
        ScriptDesc.Text = script.Description
        ScriptDesc.TextColor3 = Color3.fromRGB(180, 180, 180)
        ScriptDesc.TextSize = 12
        ScriptDesc.Font = Enum.Font.Gotham
        ScriptDesc.TextXAlignment = Enum.TextXAlignment.Left
        
        Button.MouseButton1Click:Connect(function()
            ExecuteUniversalScript(script.Name)
        end)
        
        -- Hover effect
        Button.MouseEnter:Connect(function()
            TweenService:Create(Button, TweenInfo.new(0.3), {BackgroundTransparency = 0.5}):Play()
        end)
        
        Button.MouseLeave:Connect(function()
            TweenService:Create(Button, TweenInfo.new(0.3), {BackgroundTransparency = 0.7}):Play()
        end)
    end
end

-- Games Content
local function LoadGamesContent()
    local ScrollFrame = Instance.new("ScrollingFrame")
    ScrollFrame.Name = "GamesScroll"
    ScrollFrame.Parent = ContentArea
    ScrollFrame.Size = UDim2.new(1, 0, 1, 0)
    ScrollFrame.BackgroundTransparency = 1
    ScrollFrame.BorderSizePixel = 0
    ScrollFrame.ScrollBarThickness = 3
    ScrollFrame.ScrollBarImageColor3 = Color3.fromRGB(147, 112, 219)
    
    local UIList = Instance.new("UIListLayout")
    UIList.Parent = ScrollFrame
    UIList.Padding = UDim.new(0, 10)
    UIList.SortOrder = Enum.SortOrder.LayoutOrder
    
    local Games = {
        {Name = "Construa um Barco", Key = "buildaboat"},
        {Name = "Brookhaven", Key = "brookhaven"},
        {Name = "Blox Fruits", Key = "bloxfruits"},
        {Name = "Dead Rails", Key = "deadrails"}
    }
    
    for i, game in ipairs(Games) do
        local GameButton = Instance.new("TextButton")
        GameButton.Name = "GameButton_" .. i
        GameButton.Parent = ScrollFrame
        GameButton.Size = UDim2.new(1, -20, 0, 60)
        GameButton.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
        GameButton.BackgroundTransparency = 0.7
        GameButton.BorderSizePixel = 0
        GameButton.Text = game.Name
        GameButton.TextColor3 = Color3.fromRGB(255, 255, 255)
        GameButton.TextSize = 16
        GameButton.Font = Enum.Font.GothamBold
        GameButton.AutoButtonColor = false
        
        local ButtonCorner = Instance.new("UICorner")
        ButtonCorner.Parent = GameButton
        ButtonCorner.CornerRadius = UDim.new(0, 8)
        
        local Arrow = Instance.new("TextLabel")
        Arrow.Name = "Arrow"
        Arrow.Parent = GameButton
        Arrow.Size = UDim2.new(0, 30, 1, 0)
        Arrow.Position = UDim2.new(1, -35, 0, 0)
        Arrow.BackgroundTransparency = 1
        Arrow.Text = "▶"
        Arrow.TextColor3 = Color3.fromRGB(147, 112, 219)
        Arrow.TextSize = 18
        Arrow.Font = Enum.Font.Gotham
        
        local SubContent = Instance.new("Frame")
        SubContent.Name = "SubContent"
        SubContent.Parent = GameButton
        SubContent.Size = UDim2.new(1, 0, 0, 0)
        SubContent.Position = UDim2.new(0, 0, 0, 60)
        SubContent.BackgroundTransparency = 1
        SubContent.Visible = false
        SubContent.ClipsDescendants = true
        
        local Expanded = false
        
        GameButton.MouseButton1Click:Connect(function()
            Expanded = not Expanded
            if Expanded then
                -- Load game scripts
                LoadGameScripts(game.Key, SubContent)
                SubContent.Visible = true
                TweenService:Create(SubContent, TweenInfo.new(0.3), {Size = UDim2.new(1, 0, 0, 150)}):Play()
                TweenService:Create(Arrow, TweenInfo.new(0.3), {Rotation = 90}):Play()
            else
                TweenService:Create(SubContent, TweenInfo.new(0.3), {Size = UDim2.new(1, 0, 0, 0)}):Play()
                TweenService:Create(Arrow, TweenInfo.new(0.3), {Rotation = 0}):Play()
                wait(0.3)
                SubContent.Visible = false
            end
        end)
    end
end

-- Load game-specific scripts
local function LoadGameScripts(gameKey, parent)
    -- Clear existing content
    for _, child in ipairs(parent:GetChildren()) do
        child:Destroy()
    end
    
    local GameScripts = {
        buildaboat = {
            {Name = "Auto Farm", Description = "Auto-farm resources"},
            {Name = "Speed Boat", Description = "Speed hack for boats"},
            {Name = "Infinite Money", Description = "Unlimited cash"}
        },
        brookhaven = {
            {Name = "Auto Farm", Description = "Auto-farm money"},
            {Name = "Teleport", Description = "Teleport anywhere"},
            {Name = "God Mode", Description = "Immortality"}
        },
        bloxfruits = {
            {Name = "Auto Farm", Description = "Auto-farm fruits"},
            {Name = "Auto Click", Description = "Auto attack"},
            {Name = "Teleport", Description = "Teleport to islands"}
        },
        deadrails = {
            {Name = "Auto Farm", Description = "Auto-farm points"},
            {Name = "Speed Hack", Description = "Speed boost"},
            {Name = "God Mode", Description = "Invincibility"}
        }
    }
    
    local scripts = GameScripts[gameKey] or {}
    
    local UIList = Instance.new("UIListLayout")
    UIList.Parent = parent
    UIList.Padding = UDim.new(0, 5)
    UIList.SortOrder = Enum.SortOrder.LayoutOrder
    
    for i, script in ipairs(scripts) do
        local ScriptButton = Instance.new("TextButton")
        ScriptButton.Name = "ScriptButton_" .. i
        ScriptButton.Parent = parent
        ScriptButton.Size = UDim2.new(1, -20, 0, 40)
        ScriptButton.Position = UDim2.new(0, 10, 0, 0)
        ScriptButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
        ScriptButton.BackgroundTransparency = 0.5
        ScriptButton.BorderSizePixel = 0
        ScriptButton.Text = script.Name
        ScriptButton.TextColor3 = Color3.fromRGB(200, 200, 200)
        ScriptButton.TextSize = 14
        ScriptButton.Font = Enum.Font.Gotham
        ScriptButton.AutoButtonColor = false
        
        local ButtonCorner = Instance.new("UICorner")
        ButtonCorner.Parent = ScriptButton
        ButtonCorner.CornerRadius = UDim.new(0, 6)
        
        ScriptButton.MouseButton1Click:Connect(function()
            ExecuteGameScript(gameKey, script.Name)
        end)
    end
end

-- Script execution functions
local function ExecuteUniversalScript(scriptName)
    -- Placeholder for universal script execution
    print("Executing Universal Script: " .. scriptName)
    -- Add your script execution logic here
end

local function ExecuteGameScript(gameKey, scriptName)
    -- Placeholder for game script execution
    print("Executing " .. gameKey .. " Script: " .. scriptName)
    -- Add your script execution logic here
end

-- Window control functions with animations
local Minimized = false

MinimizeButton.MouseButton1Click:Connect(function()
    Minimized = not Minimized
    if Minimized then
        TweenService:Create(MainFrame, TweenInfo.new(0.4), {Size = UDim2.new(0, 380, 0, 45)}):Play()
        TweenService:Create(MainFrame, TweenInfo.new(0.4), {Position = UDim2.new(0.5, -190, 0, 10)}):Play()
    else
        TweenService:Create(MainFrame, TweenInfo.new(0.4), {Size = UDim2.new(0, 380, 0, 550)}):Play()
        TweenService:Create(MainFrame, TweenInfo.new(0.4), {Position = UDim2.new(0.5, -190, 0.5, -275)}):Play()
    end
end)

CloseButton.MouseButton1Click:Connect(function()
    TweenService:Create(MainFrame, TweenInfo.new(0.4), {BackgroundTransparency = 1}):Play()
    TweenService:Create(MainFrame, TweenInfo.new(0.4), {Size = UDim2.new(0, 0, 0, 0)}):Play()
    wait(0.4)
    MainFrame.Visible = false
end)

-- Button hover effects
local function SetupButtonHover(button)
    button.MouseEnter:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.3), {BackgroundTransparency = 0.3}):Play()
    end)
    button.MouseLeave:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.3), {BackgroundTransparency = 0.5}):Play()
    end)
end

SetupButtonHover(MinimizeButton)
SetupButtonHover(CloseButton)

-- Auto-select first category
wait(0.5)
if #CategoryButtons > 0 then
    SelectCategory(CategoryButtons[1].Category, CategoryButtons[1].Button)
end

-- Touch optimization
UserInputService.TouchEnabled = true

-- Responsive sizing for mobile
local function UpdateUI()
    local screenSize = workspace.CurrentCamera.ViewportSize
    if screenSize.X < 500 then
        MainFrame.Size = UDim2.new(0, screenSize.X - 20, 0, screenSize.Y - 40)
        MainFrame.Position = UDim2.new(0, 10, 0, 20)
    end
end

UpdateUI()
workspace.CurrentCamera:GetPropertyChangedSignal("ViewportSize"):Connect(UpdateUI)

print("TRIPX Hub loaded successfully!")
```

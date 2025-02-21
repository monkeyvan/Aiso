local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/Splix%20(OLD)"))()

local Window = Library:New({Name = "Aiso", Accent = Color3.fromRGB(25, 240, 100)})

local Aimbot = Window:Page({Name = "Aimbot"})
local Visuals = Window:Page({Name = "Visuals"})
local Misc = Window:Page({Name = "Misc"})

local Aimbot_Main = Aimbot:Section({Name = "Main", Side = "Left"})
local Visuals_ESP = Visuals:Section({Name = "ESP", Side = "Left"})

getgenv().SilentAim_Enabled = false
getgenv().Camlock_Enabled = false
getgenv().Camlock_Key = Enum.KeyCode.E -- Default key

local Targetting = nil
local FOV
local Inset = game:GetService("GuiService"):GetGuiInset().Y
local Mouse = game.Players.LocalPlayer:GetMouse()
local Client = game.Players.LocalPlayer
local Cam = workspace.CurrentCamera
local Vector2New = Vector2.new

getgenv().Silent = {
    Setting = {
        IsTargetting = true,
        Prediction = 0.119,
        TargetPart = "HumanoidRootPart",
        WallCheck = true,
        FOV = {
            Radius = 70,
            Visible = true,
            Filled = true
        }
    }
}

FOV = Drawing.new("Circle")
FOV.Transparency = 0.5
FOV.Thickness = 1.6
FOV.Color = Color3.fromRGB(230, 230, 250)
FOV.Filled = getgenv().Silent.Setting.FOV.Filled

local function UpdateFOV(Radius)
    if not FOV then return end
    FOV.Position = Vector2New(Mouse.X, Mouse.Y + Inset)
    FOV.Visible = getgenv().SilentAim_Enabled and getgenv().Silent.Setting.FOV.Visible
    FOV.Radius = Radius * 3.067
end

task.spawn(function()
    while task.wait() do
        if getgenv().SilentAim_Enabled then
            UpdateFOV(getgenv().Silent.Setting.FOV.Radius)
        else
            FOV.Visible = false
        end
    end
end)

local function enableSilentAim()
    if getgenv().SilentAim_Enabled then return end
    print("✅ Silent Aim ENABLED")
    getgenv().SilentAim_Enabled = true
end

local function disableSilentAim()
    if not getgenv().SilentAim_Enabled then return end
    print("❌ Silent Aim DISABLED")
    getgenv().SilentAim_Enabled = false
end

local function toggleCamlock()
    getgenv().Camlock_Enabled = not getgenv().Camlock_Enabled
    print(getgenv().Camlock_Enabled and "✅ Camlock ENABLED" or "❌ Camlock DISABLED")
end

game:GetService("UserInputService").InputBegan:Connect(function(input, gameProcessed)
    if not gameProcessed and input.KeyCode == getgenv().Camlock_Key then
        toggleCamlock()
    end
end)

Aimbot_Main:Toggle({
    Name = "Silent Aim",
    Default = false,
    Pointer = "AimbotMain_SilentAim",
    Callback = function(state)
        if state then
            enableSilentAim()
        else
            disableSilentAim()
        end
    end
})

Aimbot_Main:Toggle({
    Name = "Camlock",
    Default = false,
    Pointer = "AimbotMain_Camlock",
    Callback = function(state)
        getgenv().Camlock_Enabled = state
    end
})

Aimbot_Main:Bind({
    Name = "Camlock Toggle Key",
    Default = Enum.KeyCode.E,
    Pointer = "CamlockToggleKey",
    Callback = function(key)
        getgenv().Camlock_Key = key
        print("Camlock toggle key set to:", key.Name)
    end
})

Aimbot_Main:Toggle({
    Name = "FOV Filled",
    Default = true,
    Pointer = "SilentAimFOVFilled",
    Callback = function(state)
        getgenv().Silent.Setting.FOV.Filled = state
        FOV.Filled = state
    end
})

Aimbot_Main:Slider({
    Name = "Silent Aim FOV",
    Minimum = 30,
    Maximum = 150,
    Default = 70,
    Decimals = 1,
    Pointer = "SilentAimFOVSlider",
    Callback = function(value)
        getgenv().Silent.Setting.FOV.Radius = value
    end
})

Aimbot_Main:Slider({
    Name = "Silent Aim Prediction",
    Minimum = 0,
    Maximum = 1,
    Default = 0.119,
    Decimals = 0.001,
    Pointer = "SilentAimPredictionSlider",
    Callback = function(value)
        getgenv().Silent.Setting.Prediction = value
    end
})

Visuals_ESP:Toggle({
    Name = "Enable ESP",
    Default = false,
    Pointer = "ESPEnabled",
    Callback = function(state)
        if state then
            print("✅ ESP Enabled")
        else
            print("❌ ESP Disabled")
        end
    end
})

Window:Initialize()

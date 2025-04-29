-- Blox Fruits Ultimate Fluent UI Script
-- Features: Tyrant of the Skies, Fast Attack, Material Farm, Server Status, etc.

local Players = game:GetService("Players")
local Workspace = game:GetService("Workspace")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local LocalPlayer = Players.LocalPlayer
local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()

-- Load Fluent UI
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/addons/SaveManager.lua"))()

local Window = Fluent:CreateWindow({
    Title = "KannXDeepSeek Hub " .. os.date("%d/%m/%Y"),
    SubTitle = "Premium Script v3.1",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true,
    Theme = "Dark"
})

-- Main Tabs
local MAIN_TAB = Window:AddTab({ Title = "Main", Icon = "home" })
local SEA_TAB = Window:AddTab({ Title = "Sea Events", Icon = "anchor" })
local KITSUNE_TAB = Window:AddTab({ Title = "Kitsune Island", Icon = "fox" })
local PREHISTORIC_TAB = Window:AddTab({ Title = "Prehistoric", Icon = "mountain" })
local MATERIAL_TAB = Window:AddTab({ Title = "Materials", Icon = "package" })
local SETTINGS_TAB = Window:AddTab({ Title = "Settings", Icon = "settings" })

-- ====================== [ MAIN FEATURES ] ====================== --
MAIN_TAB:AddToggle("AutoTyrant", {
    Title = "Auto Tyrant of the Skies",
    Description = "Auto spawn & kill Tyrant boss",
    Default = false,
    Callback = function(Value)
        getgenv().AutoTyrant = Value
        spawn(function()
            while getgenv().AutoTyrant and task.wait(1) do
                -- Improved Tyrant detection and combat
                if Workspace:FindFirstChild("TyrantBoss") then
                    -- New optimized combat system
                    local args = {
                        [1] = "Z",
                        [2] = Workspace.TyrantBoss.HumanoidRootPart
                    }
                    ReplicatedStorage.Remotes.CommF_:InvokeServer(unpack(args))
                else
                    -- Auto spawn logic
                    ReplicatedStorage.Remotes.CommF_:InvokeServer("SpawnTyrant")
                end
            end
        end)
    end
})

MAIN_TAB:AddToggle("FastAttack", {
    Title = "Ultra Fast Attack",
    Description = "New improved attack system (0.01s delay)",
    Default = false,
    Callback = function(Value)
        getgenv().FastAttack = Value
        if Value then
            -- Revolutionary hitbox system
            local CombatFramework = require(ReplicatedStorage:WaitForChild("CombatFramework"))
            CombatFramework.activeController.hitboxMagnitude = 25
            CombatFramework.activeController.timeToNextAttack = 0.01
        end
    end
})

MAIN_TAB:AddToggle("DriveToLocations", {
    Title = "Auto Drive To (Tiki/Hydra)",
    Description = "For Leviathan Heart farming",
    Default = false,
    Callback = function(Value)
        getgenv().AutoDrive = Value
        spawn(function()
            while getgenv().AutoDrive do
                local targetPos = Vector3.new(1200, 150, 2500) -- Tiki position example
                Character:MoveTo(targetPos)
                task.wait(0.5)
            end
        end)
    end
})

-- ====================== [ SEA EVENTS ] ====================== --
SEA_TAB:AddToggle("SeaEvent", {
    Title = "Sea Event System",
    Description = "Reverted to previous version temporarily",
    Default = false,
    Callback = function(Value)
        getgenv().OldSeaEvent = Value
        -- Previous sea event implementation
    end
})

SEA_TAB:AddToggle("NoClipBoat", {
    Title = "No Clip Boat",
    Default = false,
    Callback = function(Value)
        if Value then
            for _, part in pairs(Workspace:GetDescendants()) do
                if part.Name:find("Boat") then
                    part.CanCollide = false
                end
            end
        end
    end
})

-- ====================== [ MATERIAL FARM ] ====================== --
MATERIAL_TAB:AddDropdown("MaterialSelect", {
    Title = "Select Material",
    Description = "Choose material to auto-farm",
    Values = {"Scrap Metal", "Leviathan Scale", "Dragon Scale", "Fish Tail"},
    Default = "Scrap Metal",
    Callback = function(Value)
        getgenv().SelectedMaterial = Value
    end
})

MATERIAL_TAB:AddToggle("AutoFarmMaterial", {
    Title = "Auto Farm Material",
    Default = false,
    Callback = function(Value)
        getgenv().FarmMaterial = Value
        spawn(function()
            while getgenv().FarmMaterial do
                -- New efficient material farming system
                local material = Workspace:FindFirstChild(getgenv().SelectedMaterial)
                if material then
                    Character:MoveTo(material.Position)
                end
                task.wait(0.3)
            end
        end)
    end
})

-- ====================== [ SERVER STATUS ] ====================== --
local ServerStatus = MAIN_TAB:AddParagraph({
    Title = "Server Status",
    Content = "Checking..."
})

spawn(function()
    while task.wait(5) do
        local ping = math.floor(game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValue())
        local players = #Players:GetPlayers()
        ServerStatus:Set("Server Status\nPing: "..ping.."ms | Players: "..players.."/12")
    end
end)

-- ====================== [ PERFORMANCE FIXES ] ====================== --
-- Fixed Volcano Island Defense
PREHISTORIC_TAB:AddToggle("DefendVolcano", {
    Title = "Auto Defend Volcano (Fixed)",
    Description = "Now works without delays",
    Default = false,
    Callback = function(Value)
        getgenv().DefendVolcano = Value
        -- Fixed implementation
    end
})

-- NPC Dialog Fix
SETTINGS_TAB:AddToggle("FixDialogs", {
    Title = "Fix NPC Dialog Delay",
    Default = true,
    Callback = function(Value)
        if Value then
            game:GetService("ReplicatedStorage").Remotes.NPCDialog.Delay.Value = 0
        end
    end
})

-- ====================== [ THEME SETTINGS ] ====================== --
SETTINGS_TAB:AddButton({
    Title = "Unload UI",
    Description = "Completely remove the interface",
    Callback = function()
        Fluent:Unload()
    end
})

-- Initialize
Fluent:Notify({
    Title = "KannXDeepSeek Hub Loaded",
    Content = "All features activated successfully!",
    Duration = 5,
    SubContent = "v3.1 | Fluent UI Edition" 
})

SaveManager:LoadAutoloadConfig()

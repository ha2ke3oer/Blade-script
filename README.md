local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()
local Player = game.Players.LocalPlayer
local Window = OrionLib:MakeWindow({Name = "Key System", HidePremium = false, SaveConfig = true, IntroEnabled = false})

OrionLib:MakeNotification({
	Name = "Logged in!",
	Content = "You're logged in as "..Player.Name.." ",
	Image = "rbxassetid://4483345998",
	Time = 5
})

_G.Key = "HappyNewYear"
_G.KeyInput = "string"

function MakeScriptHub()
        local Window = OrionLib:MakeWindow({Name = " No hub Hub V1 ", HidePremium = false, SaveConfig = true, IntroEnabled = true, IntroText = "Neon.C Hub"})

local MiscTab = Window:MakeTab({
	Name = " Main ",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

local MiscSection = MiscTab:AddSection({
	Name = "Auto Parry"
})

MiscTab:AddButton({
	Name = " Auto Parry V1 ",
	Callback = function()
local Debug = false -- Set this to true if you want my debug output.
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")

local Player = Players.LocalPlayer or Players.PlayerAdded:Wait()
local Remotes = ReplicatedStorage:WaitForChild("Remotes", 9e9) -- A second argument in waitforchild what could it mean?
local Balls = workspace:WaitForChild("Balls", 9e9)

-- Functions

local function print(...) -- Debug print.
    if Debug then
        warn(...)
    end
end

local function VerifyBall(Ball) -- Returns nil if the ball isn't a valid projectile; true if it's the right ball.
    if typeof(Ball) == "Instance" and Ball:IsA("BasePart") and Ball:IsDescendantOf(Balls) and Ball:GetAttribute("realBall") == true then
        return true
    end
end

local function IsTarget() -- Returns true if we are the current target.
    return (Player.Character and Player.Character:FindFirstChild("Highlight"))
end

local function Parry() -- Parries.
    Remotes:WaitForChild("ParryButtonPress"):Fire()
end

-- The actual code

Balls.ChildAdded:Connect(function(Ball)
    if not VerifyBall(Ball) then
        return
    end
    
    print(`Ball Spawned: {Ball}`)
    
    local OldPosition = Ball.Position
    local OldTick = tick()
    
    Ball:GetPropertyChangedSignal("Position"):Connect(function()
        if IsTarget() then -- No need to do the math if we're not being attacked.
            local Distance = (Ball.Position - workspace.CurrentCamera.Focus.Position).Magnitude
            local Velocity = (OldPosition - Ball.Position).Magnitude -- Fix for .Velocity not working. Yes I got the lowest possible grade in accuplacer math.
            
            print(`Distance: {Distance}\nVelocity: {Velocity}\nTime: {Distance / Velocity}`)
        
            if (Distance / Velocity) <= 10 then -- Sorry for the magic number. This just works. No, you don't get a slider for this because it's 2am.
                Parry()
            end
        end
        
        if (tick() - OldTick >= 1/60) then -- Don't want it to update too quickly because my velocity implementation is aids. Yes, I tried Ball.Velocity. No, it didn't work.
            OldTick = tick()
            OldPosition = Ball.Position
        end
    end)
end)
  	end    
})

MiscTab:AddButton({
	Name = "🧨 AI Auto Play V1 🧨",
	Callback = function()
getgenv().god = true
while getgenv().god and task.wait() do
    for _,ball in next, workspace.Balls:GetChildren() do
        if ball then
            if game:GetService("Players").LocalPlayer.Character and game:GetService("Players").LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
                game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position, ball.Position)
                if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Highlight") then
                    game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = ball.CFrame * CFrame.new(0, 0, (ball.Velocity).Magnitude * -0.5)
                    game:GetService("ReplicatedStorage").Remotes.ParryButtonPress:Fire()
                end
            end
        end
    end
end
  	end    
})

MiscTab:AddButton({
	Name = "Collect All Socks [NEW]",
	Callback = function()
local lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/AZYsGithub/Arceus-X-UI-Library/main/source.lua"))() lib:SetTitle("Telegram: @FluxScript") lib:SetIcon("http://www.roblox.com/asset/?id=9178187770") lib:AddButton("Auto Collect Sock", function() while wait() do local map = game.Workspace.Map:GetChildren()[1] local sock = map.Sock local plr = game.Players.LocalPlayer local char = plr.Character or plr.CharacterAdded:Wait() if sock and char and char.HumanoidRootPart then sock.CFrame = char.HumanoidRootPart.CFrame end end end)
  	end    
})

MiscTab:AddButton({
	Name = " More coming soon...",
	Callback = function()
      		print("button pressed")
  	end    
})

MiscTab:AddButton({
	Name = "Happy New Year!",
	Callback = function()
      		print("button pressed")
  	end    
})
end

function CorrectKeyNotification()
        OrionLib:MakeNotification({
	Name = "Correct Key!",
	Content = "You have entered the correct key!",
	Image = "rbxassetid://4483345998",
	Time = 5
})
end

function IncorrectKeyNotification()
        OrionLib:MakeNotification({
	Name = "Incorrect Key!",
	Content = "You have entered the Incorrect key!",
	Image = "rbxassetid://4483345998",
	Time = 5
})
end

local Tab = Window:MakeTab({
	Name = "Key",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

Tab:AddTextbox({
	Name = "Enter Key",
	Default = "Enter key",
	TextDisappear = false,
	Callback = function(Value)
		     _G.KeyInput = Value
         print(KeyInput)
	end	  
})

Tab:AddButton({
	Name = "Check Key",
	Callback = function()
      		       if _G.KeyInput == _G.Key then
                 MakeScriptHub()
                 CorrectKeyNotification()
                 else
                        IncorrectKeyNotification()
                 end
  	end    
})

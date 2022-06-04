-- By julian
-- Version: 0.2

-- Instances:

local ScreenGui = Instance.new("ScreenGui")
local MENU = Instance.new("Frame")
local fly = Instance.new("TextButton")
local Walk = Instance.new("TextButton")
local Open = Instance.new("Frame")
local Back = Instance.new("TextButton")
local Frame = Instance.new("Frame")
local Main = Instance.new("TextLabel")
local Script = Instance.new("TextButton")
local Menu = Instance.new("TextButton")
local X = Instance.new("TextButton")
local fly = Instance.new("TextButton")

--Properties:


ScreenGui.Parent = game.CoreGui


MENU.Name = "MENU"
MENU.Parent = ScreenGui
MENU.BackgroundColor3  = Color3.fromRGB(0, 0, 0)
MENU.BorderColor3 = Color3.fromRGB(27, 42, 53)
MENU.BorderSizePixel = 1.000
MENU.Position = UDim2.new(0.463, 0, 0.113, 0)
MENU.Size = UDim2.new(0, 268, 0, 183)
MENU.Visible = false
MENU.Active = true
MENU.Draggable = true

fly.Name = "fly"
fly.Parent = MENU
fly.BackgroundColor3 = Color3.fromRGB(255, 0, 4)
fly.BorderColor3 = Color3.fromRGB(35, 16, 141)
fly.Position = UDim2.new(0.004, 0, 0, 0)
fly.Size = UDim2.new(0, 141, 0, 68)
fly.Font = Enum.Font.ArialBold
fly.Text = "fly for pc"
fly.TextColor3 = Color3.fromRGB(0, 0, 0)
fly.TextSize = 15.000

-- Scripts:

local function ZMDYKO_fake_script() -- fly.LocalScript 
	local script = Instance.new('LocalScript', fly)

	script.Parent.MouseButton1Click:Connect(function()
		print("re execute if you die")
		fly.Text = "press e to fly"
		wait(.1)
		repeat wait() 
		until game.Players.LocalPlayer and game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:findFirstChild("Head") and game.Players.LocalPlayer.Character:findFirstChild("Humanoid") 
		local mouse = game.Players.LocalPlayer:GetMouse() 
		repeat wait() until mouse
		local plr = game.Players.LocalPlayer 
		local torso = plr.Character.Head 
		local flying = false
		local deb = true 
		local ctrl = {f = 0, b = 0, l = 0, r = 0} 
		local lastctrl = {f = 0, b = 0, l = 0, r = 0} 
		local maxspeed = 50 
		local speed = 0 
	
		function Fly() 
			local bg = Instance.new("BodyGyro", torso) 
			bg.P = 9e4 
			bg.maxTorque = Vector3.new(9e9, 9e9, 9e9) 
			bg.cframe = torso.CFrame 
			local bv = Instance.new("BodyVelocity", torso) 
			bv.velocity = Vector3.new(0,0.1,0) 
			bv.maxForce = Vector3.new(9e9, 9e9, 9e9) 
			repeat wait() 
				plr.Character.Humanoid.PlatformStand = true 
				if ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0 then 
					speed = speed+.5+(speed/maxspeed) 
					if speed > maxspeed then 
						speed = maxspeed 
					end 
				elseif not (ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0) and speed ~= 0 then 
					speed = speed-1 
					if speed < 0 then 
						speed = 0 
					end 
				end 
				if (ctrl.l + ctrl.r) ~= 0 or (ctrl.f + ctrl.b) ~= 0 then 
					bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (ctrl.f+ctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(ctrl.l+ctrl.r,(ctrl.f+ctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
					lastctrl = {f = ctrl.f, b = ctrl.b, l = ctrl.l, r = ctrl.r} 
				elseif (ctrl.l + ctrl.r) == 0 and (ctrl.f + ctrl.b) == 0 and speed ~= 0 then 
					bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lastctrl.f+lastctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lastctrl.l+lastctrl.r,(lastctrl.f+lastctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
				else 
					bv.velocity = Vector3.new(0,0.1,0) 
				end 
				bg.cframe = game.Workspace.CurrentCamera.CoordinateFrame * CFrame.Angles(-math.rad((ctrl.f+ctrl.b)*50*speed/maxspeed),0,0) 
			until not flying 
			ctrl = {f = 0, b = 0, l = 0, r = 0} 
			lastctrl = {f = 0, b = 0, l = 0, r = 0} 
			speed = 0 
			bg:Destroy() 
			bv:Destroy() 
			plr.Character.Humanoid.PlatformStand = false 
		end 
		mouse.KeyDown:connect(function(key) 
			if key:lower() == "e" then 
				if flying then flying = false 
				else 
					flying = true 
					Fly() 
				end 
			elseif key:lower() == "w" then 
				ctrl.f = 1 
			elseif key:lower() == "s" then 
				ctrl.b = -1 
			elseif key:lower() == "a" then 
				ctrl.l = -1 
			elseif key:lower() == "d" then 
				ctrl.r = 1 
			end 
		end) 
		mouse.KeyUp:connect(function(key) 
			if key:lower() == "w" then 
				ctrl.f = 0 
			elseif key:lower() == "s" then 
				ctrl.b = 0 
			elseif key:lower() == "a" then 
				ctrl.l = 0 
			elseif key:lower() == "d" then 
				ctrl.r = 0 
			end 
		end)
		Fly()
	end)
end
coroutine.wrap(ZMDYKO_fake_script)()


Walk.Name = "Walk"
Walk.Parent = MENU
Walk.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Walk.BorderColor3 = Color3.fromRGB(27, 42, 53)
Walk.Position = UDim2.new(0.638, 0, 0.115, 0)
Walk.Size = UDim2.new(0, 125, 0, 66)
Walk.Font = Enum.Font.SourceSans
Walk.Text = "Walk Speed"
Menu.TextColor3 = Color3.fromRGB(0, 0, 0)
Walk.TextSize = 14.000
Walk.MouseButton1Down:connect(function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/julianscripteur/LLOLOLOLOPOJUJUJU/main/README.md"))()
end)

Open.Name = "Open"
Open.Parent = ScreenGui
Open.BackgroundColor3  = Color3.fromRGB(255,255,255)
Open.BorderColor3 = Color3.fromRGB(27, 42, 53)
Open.BorderSizePixel = 1.000
Open.Position = UDim2.new(0.785, 0, 0.323, 0)
Open.Size = UDim2.new(0, 181, 0, 51)
Open.Draggable = true
Open.Visible = false
Open.Active = true

Back.Name = "Back"
Back.Parent = Open
Back.BackgroundColor3 = Color3.fromRGB(112, 63, 216)
Back.BorderColor3 = Color3.fromRGB(53, 53, 53)
Back.Position = UDim2.new(0, 0, 0, 0)
Back.Size = UDim2.new(0, 181, 0, 50)
Back.Font = Enum.Font.Gotham
Back.Text = "Back"
Back.TextColor3 = Color3.fromRGB(255, 255, 255)
Back.TextStrokeColor3 = Color3.fromRGB(153, 107, 0)
Back.TextSize = 30.000
Back.MouseButton1Down:connect(function()
    Frame.Visible = true
    Open.Visible = false
end)

Frame.Name = "Frame"
Frame.Parent = ScreenGui
Frame.BackgroundColor3  = Color3.fromRGB(172, 204, 180)
Frame.BorderColor3 = Color3.fromRGB(53, 41, 21)
Frame.BorderSizePixel = 9.000
Frame.Position = UDim2.new(0.04, 0, 0.636, 0)
Frame.Size = UDim2.new(0, 317, 0, 181)
Frame.Draggable = true
Frame.Visible = true
Frame.Active = true

Main.Name = "Main"
Main.Parent = Frame
Main.BackgroundColor3 = Color3.fromRGB(99, 120, 255)
Main.BorderColor3 = Color3.fromRGB(99, 120, 255)
Main.Position = UDim2.new(0, 0, 0, 0)
Main.Size = UDim2.new(0, 280, 0, 55)
Main.Font = Enum.Font.Nunito
Main.Text = "Main"
Main.TextColor3 = Color3.fromRGB(255, 19, 180)
Main.TextSize = 50.000

Script.Name = "Script"
Script.Parent = Frame
Script.BackgroundColor3 = Color3.fromRGB(99, 120, 255)
Script.BorderColor3 = Color3.fromRGB(99, 120, 255)
Script.Position = UDim2.new(0, 0, 0.299, 0)
Script.Size = UDim2.new(0, 316, 0, 67)
Script.Font = Enum.Font.PermanentMarker
Script.Text = "Script pop it"
Script.TextColor3 = Color3.fromRGB(0, 0, 0)
Script.TextSize = 40.000

Menu.Name = "Menu"
Menu.Parent = Frame
Menu.BackgroundColor3 = Color3.fromRGB(99, 120, 255)
Menu.BorderColor3 = Color3.fromRGB(99, 120, 255)
Menu.Position = UDim2.new(0, 0, 0.663, 0)
Menu.Size = UDim2.new(0, 316, 0, 62)
Menu.Font = Enum.Font.PermanentMarker
Menu.Text = "Menu"
Menu.TextColor3 = Color3.fromRGB(198, 255, 137)
Menu.TextSize = 88.000
Menu.MouseButton1Down:connect(function()
    MENU.Visible = true
end)

X.Name = "X"
X.Parent = Frame
X.BackgroundColor3 = Color3.fromRGB(99, 120, 255)
X.BorderColor3 = Color3.fromRGB(255, 85, 0)
X.Position = UDim2.new(0.886, 0, 0, 0)
X.Size = UDim2.new(0, 36, 0, 55)
X.Font = Enum.Font.GothamBold
X.Text = "X"
X.TextColor3 = Color3.fromRGB(255, 0, 0)	
X.TextStrokeColor3 = Color3.fromRGB(255, 78, 19)
X.TextSize = 60.000
X.MouseButton1Down:connect(function()
    Frame.Visible = false
    Open.Visible = true
end)

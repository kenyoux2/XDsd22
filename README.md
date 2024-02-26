
--Script 

_G.FastAttack = true

if game.PlaceId == 2753915549 then
	World1 = true 
elseif game.PlaceId == 4442272183 then
	World2 = true
elseif game.PlaceId == 7449423635 then
	World3 = true
end

local function QuestCheck()
	local Lvl = game:GetService("Players").LocalPlayer.Data.Level.Value
	if Lvl >= 1 and Lvl <= 9 then
		if tostring(game.Players.LocalPlayer.Team) == "Marines" then
			MobName = "Trainee"
			QuestName = "MarineQuest"
			QuestLevel = 1
			Mon = "Trainee"
			NPCPosition = CFrame.new(-2709.67944, 24.5206585, 2104.24585, -0.744724929, -3.97967455e-08, -0.667371571, 4.32403588e-08, 1, -1.07884304e-07, 0.667371571, -1.09201515e-07, -0.744724929)
		elseif tostring(game.Players.LocalPlayer.Team) == "Pirates" then
			MobName = "Bandit"
			Mon = "Bandit"
			QuestName = "BanditQuest1"
			QuestLevel = 1
			NPCPosition = CFrame.new(1059.99731, 16.9222069, 1549.28162, -0.95466274, 7.29721794e-09, 0.297689587, 1.05190106e-08, 1, 9.22064114e-09, -0.297689587, 1.19340022e-08, -0.95466274)
		end
		return {
			[1] = QuestLevel,
			[2] = NPCPosition,
			[3] = MobName,
			[4] = QuestName,
			[5] = LevelRequire,
			[6] = Mon,
			[7] = MobCFrame
		}
	end

	if Lvl >= 210 and Lvl <= 249 then
		MobName = "Dangerous Prisoner"
		QuestName = "PrisonerQuest"
		QuestLevel = 2
		Mon = "Dangerous Prisoner"
		NPCPosition = CFrame.new(5308.93115, 1.65517521, 475.120514, -0.0894274712, -5.00292918e-09, -0.995993316, 1.60817859e-09, 1, -5.16744869e-09, 0.995993316, -2.06384709e-09, -0.0894274712)
		local matchingCFrames = {}
		local result = string.gsub(MobName, "Lv. ", "")
		local result2 = string.gsub(result, "[%[%]]", "")
		local result3 = string.gsub(result2, "%d+", "")
		local result4 = string.gsub(result3, "%s+", "")

		for i,v in pairs(game.workspace.EnemySpawns:GetChildren()) do
			if v.Name == result4 then
				table.insert(matchingCFrames, v.CFrame)
			end
			MobCFrame = matchingCFrames
		end
		return {
			[1] = QuestLevel,
			[2] = NPCPosition,
			[3] = MobName,
			[4] = QuestName,
			[5] = LevelRequire,
			[6] = Mon,
			[7] = MobCFrame
		}
	end

	--game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
	local GuideModule = require(game:GetService("ReplicatedStorage").GuideModule)
	local Quests = require(game:GetService("ReplicatedStorage").Quests)
	for i,v in pairs(GuideModule["Data"]["NPCList"]) do
		for i1,v1 in pairs(v["Levels"]) do
			if Lvl >= v1 then
				if not LevelRequire then
					LevelRequire = 0
				end
				if v1 > LevelRequire then
					NPCPosition = i["CFrame"]
					QuestLevel = i1
					LevelRequire = v1
				end
				if #v["Levels"] == 3 and QuestLevel == 3 then
					NPCPosition = i["CFrame"]
					QuestLevel = 2
					LevelRequire = v["Levels"][2]
				end
			end
		end
	end
	if Lvl >= 375 and Lvl <= 399 then -- Fishman Warrior
		if _G.Auto_Farm_Level and (NPCPosition.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
		end
	end

	if Lvl >= 400 and Lvl <= 449 then -- Fishman Commando
		if _G.Auto_Farm_Level and (NPCPosition.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
		end
	end
	for i,v in pairs(Quests) do
		for i1,v1 in pairs(v) do
			if v1["LevelReq"] == LevelRequire and i ~= "CitizenQuest" then
				QuestName = i
				for i2,v2 in pairs(v1["Task"]) do
					MobName = i2
					Mon = string.split(i2," [Lv. ".. v1["LevelReq"] .. "]")[1]
				end
			end
		end
	end
	if QuestName == "MarineQuest2" then
		QuestName = "MarineQuest2"
		QuestLevel = 1
		MobName = "Chief Petty Officer"
		Mon = "Chief Petty Officer"
		LevelRequire = 120
	elseif QuestName == "ImpelQuest" then
		QuestName = "PrisonerQuest"
		QuestLevel = 2
		MobName = "Dangerous Prisoner"
		Mon = "Dangerous Prisoner"
		LevelRequire = 210
		NPCPosition = CFrame.new(5310.60547, 0.350014925, 474.946594, 0.0175017118, 0, 0.999846935, 0, 1, 0, -0.999846935, 0, 0.0175017118)
	elseif QuestName == "SkyExp1Quest" then
		if QuestLevel == 1 then
			NPCPosition = CFrame.new(-4721.88867, 843.874695, -1949.96643, 0.996191859, -0, -0.0871884301, 0, 1, -0, 0.0871884301, 0, 0.996191859)
		elseif QuestLevel == 2 then
			NPCPosition = CFrame.new(-7859.09814, 5544.19043, -381.476196, -0.422592998, 0, 0.906319618, 0, 1, 0, -0.906319618, 0, -0.422592998)
		end
	elseif QuestName == "Area2Quest" and QuestLevel == 2 then
		QuestName = "Area2Quest"
		QuestLevel = 1
		MobName = "Swan Pirate"
		Mon = "Swan Pirate"
		LevelRequire = 775
	end
	MobName = MobName:sub(1,#MobName)
	if not MobName:find("Lv") then
		for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
			MonLV = string.match(v.Name, "%d+")
			if v.Name:find(MobName) and #v.Name > #MobName and tonumber(MonLV) <= Lvl + 50 then
				MobName = v.Name
			end
		end
	end
	if not MobName:find("Lv") then
		for i,v in pairs(game:GetService("ReplicatedStorage"):GetChildren()) do
			MonLV = string.match(v.Name, "%d+")
			if v.Name:find(MobName) and #v.Name > #MobName and tonumber(MonLV) <= Lvl + 50 then
				MobName = v.Name
				Mon = a
			end
		end
	end

	local matchingCFrames = {}
	local result = string.gsub(MobName, "Lv. ", "")
	local result2 = string.gsub(result, "[%[%]]", "")
	local result3 = string.gsub(result2, "%d+", "")
	local result4 = string.gsub(result3, "%s+", "")

	for i,v in pairs(game.workspace.EnemySpawns:GetChildren()) do
		if v.Name == result4 then
			table.insert(matchingCFrames, v.CFrame)
		else
			table.insert(matchingCFrames, nil)
		end
		MobCFrame = matchingCFrames
	end

	return {
		[1] = QuestLevel,
		[2] = NPCPosition,
		[3] = MobName,
		[4] = QuestName,
		[5] = LevelRequire,
		[6] = Mon,
		[7] = MobCFrame,
		[8] = MonQ,
		[9] = MobCFrameNuber
	}
end

--------------------------------------------------------------------------------------

function AutoHaki()
	if not game:GetService("Players").LocalPlayer.Character:FindFirstChild("HasBuso") then
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
	end
end

function EquipWeapon(ToolSe)
	if not _G.NotAutoEquip then
		if game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe) then
			Tool = game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe)
			wait(.1)
			game.Players.LocalPlayer.Character.Humanoid:EquipTool(Tool)
		end
	end
end

function Bypass(Position)
	local CFramePos = Position
	_G.StopTween =  true
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(111111,111111,111111)
	wait()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Position
	wait()
	game.Players.LocalPlayer.Character.Head:Destroy()
	wait()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Position
	wait()
	local args = {
		[1] = "SetSpawnPoint"
	}

	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	wait()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Position

	wait()
	local args = {
		[1] = "SetSpawnPoint"
	}

	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	wait(0.1)
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Position
	wait()
	local args = {
		[1] = "SetSpawnPoint"
	}

	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	wait()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(111111,111111,111111)
	wait()
	game.Players.LocalPlayer.Character.Head:Destroy()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(99999999,99999999,99999999)
	wait()
	local args = {
		[1] = "SetLastSpawnPoint",
		[2] = tostring(game:GetService("Players").LocalPlayer.Data.SpawnPoint.Value)
	}

	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	wait()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Position
	wait()
	local args = {
		[1] = "SetSpawnPoint"
	}

	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	wait()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(99999999,99999999,99999999)
	wait()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(99999999,99999999,99999999)
	wait()
	local args = {
		[1] = "SetLastSpawnPoint",
		[2] = tostring(game:GetService("Players").LocalPlayer.Data.SpawnPoint.Value)
	}

	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	wait()
	local args = {
		[1] = "SetLastSpawnPoint",
		[2] = tostring(game:GetService("Players").LocalPlayer.Data.SpawnPoint.Value)
	}

	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	wait(0.5)
	local args = {
		[1] = "SetLastSpawnPoint",
		[2] = tostring(game:GetService("Players").LocalPlayer.Data.SpawnPoint.Value)
	}

	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	wait()
	wait()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Position
	wait()
	game.Players.LocalPlayer.Character.Head:Destroy()
	wait()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Position
	wait()
	_G.StopTween = false
	return
end


getgenv().ToTarget = function(Pos)
	Distance = (Pos.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
	if game.Players.LocalPlayer.Character.Humanoid.Sit == true then game.Players.LocalPlayer.Character.Humanoid.Sit = false end
	pcall(function() tween = game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart,TweenInfo.new(Distance/290, Enum.EasingStyle.Linear),{CFrame = Pos}) end)
	tween:Play()
	if Distance <= 250 then
		tween:Cancel()
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
	end
	if _G.StopTween == true then
		tween:Cancel()
		_G.Clip = false
	end
	if Distance <= 100 then
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
	end
end

function StopTween(target)
	if not target then
		getgenv().ToTarget(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame)
		_G.StopTween = true
		_G.UseSkill = false
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
		if game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
			game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip"):Destroy()
		end
		wait(0.2)
		_G.StopTween = false
		_G.Clip = false
	end
	if game.Players.LocalPlayer.Character:FindFirstChild('Highlight') then
		game.Players.LocalPlayer.Character:FindFirstChild('Highlight'):Destroy()
	end
end

spawn(function()
	pcall(function()
		game:GetService("RunService").Stepped:Connect(function()
			if _G.Auto_Farm_Level then
				if not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
					local Noclip = Instance.new("BodyVelocity")
					Noclip.Name = "BodyClip"
					Noclip.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
					Noclip.MaxForce = Vector3.new(100000,100000,100000)
					Noclip.Velocity = Vector3.new(0,0,0)
				end
			else	
				if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
					game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip"):Destroy()
				end
			end
		end)
	end)
end)


canHits = {}
_G.FastAttack = true

_Module_ = function()
	local Success,Error = pcall(function()
		local PC = require(game.Players.LocalPlayer.PlayerScripts.CombatFramework.Particle)
		local RL = require(game:GetService("ReplicatedStorage").CombatFramework.RigLib)
		local DMG = require(game.Players.LocalPlayer.PlayerScripts.CombatFramework.Particle.Damage)
		local RigC = getupvalue(require(game.Players.LocalPlayer.PlayerScripts.CombatFramework.RigController), 2)
		local Combat = getupvalue(require(game.Players.LocalPlayer.PlayerScripts.CombatFramework), 2)
		local CameraShaker = require(game.ReplicatedStorage.Util.CameraShaker)
		local RigEvent = game:GetService("ReplicatedStorage").RigControllerEvent
		return {
			[1] = PC,
			[2] = RL,
			[3] = DMG,
			[4] = RigC,
			[5] = Combat,
			[6] = CameraShaker,
			[7] = RigEvent
		}
	end
	if not Success then
		warn("Module Error Send this message to mexuaita\n",Error)
	end
end

_getHits_ = function(table,self)
	local Hits = {}
	local nearbymon = false
	local Success,Error = pcall(function()
		if nearbymon then
			local Enemies = game.workspace.Enemies:GetChildren()
			local Characters = game.workspace.Characters:GetChildren()
			for i = 1, #Enemies do
				local v = Enemies[i]
				local Human = v:FindFirstChildOfClass("Humanoid")
				if Human and Human.RootPart and Human.Health > 0 and (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 50 then
					canHits[#canHits + 1] = Human.RootPart
				end
			end
			for i = 1, #Characters do
				local v = Characters[i]
				if v ~= Client.Character then
					local Human = v:FindFirstChildOfClass("Humanoid")
					if Human and Human.RootPart and Human.Health > 0 and (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 50 then
						canHits[#canHits + 1] = Human.RootPart
					end
				end
			end
		end
	end)
	if not Success then
		warn("Position Error Send this message to mexuaita\n",Error)
	end
	return Hits
end

task.spawn(function()
	local Success,Error = pcall(function()
		local Data = _Module_()[5]
		local Animation = Instance.new("Animation")
		local AttackCD = 0
		local Controller
		local lastFireValid = 0
		local MaxLag = 350
		local fucker = 0.07
		local TryLag = 0

		local resetCD = function()
			local WeaponName = Controller.currentWeaponModel.Name
			local Cooldown = {
				combat = 0.07
			}
			AttackCD = tick() + (fucker and Cooldown[WeaponName:lower()] or fucker or 0.285) + ((TryLag / MaxLag) * 0.3)
			_Module_()[7]:FireServer("weaponChange", WeaponName)
			TryLag = TryLag + 0.8
			task.delay((fucker or 0.285) + (TryLag + 0.5 / MaxLag) * 0.3, function()
				TryLag = TryLag - 0.8
			end)
		end

		if not shared.orl then
			shared.orl = _Module_()[2].wrapAttackAnimationAsync
		end

		if not shared.cpc then
			shared.cpc = _Module_()[1].play
		end

		if not shared.dnew then
			shared.dnew = _Module_()[3].new
		end

		if not shared.attack then
			shared.attack = _Module_()[4].attack
		end

		_Module_()[2].wrapAttackAnimationAsync = function(a, b, c, d, func)
			if not _G.FastAttack then
				_Module_()[1].play = shared.cpc
				return shared.orl(a, b, c, 50, func)
			end

			local Radius = _G.FastAttack or 50

			if canHits and #canHits > 0 then
				_Module_()[1].play = function() end
				a:Play(0.00075, 0.01, 0.01)
				func(canHits)
				wait(a.length * 0.5)
				a:Stop()
			end
		end

		while game:GetService("RunService").Stepped:Wait() do
			if #canHits > 0 then
				Controller = Data.activeController

				if Controller and Controller.equipped and Controller.currentWeaponModel then
					if _G.FastAttack then
						if _G.FastAttack and tick() > AttackCD then
							resetCD()
						end

						if tick() - lastFireValid > 0.5 or not _G.FastAttack then
							Controller.timeToNextAttack = 0
							Controller.hitboxMagnitude = 65
							pcall(task.spawn, Controller.attack, Controller)
							lastFireValid = tick()
							_Module_()[6]:Stop()
						end

						local AID3 = Controller.anims.basic[3]
						local AID2 = Controller.anims.basic[2]
						local ID = AID3 or AID2
						Animation.AnimationId = ID
						local Playing = Controller.humanoid:LoadAnimation(Animation)
						Playing:Play(0.00075, 0.01, 0.01)
						_Module_()[7]:FireServer("hit", canHits, AID3 and 3 or 2, "")
						delay(0.5, function()
							Playing:Stop()
						end)
					end
				end
			end
		end
	end)
	if not Success then
		warn("Fast Attack Error Send this message to mexuaita\n",Error)
	end
end)


--------------------------------------------------------------------------------------------------------------------------------------------------------
local Notification = loadstring(game:HttpGet("https://raw.githubusercontent.com/Jxereas/UI-Libraries/main/notification_gui_library.lua", true))()
local notif4 = Notification.new("success", "Zay Hub", "Success ✅")
wait(2)
notif4:delete()

local PepsisWorld = library:Evil()

local MainTab = PepsisWorld:CreateTab({
	Name = "General"
})

local MainSection = MainTab:CreateSection({
	Name = "Main",
	Side = "Left"
})

MainSection:AddToggle({
	Name = "Auto Farm Level",
	Flag = "Auto_Farm_Level",
	Value = false,
	Callback = function(value)
		_G.Auto_Farm_Level = value 
		StopTween(_G.Auto_Farm_Level)
	end
})

spawn(function()
	while wait() do
		pcall(function()
			if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true then
				if game:GetService("Workspace").Enemies:FindFirstChild(QuestCheck()[3]) then
					for _,_self in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
						if string.find(_self.Name,QuestCheck()[3]) then
							if _self:FindFirstChild("Humanoid") and _self:FindFirstChild("HumanoidRootPart") and _self.Humanoid.Health > 0 then
								repeat task.wait()
									if not string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, QuestCheck()[6]) then
										game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
									else												
										PosMon = _self.HumanoidRootPart.CFrame
										_self.HumanoidRootPart.Size = Vector3.new(60,60,60)
										_self.HumanoidRootPart.CanCollide = false
										_self.Humanoid.WalkSpeed = 0
										_self.Head.CanCollide = false
										local HowFar = 50 and Vector3.new(0,50,0) and Vector3.new(0,60,0) or Vector3.new(0,50,0)
										if math.abs(_self.HumanoidRootPart.RootPart.Position.X - 1000) < 25 then
											local a = _self.HumanoidRootPart.RootPart.Position + HowFar + Vector3.new(math.random(-1,1)/4,0,math.random(-1,1)/4)
											print(math.floor(a.X),math.floor(a.X),math.floor(a.Z))
										end
										getgenv().ToTarget(_self.HumanoidRootPart.RootPart.Position + HowFar)
										EquipWeapon(_G.Select_Weapon)
										_self.HumanoidRootPart.Transparency = 1
										getgenv().ToTarget(_self.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
										game:GetService("VirtualUser"):CaptureController()
										game:GetService("VirtualUser"):Button1Down(Vector2.new(1280,672))
									end
								until not _G.Auto_Farm_Level or not _self.Parent or _self.Humanoid.Health <= 0 or QuestC.Visible == false or not _self:FindFirstChild("HumanoidRootPart")
							end
						end
					end
				else
					for _,_self in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
						for _,__x in pairs(workspace._WorldOrigin.EnemySpawns:GetChildren()) do
							if __x.Name == "Baking Staff" or __x.Name == "Head Baker" or __x.Name == "Cake Guard" or __x.Name == "Cookie Crafter" then local CFrameEnemySpawns = __x.CFrame  wait(0.5)
								repeat wait() 
									getgenv().ToTarget(CFrameEnemySpawns * CFrame.new(0,30,0)) 
								until _self.Humanoid.Health <= 0 or not _G.Auto_Farm_Level
							end
						end
					end
				end
			else
				getgenv().ToTarget(QuestCheck()[2])
				if (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 1 then
					BringMobFarm = false
					wait(0.2)
					game:GetService('ReplicatedStorage').Remotes.CommF_:InvokeServer("StartQuest", QuestCheck()[4], QuestCheck()[1]) wait(0.5)
					getgenv().ToTarget(QuestCheck()[7][1] * CFrame.new(0,30,20))
				else
					if (QuestCheck()[2].Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 2000 then
						Bypass(QuestCheck()[2])
						return
					else
						getgenv().ToTarget(QuestCheck()[2])
					end
				end
			end
		end)
	end
end)


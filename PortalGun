if not owner then
	owner = script.Parent.Parent

	function NS(code, parent)
		local ss = script.ServerScript:Clone()
		ss.Code.Value = code
		ss.Parent = parent
		ss.Disabled = false
	end

	function NLS(code, parent)
		local ls = script.LocalScript:Clone()
		ls.Code.Value = code
		ls.Parent = parent
		ls.Disabled = false
	end

	task.wait(1)
end

local function weld(p0, p1)
	local w = Instance.new("WeldConstraint")
	w.Part0 = p0
	w.Part1 = p1
	w.Parent = p0
end

local tool = Instance.new("Tool")
tool.Name = "Portal Gun"
tool.Grip = CFrame.Angles(0, 0, math.rad(-90)) * CFrame.new(0, -0.325, 0)

local handle = Instance.new("Part")
handle.Name = "Handle"
handle.Material = Enum.Material.SmoothPlastic
handle.Color = Color3.fromRGB(255, 255, 255)
handle.Size = Vector3.new(0.75, 0.625, 0.5)
handle.Orientation = Vector3.new(90, 0, 0)
handle.Shape = Enum.PartType.Cylinder
handle.Parent = tool

local bottomSphere = Instance.new("Part")
bottomSphere.Shape = Enum.PartType.Ball
bottomSphere.Size = Vector3.new(0.5, 0.5, 0.5)
bottomSphere.CFrame = handle.CFrame * CFrame.new(-handle.Size.X/2, 0, 0)
bottomSphere.Material = Enum.Material.SmoothPlastic
bottomSphere.Color = Color3.fromRGB(255, 255, 255)
weld(bottomSphere, handle)
bottomSphere.Parent = handle

local mainPart = Instance.new("Part")
mainPart.Material = Enum.Material.SmoothPlastic
mainPart.Color = Color3.fromRGB(255, 255, 255)
mainPart.Size = Vector3.new(0.5, 1, 1.75)
mainPart.CFrame = handle.CFrame * CFrame.new(handle.Size.X/2+0.125, 0, -mainPart.Size.Z/2+0.1)
weld(mainPart, handle)
mainPart.Parent = handle

local mainPartHandleConnect = Instance.new("Part")
mainPartHandleConnect.Material = Enum.Material.SmoothPlastic
mainPartHandleConnect.CFrame = (mainPart.CFrame * CFrame.new(0, 0, mainPart.Size.Z/2)) * CFrame.Angles(0, 0, math.rad(-90))
mainPartHandleConnect.Shape = Enum.PartType.Cylinder
mainPartHandleConnect.Size = Vector3.new(mainPart.Size.Y, 0.5, 0.5)
mainPartHandleConnect.Color = Color3.fromRGB(255, 255, 255)
weld(mainPartHandleConnect, mainPart)
mainPartHandleConnect.Parent = mainPart

local button = Instance.new("Part")
button.Material = Enum.Material.SmoothPlastic
button.Color = Color3.fromRGB(50, 50, 50)
button.Size = Vector3.new(0.25, 0.25, 0.25)
button.Shape = Enum.PartType.Cylinder
button.CFrame = ((mainPartHandleConnect.CFrame * CFrame.new(0, mainPartHandleConnect.Size.Y/2, 0)) * CFrame.Angles(math.rad(45), 0, math.rad(90))) * CFrame.new(0, 0, 0.125)
weld(button, mainPartHandleConnect)
button.Parent = mainPart

local display = Instance.new("Part")
display.Material = Enum.Material.SmoothPlastic
display.Size = Vector3.new(0.1, 0.75, 0.25)
display.CFrame = mainPart.CFrame * CFrame.new(0.201, 0, 0.6)
display.Color = Color3.fromRGB(225, 0, 0)
weld(display, mainPart)
display.Parent = mainPart

local middleCylinder = Instance.new("Part")
middleCylinder.Material = Enum.Material.SmoothPlastic
middleCylinder.Size = Vector3.new(0.1, 0.4, 0.4)
middleCylinder.CFrame = mainPart.CFrame * CFrame.new(0.3, 0, 0)
middleCylinder.Shape = Enum.PartType.Cylinder
middleCylinder.Color = Color3.fromRGB(255, 255, 255)
weld(middleCylinder, mainPart)
middleCylinder.Parent = mainPart

local energyThing = Instance.new("Part")
energyThing.Color = Color3.fromRGB(100, 255, 100)
energyThing.Size = Vector3.new(0.6, 0.4, 0.4)
energyThing.Material = Enum.Material.Glass
energyThing.Transparency = 0.5
energyThing.CFrame = middleCylinder.CFrame * CFrame.new(0.35, 0, 0)
energyThing.Shape = Enum.PartType.Cylinder
weld(energyThing, middleCylinder)
energyThing.Parent = middleCylinder

local energyThingTopSphere = Instance.new("Part")
energyThingTopSphere.Color = Color3.fromRGB(100, 255, 100)
energyThingTopSphere.Size = Vector3.new(0.4, 0.4, 0.4)
energyThingTopSphere.Material = Enum.Material.Glass
energyThingTopSphere.Transparency = 0.5
energyThingTopSphere.CFrame = energyThing.CFrame * CFrame.new(energyThing.Size.X/2, 0, 0)
energyThingTopSphere.Shape = Enum.PartType.Ball
weld(energyThingTopSphere, energyThing)
energyThingTopSphere.Parent = energyThing

NLS([[

script.Parent:WaitForChild("KEY_REMOTE").OnClientInvoke = function()
	return game:GetService("Players").LocalPlayer:GetMouse().Hit
end

local a = {'Q', 'E'}
game:GetService("UserInputService").InputBegan:Connect(function(i, gpe)
	if not gpe then
		if table.find(a, i.KeyCode.Name) then
			script.Parent.KEY_REMOTE:InvokeServer(i.KeyCode.Name)
		end
	end
end)

]], tool)

local rf = Instance.new("RemoteFunction")
rf.Name = "KEY_REMOTE"
rf.Parent = tool

local db = false
rf.OnServerInvoke = function(plr, k)
	if plr == owner then
		if db then return end
		db = true
		if k == "Q" then
			for _, v in pairs(owner.Character:GetChildren()) do
				if v.Name == "Portal" then
					game:GetService("TweenService"):Create(v, TweenInfo.new(0.5, Enum.EasingStyle.Back, Enum.EasingDirection.In), {Size = Vector3.new(0, 0, 0)}):Play()
					game:GetService("Debris"):AddItem(v, 0.501)
				end
			end
		elseif k == "E" then
			local portalPart = Instance.new("Part")
			portalPart.Name = "Portal"
			portalPart.Size = Vector3.new(0.25, 0.25, 0.25)
			portalPart.CanCollide = false
			portalPart.Anchored = true
			portalPart.CFrame = mainPart.CFrame * CFrame.Angles(0, math.rad(90), 0)
			portalPart.Transparency = 1

			local decal = Instance.new("Decal")
			decal.Texture = "rbxassetid://383899755"
			decal.Parent = portalPart
			decal.Face = Enum.NormalId.Left

			local dC = decal:Clone()
			dC.Face = Enum.NormalId.Right
			dC.Parent = portalPart

			portalPart.Parent = owner.Character
			game:GetService("TweenService"):Create(portalPart, TweenInfo.new(0.75), {Size = Vector3.new(0.001, 7.5, 11.125), CFrame = owner.Character.HumanoidRootPart.CFrame * CFrame.new(0, 1.125, -10) * CFrame.Angles(0, math.rad(90), 0)}):Play()
			coroutine.wrap(function()
				while portalPart do
					portalPart.CFrame *= CFrame.Angles(math.rad(0.5), 0, 0)
					task.wait()
				end
			end)()
			task.wait(1.5)
			
			owner.Character.Archivable = true
			local morty = owner.Character:Clone()
			morty:SetPrimaryPartCFrame(portalPart.CFrame * CFrame.Angles(0, math.rad(90), 0))
			coroutine.wrap(function()
				local closest
				--// This is so efficient
				for _, v in pairs(workspace:GetDescendants()) do
					if v:IsA("Humanoid") then
						closest = v.Parent.HumanoidRootPart
					end
				end
				if not closest then return end
				morty.Humanoid:MoveTo(closest.Position, closest, true)
				task.wait(10)
				local e = Instance.new("Explosion")
				e.Position = morty.HumanoidRootPart.Position
				e.Parent = morty
			end)()
			for _, v in pairs(morty:GetChildren()) do
				if v.Name == "Portal" then
					v:Destroy()
				end
			end
			pcall(function()
				morty['Portal Gun']:Destroy()
			end)
			morty.Humanoid.DisplayName = "Morty"
			morty.Parent = workspace
			
			local shirt = morty:FindFirstChildWhichIsA("Shirt") or Instance.new("Shirt", morty)
			shirt.ShirtTemplate = "rbxassetid://5962444893"
			local pants = morty:FindFirstChildWhichIsA("Pants") or Instance.new("Pants", morty)
			pants.PantsTemplate = "rbxassetid://129458425"

			for _, v in pairs(morty:GetChildren()) do
				if v:IsA("Accessory") then
					v:Destroy()
				end
			end
			
			local accessory = Instance.new("Accessory")
			do
				accessory.Name = "BoyNormalHair1"
				
				local handle = Instance.new("Part")
				handle.Name = "Handle"
				handle.Size = Vector3.new(1, 0.8, 1)
				handle.Parent = accessory
				
				local hairAttachment = Instance.new("Attachment")
				hairAttachment.Name = "HairAttachment"
				hairAttachment.Position = Vector3.new(0, 0.25, -0.063)
				hairAttachment.Orientation = Vector3.new(-1.718, 0, 0)
				hairAttachment.Parent = handle
				
				local mesh = Instance.new("SpecialMesh")
				mesh.Scale = Vector3.new(1.05, 1, 1.05)
				mesh.MeshId = "rbxassetid://13332444"
				mesh.TextureId = "rbxassetid://13332337"
				mesh.Parent = handle
				
			end
			
			morty.Humanoid:AddAccessory(accessory)
			
			task.wait(0.5)
			game:GetService("TweenService"):Create(portalPart, TweenInfo.new(0.5, Enum.EasingStyle.Back, Enum.EasingDirection.In), {Size = Vector3.new(0, 0, 0)}):Play()
			task.wait(0.501) --// No debris for db
			portalPart:Destroy()
			
		end
		db = false
	end
end

tool.Activated:Connect(function()
	if db then return end
	db = true
	local portalPart = Instance.new("Part")
	portalPart.Name = "Portal"
	portalPart.Size = Vector3.new(0.25, 0.25, 0.25)
	portalPart.CanCollide = false
	portalPart.Anchored = true
	portalPart.CFrame = mainPart.CFrame * CFrame.Angles(0, math.rad(90), 0)
	portalPart.Transparency = 1
	
	local decal = Instance.new("Decal")
	decal.Texture = "rbxassetid://383899755"
	decal.Parent = portalPart
	decal.Face = Enum.NormalId.Left
	
	local dC = decal:Clone()
	dC.Face = Enum.NormalId.Right
	dC.Parent = portalPart
	
	portalPart.Parent = owner.Character
	game:GetService("TweenService"):Create(portalPart, TweenInfo.new(0.75), {Size = Vector3.new(0.001, 7.5, 11.125), CFrame = owner.Character.HumanoidRootPart.CFrame * CFrame.new(0, 1.125, -10) * CFrame.Angles(0, math.rad(90), 0)}):Play()
	
	local otherPortal = portalPart:Clone()
	local pos = rf:InvokeClient(owner).Position
	
	otherPortal.Position = pos + Vector3.new(0, 5, 0)
	otherPortal.Parent = owner.Character
	
	local portalDB = {}
	otherPortal.Touched:Connect(function(hit)
		if table.find(portalDB, hit.Parent) then return end
		if hit.Parent:FindFirstChild("Humanoid") then
			table.insert(portalDB, hit.Parent)
			hit.Parent.HumanoidRootPart.CFrame = CFrame.new(portalPart.Position, hit.Parent.HumanoidRootPart.CFrame.LookVector)
			task.wait(1)
			table.remove(portalDB, table.find(portalDB, hit.Parent))
		end
	end)
	
	portalPart.Touched:Connect(function(hit)
		if table.find(portalDB, hit.Parent) then return end
		if hit.Parent:FindFirstChild("Humanoid") then
			table.insert(portalDB, hit.Parent)
			hit.Parent.HumanoidRootPart.CFrame = CFrame.new(otherPortal.Position, hit.Parent.HumanoidRootPart.CFrame.LookVector)
			task.wait(1)
			table.remove(portalDB, table.find(portalDB, hit.Parent))
		end
	end)
	
	game:GetService("TweenService"):Create(otherPortal, TweenInfo.new(0.75), {Size = Vector3.new(0.001, 7.5, 11.125)}):Play()
	
	coroutine.wrap(function()
		while portalPart do
			portalPart.CFrame *= CFrame.Angles(math.rad(0.5), 0, 0)
			otherPortal.CFrame *= CFrame.Angles(math.rad(0.5), 0, 0)
			task.wait()
		end
	end)()
	
	task.wait(1)
	
	db = false
end)

for _, v in pairs(tool:GetDescendants()) do
	if v:IsA("BasePart") then
		v.CanCollide = false
	end
end
tool.Parent = owner.Backpack

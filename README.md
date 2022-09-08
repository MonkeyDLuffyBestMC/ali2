local IsHitting = false
local Proto1 = nil
local Proto2 = nil
local Proto3 = nil
local TweenService = game:GetService("TweenService")
local ChargeTimeE = 0.3
local ChargeTimeR = 0.5
local ChargeTimeZ = 0.4
local ChargeTimeX = 0.2
local ChargeTimeC = 0.4
local Timer = nil
local UltCharging = false
local UltSize = 10
 
script.Parent.OnServerEvent:Connect(function(plr, val, Item1, Item2, Item3) 
    if val == "holdE" then
        Timer = ChargeTimeE
        for i = 1,ChargeTimeE*10 do
            Timer = Timer - 0.1
            wait(0.1)
        end
        local Value = Instance.new("StringValue")
        Value.Name = "1LightningParalyzeValue"
        Value.Parent = plr.Character
        Proto2 = Value
    elseif val == "releaseE" then
        IsHitting = true
        game.ReplicatedStorage.FireClientEvent:FireAllClients("LightningCloud", plr.Character.RightHand)
        local Projectile = game.ReplicatedStorage.Goro.Radius:Clone()
        local Item22 = math.clamp(Item2, 20, 100)
        Projectile.Size = Vector3.new(Item22, Item22, Item22)
        Projectile.Transparency = 1
        Projectile.Anchored = true
        Projectile.Parent = workspace.Visuals
        Projectile.Sound:Play()
        Projectile.Sound.TimePosition = 0.7
        game.Debris:AddItem(Proto2, 2)
        Proto2 = nil
        Projectile.CFrame = Item1
        Projectile.Touched:Connect(function(hit)
            if hit.Parent:FindFirstChild("Humanoid") and IsHitting == true then
                if hit.Parent.Name ~= plr.Name and not hit.Parent:FindFirstChild("AlreadyHitLightningParalyze".. plr.Name) then
                    local Check = Instance.new("IntValue", hit.Parent)
                    Check.Name = "AlreadyHitLightningParalyze".. plr.Name
                    game.Debris:AddItem(Check ,1)
                    hit.Parent.PrimaryPart.Anchored = false
                    local B2V = Instance.new("BodyPosition",hit.Parent.PrimaryPart)
                    B2V.Position = hit.Parent.PrimaryPart.Position + Vector3.new(0,6,0)
                    B2V.MaxForce = Vector3.new(150000,150000,150000)
                    wait(math.random(1,3)/10)
                    hit.Parent.Humanoid:TakeDamage(10)
                    game.Debris:AddItem(B2V, 0.5)
                    game.ReplicatedStorage.FireClientEvent:FireAllClients("LightningCloud", hit.Parent.Head)
                end
            end
        end)
        wait(0.3)
        IsHitting = false
        game.Debris:AddItem(Projectile, 0.1)
    elseif val == "holdR" then
        Timer = ChargeTimeR
        for i = 1,ChargeTimeR*10 do
            Timer = Timer - 0.1
            wait(0.1)
        end
        local Value = Instance.new("StringValue")
        Value.Name = "2FlashSmashValue"
        Value.Parent = plr.Character
        Proto2 = Value
    elseif val == "releaseR" then
        Proto2:Destroy()
        Proto2 = nil
        plr.Character.PrimaryPart.CFrame = CFrame.new(Item2.X, Item2.Y + 4, Item2.Z) * CFrame.fromOrientation(Item1.Rotation.X*3.14/180,Item1.Rotation.Y*3.14/180,Item1.Rotation.Z*3.14/180)
        game.ReplicatedStorage.FireClientEvent:FireAllClients("GoroDash", plr, Item3, "ForAll")
        wait(0.4)
        local Projectile = game.ReplicatedStorage.Goro.Radius:Clone()
        Projectile.Size = Vector3.new(45,45,45)
        Projectile.Transparency = 1
        Projectile.Mesh:Destroy()
        Projectile.Anchored = true
        Projectile.Parent = workspace.Visuals
        Projectile.CFrame = CFrame.new(Item2)
        Projectile.Touched:Connect(function(hit)
            if hit.Parent:FindFirstChild("Humanoid") then
                if hit.Parent.Name ~= plr.Name and not hit.Parent:FindFirstChild("AlreadyHitFlashSmash".. plr.Name) then
                    local Check = Instance.new("IntValue", hit.Parent)
                    Check.Name = "AlreadyHitFlashSmash".. plr.Name
                    game.Debris:AddItem(Check ,1)
                    hit.Parent.PrimaryPart.Anchored = false
                    local B2V = Instance.new("BodyVelocity",hit.Parent.PrimaryPart)
                    B2V.Velocity = CFrame.new(Projectile.Position, hit.Parent.HumanoidRootPart.Position).LookVector * 30 + Projectile.CFrame.UpVector * 10
                    B2V.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                    hit.Parent.Humanoid:TakeDamage(20)
                    game.Debris:AddItem(B2V, 0.64)
                    game.ReplicatedStorage.FireClientEvent:FireAllClients("Electrify", hit.Parent)
                end
            end
        end)
        game.Debris:AddItem(Projectile, 0.6)
    elseif val == "holdZ" then
        Timer = ChargeTimeZ
        for i = 1,ChargeTimeZ*10 do
            Timer = Timer - 0.1
            wait(0.1)
        end
        local Value = Instance.new("StringValue")
        Value.Name = "3ElThorValue"
        Value.Parent = plr.Character
        Proto1 = Value
    elseif val == "releaseZ" then
        Proto1:Destroy()
        Proto1 = nil
        game.ReplicatedStorage.FireClientEvent:FireAllClients("ElThor", Item1, plr)
        for i = 1,10 do
            local Projectile = game.ReplicatedStorage.Goro.Radius:Clone()
            Projectile.Size = Vector3.new(80,80,80)
            Projectile.Transparency = 1
            Projectile.Mesh:Destroy()
            Projectile.Anchored = true
            Projectile.Parent = workspace.Visuals
            Projectile.CFrame = CFrame.new(Item1)
            Projectile.Touched:Connect(function(hit)
                if hit.Parent:FindFirstChild("Humanoid") then
                    if hit.Parent.Name ~= plr.Name and not hit.Parent:FindFirstChild("AlreadyHitElThor"..i.. plr.Name) then
                        local Check = Instance.new("IntValue", hit.Parent)
                        Check.Name = "AlreadyHitElThor"..i.. plr.Name
                        game.Debris:AddItem(Check, 1)
                        hit.Parent.PrimaryPart.Anchored = false
                        local B2V = Instance.new("BodyVelocity",hit.Parent.PrimaryPart)
                        B2V.Velocity = CFrame.new(Projectile.Position, Vector3.new(hit.Parent.HumanoidRootPart.Position.X,Projectile.Position.Y,hit.Parent.HumanoidRootPart.Position.Z)).LookVector * 60 + Projectile.CFrame.UpVector * 20
                        B2V.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                        hit.Parent.Humanoid:TakeDamage(5)
                        game.Debris:AddItem(B2V, 0.3)
                        game.ReplicatedStorage.FireClientEvent:FireAllClients("Electrify", hit.Parent)
                    end
                end
            end)
            game.Debris:AddItem(Projectile, 0.3)
            wait(0.2)
        end
    elseif val == "holdX" then
        Timer = ChargeTimeX
        for i = 1,ChargeTimeX*10 do
            Timer = Timer - 0.1
            wait(0.1)
        end
        local Value = Instance.new("StringValue")
        Value.Name = "4LightningDragonValue"
        Value.Parent = plr.Character
        Proto1 = Value
    elseif val == "releaseX" then
        game.Debris:AddItem(Proto1)
        Proto1 = nil
        local ray = Ray.new(Item1 + Vector3.new(0, 50, 0), Item1 - Vector3.new(0, 50000, 0))
        local HitPart, HitPos = game.Workspace:FindPartOnRayWithIgnoreList(ray, {game.Workspace.Visuals, plr.Character})
        local speed = math.clamp((plr.Character.PrimaryPart.CFrame.p - HitPos).Magnitude/10, 1, 8)
        local duration = (plr.Character.PrimaryPart.Position - HitPos).Magnitude / speed
        game.ReplicatedStorage.FireClientEvent:FireAllClients("LightningDragon", plr.Character.PrimaryPart, CFrame.new(HitPos), speed)
        delay(duration/20, function()
            local Projectile = game.ReplicatedStorage.Goro.Radius:Clone()
            Projectile.Size = Vector3.new(50,50,50)
            Projectile.Transparency = 1
            Projectile.Mesh:Destroy()
            Projectile.Anchored = true
            Projectile.Parent = workspace.Visuals
            Projectile.CFrame = CFrame.new(Item1)
            Projectile.Touched:Connect(function(hit)
                if hit.Parent:FindFirstChild("Humanoid") then
                    if hit.Parent.Name ~= plr.Name and not hit.Parent:FindFirstChild("AlreadyHitLightningDragon".. plr.Name) then
                        local Check = Instance.new("IntValue", hit.Parent)
                        Check.Name = "AlreadyHitLightningDragon".. plr.Name
                        game.Debris:AddItem(Check ,1)
                        hit.Parent.PrimaryPart.Anchored = false
                        local B2V = Instance.new("BodyVelocity",hit.Parent.PrimaryPart)
                        B2V.Velocity = CFrame.new(Projectile.Position, hit.Parent.HumanoidRootPart.Position).LookVector * 60 + Projectile.CFrame.UpVector * 10
                        B2V.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                        hit.Parent.Humanoid:TakeDamage(20)
                        game.Debris:AddItem(B2V, 0.3)
                        game.ReplicatedStorage.FireClientEvent:FireAllClients("Electrify", hit.Parent)
                    end
                end
            end)
            game.Debris:AddItem(Projectile, 0.6)
        end)
    elseif val == "holdC" then
        local prevVal = plr.Character:FindFirstChild("5GoroUltValue")
        if prevVal then
            prevVal:Destroy()
        end
        local ThunderBomb = game.ReplicatedStorage.Goro.ThunderBomb:Clone()
        ThunderBomb.Parent = game.Workspace.Visuals
        ThunderBomb.Position = plr.Character.PrimaryPart.Position + Vector3.new(0, 150, 0)
        ThunderBomb.Inner.Position = plr.Character.PrimaryPart.Position + Vector3.new(0, 150, 0)
        ThunderBomb.Name = tostring(math.random(0,1000)).. "#" .. plr.Name.. "RaigoUltimate"
        Proto1 = ThunderBomb
        UltCharging = true
        local BV = Instance.new("BodyPosition", plr.Character.PrimaryPart)
        BV.MaxForce = Vector3.new(1000000000,7000000000,100000000)
        BV.Position = Vector3.new(plr.Character.PrimaryPart.Position.X, plr.Character.PrimaryPart.Position.Y + 45, plr.Character.PrimaryPart.Position.Z)
        Proto3 = BV
        game.ReplicatedStorage.FireClientEvent:FireAllClients("Raigo", ThunderBomb, plr.Character.PrimaryPart.Position + Vector3.new(0, 70, 0), BV)
        wait(0.4)
        Timer = ChargeTimeC
        for i = 1,ChargeTimeC*10 do
            Timer = Timer - 0.05
            wait(0.1)
        end
        local Value = Instance.new("StringValue")
        Value.Name = "5GoroUltValue"
        Value.Parent = plr.Character
        Proto2 = Value
        while UltCharging == true do
            if UltSize < 150 then
                UltSize = UltSize + 1
                ThunderBomb.Value.Value = UltSize
            end
            wait(0.05)
        end
    elseif val == "releaseC" then
        UltCharging = false
        local Hitting = true
        local ray = Ray.new(plr.Character.PrimaryPart.Position, CFrame.new(plr.Character.PrimaryPart.Position, Item2).LookVector * 1200)
        local HitPart, HitPos = game.Workspace:FindPartOnRayWithIgnoreList(ray, {game.Workspace.Visuals, plr.Character})
        local Distance = (Item2 - Proto1.Position).Magnitude/175 * math.clamp(Proto1.Value.Value/75, 0.75, math.huge)
        Proto1.Value.Value = -1
        Proto1.Size = Vector3.new(1.05 * UltSize, 1.05 * UltSize, 1.05 * UltSize)
        Proto1.Inner.Size = Vector3.new(UltSize, UltSize, UltSize)
        game.ReplicatedStorage.FireClientEvent:FireAllClients("RaigoThrow", Proto1, HitPos, Distance, HitPart)
        game.Debris:AddItem(Proto1, Distance + 5)
        Proto1 = nil
        Proto2:Destroy()
        Proto2 = nil
        delay(0.4, function()
            Proto3:Destroy()
            Proto3 = nil
        end)
        wait(Distance)
        local Projectile = game.ReplicatedStorage.Goro.Radius:Clone()
        Projectile.Size = Vector3.new(UltSize * 2.2,UltSize * 2.2, UltSize * 2.2)
        Projectile.Transparency = 1
        Projectile.Mesh:Destroy()
        Projectile.Anchored = true
        Projectile.Parent = workspace.Visuals
        Projectile.CFrame = CFrame.new(HitPos)
        Projectile.Touched:Connect(function(hit)
            if hit.Parent:FindFirstChild("Humanoid") and Hitting == true then
                if hit.Parent.Name ~= plr.Name and not hit.Parent:FindFirstChild("AlreadyHitLightningRaigoUlt".. plr.Name) then
                    local Check = Instance.new("IntValue", hit.Parent)
                    Check.Name = "AlreadyHitLightningRaigoUlt".. plr.Name
                    game.Debris:AddItem(Check ,1)
                    hit.Parent.PrimaryPart.Anchored = false
                    local B2V = Instance.new("BodyVelocity",hit.Parent.PrimaryPart)
                    B2V.Velocity = CFrame.new(Projectile.Position, hit.Parent.HumanoidRootPart.Position).LookVector * Projectile.Size.X/1.5 + Projectile.CFrame.UpVector * Projectile.Size.X/1.5
                    B2V.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                    hit.Parent.Humanoid:TakeDamage(20)
                    game.Debris:AddItem(B2V, 0.64)
                    game.ReplicatedStorage.FireClientEvent:FireAllClients("Electrify", hit.Parent)
                end
            end
        end)
        UltSize = 10
        game.Debris:AddItem(Projectile, 2)
        wait(2)
        Hitting = false
    elseif val == "GoroDash" then
        game.ReplicatedStorage.FireClientEvent:FireAllClients("GoroDash", plr, Item1, "NotForAll")
    elseif val == "GoroFlight1" then
        game.ReplicatedStorage.FireClientEvent:FireAllClients("GoroFlight1", plr.Character)
    elseif val == "GoroFlight2" then
        game.ReplicatedStorage.FireClientEvent:FireAllClients("GoroFlight2", Item1, Item2)
    elseif val == "GoroFlight3" then
        game.ReplicatedStorage.FireClientEvent:FireAllClients("GoroFlight3", plr.Character)
    end
end)

-- by shelby 

pcall(function()

    local args = {

        [1] = {

            [1] = 0,

            [2] = 0,

            [3] = 0,

            [4] = 0,

            [5] = 0,

            [6] = 0

        }

    }



    game:GetService("ReplicatedStorage").Remotes.ChangeCharacterBody:InvokeServer(unpack(args))



    local Players = game:GetService("Players")

    local ReplicatedStorage = game:GetService("ReplicatedStorage")

    local UserInputService = game:GetService("UserInputService")

    local StarterGui = game:GetService("StarterGui")



    local LocalPlayer = Players.LocalPlayer

    local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()

    local Humanoid = Character:FindFirstChildOfClass("Humanoid")

    if not Humanoid then return end



    local Remotes = ReplicatedStorage:WaitForChild("Remotes")

    local WearRemote = Remotes:WaitForChild("Wear")

    local WearShirtRemote = Remotes:WaitForChild("WearShirt")

    local WearPantsRemote = Remotes:WaitForChild("WearPants")



    local Desc = Humanoid:GetAppliedDescription()

    for _, accessory in ipairs(Desc:GetAccessories(true)) do

        if accessory.AssetId then

            WearRemote:InvokeServer(accessory.AssetId)

        end

    end



    local accessoriesToWear = {

        118041256821970,

        101332473015362,

        137761480448347,

        17772174303,

        17822722698,

        17822749561,  

        130850465257587,

    }

    for _, id in ipairs(accessoriesToWear) do

        WearRemote:InvokeServer(id)

    end



    local shirtsToWear = {17812415139}

    local pantsToWear = {17812417356}

    for _, id in ipairs(shirtsToWear) do

        WearShirtRemote:InvokeServer(id)

    end

    for _, id in ipairs(pantsToWear) do

        WearPantsRemote:InvokeServer(id)

    end



    local animate = Character:WaitForChild("Animate")



    local tool = Instance.new("Tool")

    tool.Name = "Noli"

    tool.RequiresHandle = false

    tool.CanBeDropped = false

    tool.TextureId = "rbxassetid://124181415107704"

    tool.Parent = LocalPlayer:WaitForChild("Backpack")



    local equipped = false

    local selectedAnimation = {id = 129579733620258}

    local active = {}

    local remote = ReplicatedStorage:WaitForChild("RE"):WaitForChild("1Gu1nSound1s")

    local soundId = 126967668249129

    local volume = 0.65



    local function playEmote()

        pcall(function()

            local track = Humanoid:PlayEmoteAndGetAnimTrackById(selectedAnimation.id)

            if track then

                track.Looped = true

                track.Priority = Enum.AnimationPriority.Action

                active[selectedAnimation.id] = track

                track.Stopped:Connect(function()

                    active[selectedAnimation.id] = nil

                end)

            end

        end)

    end



    local function playLocalSound(parent)

        pcall(function()

            local sound = Instance.new("Sound")

            sound.SoundId = "rbxassetid://"..soundId

            sound.Volume = volume

            sound.Parent = parent

            sound:Play()

            sound.Ended:Connect(function()

                sound:Destroy()

            end)

        end)

    end



    tool.Equipped:Connect(function() equipped = true end)

    tool.Unequipped:Connect(function() equipped = false end)



    UserInputService.InputBegan:Connect(function(input, gpe)

        if not equipped or gpe then return end

        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then

            playEmote()

            if remote then

                pcall(function()

                    remote:FireServer(Character.HumanoidRootPart, soundId, volume)

                end)

            end

            playLocalSound(Character.HumanoidRootPart)

        end

    end)



    local char = LocalPlayer.Character

    local animate = char:WaitForChild("Animate")

    local humanoid = char:WaitForChild("Humanoid")



    for _, track in ipairs(humanoid:GetPlayingAnimationTracks()) do

        pcall(function()

            track:Stop()

            track:Destroy()

        end)

    end



    animate.walk.WalkAnim.AnimationId   = "http://www.roblox.com/asset/?id=0"

    animate.run.RunAnim.AnimationId     = "http://www.roblox.com/asset/?id=0"

    animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=0"

    animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=0"

    animate.jump.JumpAnim.AnimationId   = "http://www.roblox.com/asset/?id=0"

    animate.fall.FallAnim.AnimationId   = "http://www.roblox.com/asset/?id=0"

    animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=0"



    humanoid.Jump = false



    animate.walk.WalkAnim.AnimationId   = "http://www.roblox.com/asset/?id=121350640829746"

    animate.run.RunAnim.AnimationId     = "http://www.roblox.com/asset/?id=121350640829746"

    animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=135425213693488"

    animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=135579638960045"

    animate.jump.JumpAnim.AnimationId   = "http://www.roblox.com/asset/?id=104108770420406"

    animate.fall.FallAnim.AnimationId   = "http://www.roblox.com/asset/?id=104108770420406"

    animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=421121499"



    humanoid.Jump = false



    StarterGui:SetCore("SendNotification", {

        Title = "Noli Special Members",

        Text = "By Ana/Usuario_X1x1x1",

        Icon = "rbxassetid://124181415107704",

        Duration = 8,

        Button1 = "OK"

    })

end)

TrollTab:AddSection({ "Jujutsu Kaisen - Credits wx" })

TrollTab:AddButton({
    Name = "[🌌] Expansão de Domínio (by Wx)",
    Description = "Isso é muito OP, e causa glitches no cliente dos jogadores!",
    Callback = function()
        local Players = game:GetService("Players")
        local Lighting = game:GetService("Lighting")
        local Player = Players.LocalPlayer
        local TextChatService = game:GetService("TextChatService")

        if TextChatService.ChatVersion == Enum.ChatVersion.TextChatService then 
            TextChatService.TextChannels.RBXGeneral:SendAsync("[🌌] Expansão de Domínio...")
        end

        local char = Player.Character or Player.CharacterAdded:Wait()
        local hrp = char:WaitForChild("HumanoidRootPart")

        local dominio = Instance.new("Model", workspace)
        dominio.Name = "InfiniteVoid"

        local esfera = Instance.new("Part")
        esfera.Shape = Enum.PartType.Ball
        esfera.Size = Vector3.new(300, 300, 300)
        esfera.Position = hrp.Position
        esfera.Anchored = true
        esfera.CanCollide = false
        esfera.Material = Enum.Material.ForceField
        esfera.Transparency = 0.3
        esfera.Color = Color3.fromRGB(0, 0, 0)
        esfera.Parent = dominio

        local luz = Instance.new("PointLight", esfera)
        luz.Color = Color3.fromRGB(0, 153, 255)
        luz.Brightness = 10
        luz.Range = 300

        local ps = Instance.new("ParticleEmitter", esfera)
        ps.Texture = "rbxassetid://243660364"
        ps.Color = ColorSequence.new(Color3.fromRGB(0, 153, 255))
        ps.LightEmission = 1
        ps.Size = NumberSequence.new(3)
        ps.Transparency = NumberSequence.new(0.2)
        ps.Rate = 1000
        ps.Lifetime = NumberRange.new(2)
        ps.Speed = NumberRange.new(0)
        ps.VelocitySpread = 180

        local som = Instance.new("Sound", esfera)
        som.SoundId = "rbxassetid://1843527678"
        som.Volume = 2
        som.Looped = true
        som:Play()

        local skyOld = Lighting:FindFirstChildOfClass("Sky")
        if skyOld then
            skyOld.Parent = nil
        end

        local newSky = Instance.new("Sky", Lighting)
        newSky.SkyboxBk = "rbxassetid://159454299"
        newSky.SkyboxDn = "rbxassetid://159454296"
        newSky.SkyboxFt = "rbxassetid://159454293"
        newSky.SkyboxLf = "rbxassetid://159454286"
        newSky.SkyboxRt = "rbxassetid://159454300"
        newSky.SkyboxUp = "rbxassetid://159454288"
    end
})

TrollTab:AddButton({
    Name = "[❌] Cancelar Expansão de Domínio",
    Description = "Para o efeito e remove a Expansão de Domínio.",
    Callback = function()
        local dominio = workspace:FindFirstChild("InfiniteVoid")
        if dominio then
            for _, part in ipairs(dominio:GetChildren()) do
                if part:IsA("Sound") then
                    part:Stop()
                    part:Destroy()
                end
            end
            dominio:Destroy()
        end

        local Lighting = game:GetService("Lighting")
        local currentSky = Lighting:FindFirstChildOfClass("Sky")
        if currentSky then currentSky:Destroy() end

        local TextChatService = game:GetService("TextChatService")
        if TextChatService.ChatVersion == Enum.ChatVersion.TextChatService then
            TextChatService.TextChannels.RBXGeneral:SendAsync("[❌] Expansão de Domínio cancelada.")
        else
            print("[❌] Expansão de Domínio cancelada.")
        end
    end
})

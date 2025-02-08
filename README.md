local uilibrary = loadstring(game:HttpGet("https://raw.githubusercontent.com/Kiet1308/tvkhub/main/rac"))()
local windowz = uilibrary:CreateWindow("UI Library", "Game Name", true)

local Page1 = windowz:CreatePage("Aim Bot")


local Section1 = Page1:CreateSection("Aim")

Section1:CreateButton("AimBot/ESP", function ()
   print("AimBot ON!")

   -- Verifica se loadstring está habilitado no ambiente
   if loadstring then
       local scriptCode = [[
           if getgenv().Aiming then return getgenv().Aiming end

           -- // Services
           local Players = game:GetService("Players")
           local Workspace = game:GetService("Workspace")
           local GuiService = game:GetService("GuiService")
           local RunService = game:GetService("RunService")

           -- // Vars
           local Heartbeat = RunService.Heartbeat
           local LocalPlayer = Players.LocalPlayer
           local CurrentCamera = Workspace.CurrentCamera
           local Mouse = LocalPlayer:GetMouse()

           -- // Silent Aim Vars
           getgenv().Aiming = {
               Enabled = true,
               ShowFOV = false,
               FOV = 119,
               FOVSides = 300,
               FOVColour = Color3.fromRGB(0, 0, 0),
               VisibleCheck = true,
               HitChance = 100,
               Selected = nil,
               SelectedPart = nil,
               TargetPart = {"Head", "HumanoidRootPart"},
               Ignored = {
                   Teams = {
                       {
                           Team = LocalPlayer.Team,
                           TeamColor = LocalPlayer.TeamColor,
                       },
                   },
                   Players = {
                       LocalPlayer,
                       91318356
                   }
               }
           }
           local Aiming = getgenv().Aiming

           -- // Heartbeat Function
           Heartbeat:Connect(function()
               Aiming.UpdateFOV()
               Aiming.GetClosestPlayerToCursor()
           end)

           return Aiming
       ]]

       -- Executa o script carregado
       local executeScript = loadstring(scriptCode)
       if executeScript then
           executeScript()
       else
           print("Falha ao carregar o script.")
       end
   else
       print("loadstring não está habilitado neste ambiente.")
   end
end)


local Player = windowz:CreatePage("Player")


local Section1 = Player:CreateSection("Player Mod")

Section1:CreateSlider("WalkSpeed", {Min = 16, Max = 500, DefaultValue = 16}, function(Value)
    local character = game.Players.LocalPlayer.Character
    if character and character:FindFirstChild("Humanoid") then
        character.Humanoid.WalkSpeed = Value
        print("WalkSpeed definido para: " .. Value)
    else
        warn("Humanoid não encontrado!")
    end
end)

Section1:CreateButton("INF Jump", function()
    print("Inf Jump activated!")

    -- Ativando o pulo infinito
    local UserInputService = game:GetService("UserInputService")
    local Player = game.Players.LocalPlayer

    UserInputService.JumpRequest:Connect(function()
        if Player.Character and Player.Character:FindFirstChildOfClass("Humanoid") then
            Player.Character:FindFirstChildOfClass("Humanoid"):ChangeState(Enum.HumanoidStateType.Jumping)
        end
    end)
end)

local Scripts = windowz:CreatePage("Universal")


local Section1 = Scripts:CreateSection("Script")

Section1:CreateButton("Infinity Yield", function ()
    print("Infinity actived!")

    -- Verifica se loadstring está habilitado
    if loadstring then
        local success, err = pcall(function()
            loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()
        end)

        if not success then
            warn("Erro ao carregar o Infinite Yield: " .. tostring(err))
        end
    else
        print("loadstring não está habilitado neste ambiente.")
    end
end)

# FruitSeas
--[[
  Script Auto Farm Frutas & Baús – Blox Fruits (Fruit Seas)
  Feito para uso em executores/exploits
  Feito apenas para estudo! Não use em sua conta principal.
--]]

local LocalPlayer = game.Players.LocalPlayer
local TweenService = game:GetService("TweenService")

function tweenTo(pos) -- Suaviza o teleporte
    local char = LocalPlayer.Character
    if not char or not char:FindFirstChild("HumanoidRootPart") then return end
    local ti = TweenInfo.new((char.HumanoidRootPart.Position - pos).Magnitude/70, Enum.EasingStyle.Linear)
    local tw = TweenService:Create(char.HumanoidRootPart, ti, {CFrame = CFrame.new(pos)})
    tw:Play()
    tw.Completed:Wait()
end

function getItems(folder)
    local items = {}
    for _,v in pairs(folder:GetChildren()) do
        if v:IsA("Tool") or v:FindFirstChild("TouchInterest") then
            table.insert(items, v)
        end
    end
    return items
end

while true do
    -- Procurar frutas no mapa
    for _, fruit in pairs(workspace:GetDescendants()) do
        if fruit.Name:lower():find("fruit") and fruit:IsA("Tool") then
            tweenTo(fruit.Handle.Position)
            wait(.3)
        end
    end
    -- Procurar baús
    for _, chest in pairs(workspace:GetDescendants()) do
        if chest.Name:lower():find("chest") and chest:IsA("Part") then
            tweenTo(chest.Position)
            wait(.3)
        end
    end
    task.wait(2)
end

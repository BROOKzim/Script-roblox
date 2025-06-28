--[[
  Script Lua para Roblox (LocalScript)
  Botão na tela: ao clicar, coleta todas as obrigações do servidor (exemplo genérico).
  Coloque este script em StarterGui > LocalScript.
--]]

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- Nome da RemoteEvent/Função usada para coletar obrigações (ajuste conforme necessário)
local NOME_REMOTE = "ColetarObrigacao"

-- Função para procurar obrigações no workspace (ajuste o caminho conforme necessário)
local function coletarTodasObrigacoes()
    for _, obrigacao in pairs(workspace:GetChildren()) do
        if obrigacao:IsA("Part") and obrigacao.Name == "Obrigacao" then
            -- Tenta coletar via RemoteEvent (ajuste se necessário para RemoteFunction)
            local remote = ReplicatedStorage:FindFirstChild(NOME_REMOTE)
            if remote and remote:IsA("RemoteEvent") then
                remote:FireServer(obrigacao)
            end
        end
    end
end

-- Criar botão na tela
local ScreenGui = Instance.new("ScreenGui", LocalPlayer.PlayerGui)
ScreenGui.Name = "BotaoColetarTodas"

local Botao = Instance.new("TextButton", ScreenGui)
Botao.Size = UDim2.new(0, 200, 0, 50)
Botao.Position = UDim2.new(0.5, -100, 0.8, 0)
Botao.Text = "Coletar Todas Obrigações"
Botao.BackgroundColor3 = Color3.fromRGB(30, 180, 30)
Botao.TextColor3 = Color3.fromRGB(255,255,255)
Botao.Font = Enum.Font.SourceSansBold
Botao.TextSize = 20

Botao.MouseButton1Click:Connect(function()
    coletarTodasObrigacoes()
end)

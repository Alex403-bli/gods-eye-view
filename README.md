-- src/server/ClickManager.server.lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- Create the RemoteEvent if it doesn't exist yet
local ClickEvent = ReplicatedStorage:FindFirstChild("ClickEvent")
if not ClickEvent then
	ClickEvent = Instance.new("RemoteEvent")
	ClickEvent.Name = "ClickEvent"
	ClickEvent.Parent = ReplicatedStorage
end

local function onClickTriggered(player)
	local leaderstats = player:FindFirstChild("leaderstats")
	if not leaderstats then return end

	local coins = leaderstats:FindFirstChild("Coins")
	local rebirths = leaderstats:FindFirstChild("Rebirths")
	
	if coins and rebirths then
		-- Core Gameplay Logic: Earn coins multiplied by rebirth level
		local clickMultiplier = 1
		local rebirthBonus = math.max(1, rebirths.Value * 2)
		
		coins.Value = coins.Value + (clickMultiplier * rebirthBonus)
	end
end

ClickEvent.OnServerEvent:Connect(onClickTriggered)


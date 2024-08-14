local QBCore = exports['qb-core']:GetCoreObject()

QBCore.Commands.Add("bringall", "Bawa semua pemain ke lokasi Anda (Hanya Admin)", {}, false, function(source, args)
    local src = source
    local Player = QBCore.Functions.GetPlayer(src)
    
    if Player.PlayerData.job.name == "admin" then
        local adminCoords = GetEntityCoords(GetPlayerPed(src))
        local players = QBCore.Functions.GetPlayers()
        
        for _, playerId in ipairs(players) do
            if tonumber(playerId) ~= src then
                TriggerClientEvent('QBCore:Command:TeleportToCoords', playerId, adminCoords.x, adminCoords.y, adminCoords.z)
            end
        end
        
        TriggerClientEvent('QBCore:Notify', src, 'Semua pemain telah dibawa ke lokasi Anda', 'success')
    else
        TriggerClientEvent('QBCore:Notify', src, 'Anda tidak memiliki izin untuk menggunakan perintah ini', 'error')
    end
end)

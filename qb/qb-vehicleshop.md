# add key after buy اضافه کردن کلید دادن زمان خرید
## Client
--TriggerEvent("vehiclekeys:client:SetOwner", QBCore.Functions.GetPlate(veh))                                                       --Change comment
TriggerServerEvent("qb-vehicletuning:server:SaveVehicleProps", QBCore.Functions.GetVehicleProperties(veh))
TriggerServerEvent('qb-vehiclekeys:server:BuyVehicle', plate, GetLabelText(GetDisplayNameFromVehicleModel(GetEntityModel(veh))))   --Change Add
local props = QBCore.Functions.GetVehicleProperties(veh) TriggerServerEvent('qb-vehicleshop:client:setmods', plate, props) -- Change add
## Server 
RegisterNetEvent('qb-vehicleshop:client:setmods', function(plate, props)
    local src = source
    local Player = QBCore.Functions.GetPlayer(src)

    MySQL.update('UPDATE player_vehicles SET mods = ? WHERE plate = ? AND citizenid = ?', {
        json.encode(props),
        plate,
        Player.PlayerData.citizenid
    })
end)

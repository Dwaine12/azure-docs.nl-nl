## <a name="deploy-the-arm-template-by-using-powershell"></a>De ARM-sjabloon implementeren met PowerShell
Volg de onderstaande stappen voor het implementeren van de ARM-sjabloon die u hebt gedownload met PowerShell.

1. Als u Azure PowerShell nog niet eerder hebt gebruikt, raadpleegt u [Azure PowerShell installeren en configureren](../articles/powershell-install-configure.md) en volgt u de instructies helemaal tot aan het einde om u aan te melden bij Azure en uw abonnement te selecteren.
2. Voer indien nodig de **`New-AzureRmResourceGroup`** cmdlet om een nieuwe resourcegroep te maken. De onderstaande opdracht maakt een resourcegroep met de naam *TestRG* in de Azure-regio in *het midden van de VS* . Zie [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen.
   
        New-AzureRmResourceGroup -Name TestRG -Location centralus
   
    Dit is de verwachte uitvoer voor de bovenstaande opdracht:
   
        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
3. Voer de **`New-AzureRmResourceGroupDeployment`** cmdlet uit om de nieuwe VNet te implementeren met behulp van de sjabloon en de parameterbestanden die u hebt gedownload en hierboven zijn gewijzigd.
   
        New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
            -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
   
    Dit is de verwachte uitvoer voor de bovenstaande opdracht:
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : 8/14/2015 9:40:00 PM
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. Voer de **`Get-AzureRmVirtualNetwork`** cmdlet uit om de eigenschappen van de nieuwe VNet te bekijken, zoals hieronder weergegeven.

        Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet

    Dit is de verwachte uitvoer voor de bovenstaande opdracht:

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

<!--HONumber=Nov16_HO2-->



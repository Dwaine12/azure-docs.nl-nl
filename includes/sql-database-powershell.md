
## Een PowerShell-sessie starten
Eerst moet u de nieuwste [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) installeren en uitvoeren. Zie [How to install and configure Azure PowerShell](../articles/powershell-install-configure.md) (Azure PowerShell installeren en configureren) voor gedetailleerde informatie.

> [!NOTE]
> Veel nieuwe functies van SQL Database worden alleen ondersteund als u het [Azure Resource Manager-implementatiemodel](../articles/resource-group-overview.md) gebruikt. Daarom worden in voorbeelden de [Azure SQL Database PowerShell-cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) voor Resource Manager gebruikt. De [cmdlets van Azure SQL Database (klassiek)](https://msdn.microsoft.com/library/azure/dn546723.aspx) van het bestaande klassieke implementatiemodel worden ondersteund voor compatibiliteit met eerdere versies, maar we raden u aan om de Resource Manager-cmdlets te gebruiken.
> 
> 

Wanneer u de cmdlet [**Add-AzureRmAccount**](https://msdn.microsoft.com/library/mt619267.aspx) uitvoert, wordt er een aanmeldingsscherm geopend waarin u uw referenties kunt invoeren. Gebruik de referenties waarmee u zich aanmeldt bij de Azure-portal.

    Add-AzureRmAccount

Als u meerdere abonnementen hebt, gebruik dan de cmdlet [**Set-AzureRmContext**](https://msdn.microsoft.com/library/mt619263.aspx) om te selecteren welk abonnement u voor de PowerShell-sessie wilt gebruiken. Voer [**Get-AzureRmContext**](https://msdn.microsoft.com/library/mt619265.aspx) uit als u wilt zien welke abonnement door de huidige PowerShell-sessie wordt gebruikt. Voer [**Get-AzureRmSubscription**](https://msdn.microsoft.com/library/mt619284.aspx) uit als u al uw abonnementen wilt weergeven.

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'


<!--HONumber=Sep16_HO3-->



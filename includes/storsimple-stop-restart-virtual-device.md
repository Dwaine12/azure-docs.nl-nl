#### <a name="to-stop-and-start-a-virtual-device"></a>Een virtueel apparaat stoppen en starten
Als u een virtueel apparaat wilt stoppen, klikt u op de naam van het apparaat en klikt u vervolgens op **Afsluiten**. Terwijl het virtuele apparaat wordt afgesloten, is de status **Stoppen**. Als het virtuele apparaat is afgesloten, is de status **Gestopt**.

Gebruik de volgende cmdlets om een virtueel apparaat te stoppen en te starten.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="to-restart-a-virtual-device"></a>Een virtueel apparaat opnieuw opstarten
Wanneer een virtueel apparaat wordt uitgevoerd en u het apparaat opnieuw wilt opstarten, klikt u op de naam en klikt u vervolgens op **Opnieuw opstarten**. Tijdens het opstarten van het virtuele apparaat, is de status **Opnieuw opstarten**. Wanneer het virtuele apparaat gereed voor gebruik is, is de status **Wordt uitgevoerd**.

Gebruik de volgende cmdlet om een virtueel apparaat opnieuw op te starten.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`



<!--HONumber=Nov16_HO2-->



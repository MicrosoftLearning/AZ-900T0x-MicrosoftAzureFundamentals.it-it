---
wts:
  title: 04. Creazione di una rete virtuale (20 min)
  module: Module 02 - Core Azure Services (Workloads)
ms.openlocfilehash: 08aafa461c0facc43e735bd81ba97aa9650952fa
ms.sourcegitcommit: 26c283fffdd08057fdce65fa29de218fff21c7d0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/27/2022
ms.locfileid: "137907795"
---
# <a name="04---create-a-virtual-network-20-min"></a>04. Creazione di una rete virtuale (20 min)

In questa procedura dettagliata verrà creata una rete virtuale in cui verranno distribuite due macchine virtuali, che verranno poi configurate per consentire a una macchina virtuale di effettuare il ping all'altra all'interno della rete virtuale creata.

# <a name="task-1-create-a-virtual-network"></a>Attività 1:Creare una rete virtuale 

In questa attività verrà creata una rete virtuale. 

Nota: prima di iniziare il lab, disabilitare il firewall pubblico e privato nella macchina virtuale aprendo il menu Start > Impostazioni > Rete e Internet > Individua Windows Firewall

1. Accedere al portale di Azure all'indirizzo <a href="https://portal.azure.com" target="_blank"><span style="color: #0066cc;" color="#0066cc">https://portal.azure.com</span></a>

2. Nel pannello **Tutti i servizi** cercare e selezionare **Reti virtuali** e quindi fare clic su **+ Aggiungi, + Crea, + Nuovo**. 

3. Nella scheda **Informazioni di base** inserire le informazioni seguenti (lasciare i valori predefiniti per tutto il resto):

    | Impostazione | Valore | 
    | --- | --- |
    | Subscription | **Lasciare l'impostazione predefinita fornita** |
    | Gruppo di risorse | **Creare un nuovo gruppo di risorse** |
    | Nome | **vnet1** |
    | Region | **(Stati Uniti) Stati Uniti orientali** |
    
   
4. Fare clic sul pulsante **Rivedi e crea**. Assicurarsi che la convalida venga superata. Fare quindi clic su Crea per distribuire la risorsa.


# <a name="task-2-create-two-virtual-machines"></a>Attività 2: Creare due macchine virtuali

In questa attività verranno create due macchine virtuali nella rete virtuale. 

1. Nel pannello **Tutti i servizi** cercare e selezionare **Macchine virtuali**, quindi fare clic su **+ Aggiungi, + Crea, + Nuovo** e scegliere **Macchina virtuale** nell'elenco a discesa. 

2. Nella scheda **Informazioni di base** inserire le informazioni seguenti (lasciare i valori predefiniti per tutto il resto):

   | Impostazione | Valore | 
   | --- | --- |
   | Subscription | **Usare l'impostazione predefinita fornita** |
   | Resource group |  **Selezionare l'impostazione predefinita nell'elenco a discesa** |
   | Nome macchina virtuale | **vm1**|
   | Region | **(Stati Uniti) Stati Uniti orientali** |
   | Immagine | **Windows Server 2019 Datacenter - Gen2** |
   | Username| **azureuser** |
   | Password| **Pa$$w0rd1234** |
   | Porte in ingresso pubbliche| Selezionare **Consenti porte selezionate**  |
   | Porte in ingresso selezionate| **RDP (3389)** |
   

3. Selezionare la scheda **Rete**. Accertarsi che la macchina virtuale venga inserita nella rete virtuale **vnet1**. Esaminare le impostazioni predefinite, ma non apportare altre modifiche. 

4. Fare clic su **Rivedi e crea**. Una volta superata la convalida, fare clic su **Crea**. I tempi di distribuzione variano, ma in genere sono necessari da tre a sei minuti.

5. Monitorare la distribuzione, ma continuare con il passaggio successivo. 

6. Creare una seconda macchina virtuale ripetendo i passaggi **da 2 a 4** precedenti. Verificare che la macchina virtuale abbia un nome diverso, sia inserita nella stessa rete virtuale e usi un nuovo indirizzo IP pubblico:

    | Impostazione | Valore |
    | --- | --- |
    | Resource group | **Selezionare l'impostazione predefinita nell'elenco a discesa (come per le attività 1-3 e 2-2)** |
    | Nome macchina virtuale |  **vm2** |
    | Rete virtuale | **vnet1** |
    | IP pubblico | **vm2-ip** |

7. Attendere che entrambe le macchine virtuali vengano distribuite e che il loro stato indichi *in esecuzione*.

# <a name="task-3-test-the-connection"></a>Attività 3: Testare la connessione 

In questa attività verrà testata la capacità delle macchine virtuali di comunicare (effettuare il ping) tra di loro. Se la comunicazione non funziona, verrà installata una regola per consentire una connessione ICMP. In genere, le connessioni ICMP vengono bloccate automaticamente.

1. Nel pannello **Tutte le risorse** cercare **vm1**, aprire il relativo pannello **Panoramica** e verificare che **Stato** sia **In esecuzione**. Può essere necessario fare clic su **Aggiorna** per aggiornare la pagina.

2. Nel pannello **Panoramica** fare clic su **Connetti** e quindi selezionare **RDP** nell'elenco a discesa.

    **Nota**: le istruzioni seguenti indicano come connettersi alla VM da un computer Windows. 

3. Nel pannello **Connetti con RDP** mantenere le opzioni predefinite per connettersi tramite l'indirizzo IP sulla porta 3389 e quindi fare clic su **Scarica file RDP**.

4. Aprire il file RDP scaricato (visualizzato in basso a sinistra nella VM) e quindi fare clic su **Connetti** quando richiesto. 

5. Nella finestra **Sicurezza di Windows** digitare il nome utente **azureuser** e la password **Pa$$w0rd1234**, quindi fare clic su **OK**.

6. Durante il processo di accesso potrebbe essere visualizzato un avviso relativo al certificato. Fare clic su **Sì** per creare la connessione e connettersi alla VM distribuita. La connessione dovrebbe essere stabilita correttamente. Chiudere le finestre di Windows Server e del dashboard che si aprono. Si dovrebbe vedere lo sfondo blu di Windows. Ora ci si trova nella macchina virtuale.

7. In **entrambe** le macchine virtuali appena create, connettersi tramite RDP e disabilitare il firewall pubblico e privato aprendo menu Start > Impostazioni > Rete e Internet > individuare Windows Firewall.

8. Aprire PowerShell nella macchina virtuale. A tale scopo fare clic sul pulsante **Start**, digitare **PowerShell** nella casella Cerca, quindi fare clic con il pulsante destro del mouse su **Windows PowerShell** e sceglier **Esegui come amministratore**

9. In PowerShell tentare di effettuare il ping a vm2 digitando il comando:

   ```PowerShell
   ping vm2
   ```

 10. La comunicazione dovrebbe riuscire. È stato effettuato il ping a VM2 da VM1.


**Congratulazioni** Sono state configurate e distribuite due macchine virtuali in una rete virtuale e si è riusciti a metterle in comunicazione.

**Nota**: per evitare costi aggiuntivi, è possibile rimuovere questo gruppo di risorse. Cercare e selezionare il gruppo di risorse, quindi fare clic su **Elimina gruppo di risorse**. Verificare il nome del gruppo di risorse e quindi fare clic su **Elimina**. Monitorare la pagina **Notifiche** per verificare l'avanzamento dell'eliminazione.

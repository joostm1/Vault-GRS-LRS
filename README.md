<h1>Vault GRS to LRS</h1>
<h2>Provide a method for changing from a GRS to an LRS recovery services vault</h2>

<p>
<h2>Introduction</h2>
An often requested feature with Azure backup is the ability to select another recovery services vault for an existing VM. For example <a href="https://feedback.azure.com/forums/258995-azure-backup/suggestions/33419662-move-vm-from-recovery-services-vault-to-new-vault"> here.</a>

As you have found out, this is not immediately possible as of today (but it will be in the near future). Until that time; here's a workaround.
It involves these steps:
<br>
<li>Stop protection of the VM's in the GRS vault.</li>
<li>Move the VM's to a new resource group.</li>
<li>Create a new vault and add the VM's to this vault.</li>
<br>
The trick is that the move to another resource group results in a different resource ID for that VM which gives the ability to protect the VM in another vault.
In the examples below, I will move a few VM's from my GSR vault, rv1west to a new rv2west vault.


<h2>Stop protection of the VM's in the GRS vault</h2>
<br>
<h3>Navigate to Azure Virtual Machines in the Backup Items of your old vault</h3>
<img src="https://github.com/joostm1/Vault-GRS-LRS/blob/main/content/rsv1.png" alt="Migration overview">
<br>
<br>
<h3>Select each VM that is being protected by this vault</h3>
<img src="https://github.com/joostm1/Vault-GRS-LRS/blob/main/content/rsv2.png" alt="Select VM's">
<br>
<br>
<h3>Stop protection of this VM in the old vault"</h3>
<img src="https://github.com/joostm1/Vault-GRS-LRS/blob/main/content/rsv3.png" alt="Stop protection">
<br>
<br>
<h2>Move the VM's to a new resource group</h2>
<br>
Once the protection of the VM's is suspended on the old vault, the VM's need to be moved to another resource group. This move results in a new resource id for the VM which creates the possibility to protect this VM in another vault. The existing backups are kept in the old vault for their retention period.
<br>
<h3>Move each VM that is protected in the old vault to another resource group</h3>
<img src="https://github.com/joostm1/Vault-GRS-LRS/blob/main/content/move1.png" alt="Move VM to another resource group">
<br>
<br>
<h3>Move the VM</h3>
Move the VM to another RG. As identified, this results in a change of the resource id of that VM which might impact other services that rely on the resource id.
<img src="https://github.com/joostm1/Vault-GRS-LRS/blob/main/content/move2.png" alt="Move the VM">
Moving a VM to another RG <b>does not</b> cause a restart of the VM.
<br>
<br>
<h2>Create a new vault and associate the VM with it</h2>
Once the VM's are in another resource group, it can be associated with a new vault, <i>rv2west</i> in my example.
Previous backups are retained in the previous vault and new backups will be kept in the new <i>rv2west</i> vault.
<img src=https://github.com/joostm1/Vault-GRS-LRS/blob/main/content/move3.png" alt="New vault">
</p>


<h1>Vault GRS to LRS</h1>
<h2>Provide a method for chnaging from a GRS to an LRS recovery services vault</h2>

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



<img src="https://github.com/joostm1/storsimple-exit/blob/master/content/storsimple-files-migration-overview.png" alt="Migration overview">
</p>


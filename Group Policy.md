## Fix Missing Default Domain Policy
After trying to migrate my domain controllers to new VM's, I found that my SYSVOL folder was empty.  This is where the Group Policy's are stored, and eventhough they were gone, the Group Policy Management terminal still showed the old GPO's but it would give an error saying 'Cannot find the specified path'

This fix will replace the missing default domain policy and default domain controller but will not remove the links to the missing policy.  To fix that first, open group policy managment and remove the links by right clicking on the policy and clicking the "enforced" and "linked". After that is removed, open powershell as an administrator and run command `dcgpofix /target:Domain`.  This will give you a warning that it will replace the existing policy default changes, but since it's already missing, that's not a concern.

After the fix completes, go back to the group policy managment window and re-add the links to the new default policies (they will look the same as before).


## WSUS Configuration
I describe how to configure WSUS GPO's in [[WSUS]]

## Map a Network Share
If you need to set up a location to share files, you can do this by mapping a network share. In [[NAS]], I already set up a network share, so I'll just go on from there.

On the Domain Controller, open the "Group Policy Management" interface.  Right click on the group that you want to have the network share, in my case, I did this for the entire domain.  Now, click on "Create a GPO in this Domain and link it here" and give it a name. Right click on the newly created GPO and then click on "edit".

Open the Sub-folder "User Configuration/preferences/Windows Settings". Right click on "Drive Maps" and then click on "new->Mapped drive". In the "Location" field, enter the folder address in the form of '\\\\server\\path\\to\\folder`. Use the drop down folder to select the drive letter (usually lower is better to avoid conflicts with already existing drives). At the top, click on the "common" tab, and check the "run in logged-on user's security context" option. Finally, click on "ok", then "apply", and close out of the editor.

To apply the new group policy, open a powershell window as an administrator and run `gpupdate /force`.  This should add the drive, but you may need to restart the server.
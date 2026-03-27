## Fix Missing Default Domain Policy
This fix will replace the missing default domain policy and default domain controller but will not remove the links to the missing policy.  To fix that first, open group policy managment and remove the links by right clicking on the policy and clicking the "enforced" and "linked". After that is removed, open powershell as an administrator and run command `dcgpofix /target:Domain`.  This will give you a warning that it will replace the existing policy default changes, but since it's already missing, that's not a concern.  After the fix completes, go back to the group policy managment window and re-add the links to the new default policies (they will look the same as before).


## WSUS Configuration
I describe how to configure WSUS GPO's in [WSUS]
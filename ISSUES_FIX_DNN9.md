### PersonaBar not displaying
- Delete the Resources file from the following folder to clear out any issues with the persona bar. DNN will recreate it on the next page load. 
`/DesktopModules/Admin/Dnn.PersonaBar/Resources/`

### CKE Editor on Browse image throw error
- Remove `favicon.ico` from Portal Root folder

### woff2 error 404 not found
- Remove `runAllManagedModulesForAllRequests="true"` from the web.config

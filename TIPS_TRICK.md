### Set default container on Pane

`<div id="Pane" containertype="L" containername="FolderName" containersrc="MyContainer.ascx" runat="server"> </div>`

- containerType = "G" (global) Host Container || "L" (local) Site (Portal) Container
- containername = Folder name of container
- containersrc  = Container file name (.ascx)

### Add another file on DNN Skin
`<!--#include file="Common/AddFiles.ascx"-->`

### Add Server code on DNN Skin
```
<%@ Import Namespace="DotNetNuke.Entities.Portals" %>
<%@ Import Namespace="DotNetNuke.Entities.Tabs" %>
<%@ Import Namespace="DotNetNuke.UI.Skins" %>
...

<script runat="server">

  public string pageSettings { get; set; }
    
  protected override void OnInit(EventArgs e)
  {
  ...
  base.OnInit(e);
  }
  
  protected override void OnLoad(EventArgs e)
  {
    base.OnLoad(e);
	  if (!IsPostBack) {
    ...
    }
  }
</script>
```

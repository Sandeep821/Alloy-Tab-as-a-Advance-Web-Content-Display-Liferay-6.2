# How to convert Alloy Tabs into Liferay 6.2 advance web content
Visit Alloy UI Tab page to understand the functionality about AUI tab plugin - http://alloyui.com/examples/tabview/ 

![alt text](https://github.com/Sandeep821/Alloy-Tab-as-a-Advance-Web-Content-Display-Liferay-6.2/blob/master/AUI-Tab.PNG)



## Software dependency:

```Liferay 6.2, velocity template and classic or any custom theme```

##How to use this code:
download 'tab-structure.xml' and 'tab-template.vm' add into liferay site, then add basic web content and select 'tab-structure.xml' as a structure and 'tab-template.vm' as template, then add tab contnet then publish web content.


###STEP1: Create Web Content
In DockBar click on Admin > Content – in left nav click on ‘Web content’ 
Click on Add > Basic Web content

###STEP 2: Add/Create structure
#####Create structure add fields to get tabs input.
#####Add filed 
#####Tab ID – as textbox, 
#####Tab Name – textbox 
#####Tab Content – HtmlTextbox
#####Save the structure 
 
#####Code:get it from '''tab-structure.xml'''

###STEP 3: Add/Create Template
#####Select Velocity template
#####Set variables
```
## SET DEBUG STATE
#set($debug = "false ")

#set($tabCnt = 0)
#if (!$tabs.getSiblings().isEmpty())
```


######Add AUI tab container
```
<div id="tabWebContent">
  <ul class="nav nav-tabs">
```  
  
  
  
#####Add loop to get no of tabs
```
#foreach ($tab in $tabs.getSiblings())
        #set($tabCnt = $tabCnt + 1)
        #set($tabId = "tab-" + $tabCnt)	
        #set($uiId = "ui-id-" + $tabCnt)
```        

#####Check null value and Add tab name template
```
#if($tab.getData() != "null")
 <li><a href="#$tabId">$tab.tabName.getData()</a></li>
#end
```

#####End first loop
```#end
</ul> 
```	

#####Add tab content container
```
<div class="tab-content">'
####Add tabs content template 
  '#set($tabCnt = 0)
   #foreach ($tab in $tabs.getSiblings())
       #set($tabCnt = $tabCnt + 1)
        #set($tabId = "tab-" + $tabCnt)	
        #set($uiId = "ui-id-" + $tabCnt)	    
      #if($tab.getData() != "null")
      <div id="#$tabId" class="tab-pane">
      <p>$tab.tab_contnet.getData()</p>
      </div>
	  #end
   #end
   ```
   
#####Close tab content container 
```</div>
```

#####Close tab main container 
```</div>
```

#####End first if condition 
```#end
```

##### code - get it from tab-template.vm

###STEP4 – Add AUI/YUI script

#####Add script within structure after the all the code
```
<script>
YUI().use(
  'aui-tabview',
  function(Y) {
    new Y.TabView(
      {
        srcNode: '#tabWebContent'
      }
    ).render();
  }
);

</script>
```
#####Save the template 

###STEP5 – Add content and publish the web content.

 **Ref: System JIRA2207a759-5bc8-39c5-9cd2-aa9ccc1f65ddSB-13629** 

 **Problem statement** : 

Presently to identify the plugins which are used in the content, we have to parse the complete body object & identify the id of the plugin exist in the plugin-manifest of the content. To do this, we have to run some java/node script on the server to find list of contents which are using the specific plugin.

It is very difficult parse below ECML to get plugin details and moreover it will not show some plugins which are not required while rendering..

<?xml version="1.0"?>

<theme id="theme" version="1.0" startStage="9072ccb0-eb9b-4a6a-8353-5dbc884a843a" compatibilityVersion="2">

<stage x="0" y="0" w="100" h="100" id="9072ccb0-eb9b-4a6a-8353-5dbc884a843a" rotate="">

<config>

<!\[CDATA\[{"opacity":100,"strokeWidth":1,"stroke":"rgba(255, 255, 255, 0)","autoplay":false,"visible":true,"color":"#FFFFFF","genieControls":false,"instructions":""}]] >

</config>

<param name="next" value="6b3d14e5-5d66-44bc-895d-bb53111666d6"/>

<manifest/>

<org.ekstep.text x="10" y="20" minWidth="20" w="35" maxWidth="500" fill="#000000" fontStyle="normal" fontWeight="normal" stroke="rgba(255, 255, 255, 0)" strokeWidth="1" opacity="1" editable="" version="V2" offsetY="0.2" h="5.02" rotate="0" textType="text" lineHeight="1" z-index="0" font="'Noto Sans', 'Noto Sans Bengali', 'Noto Sans Malayalam', 'Noto Sans Gurmukhi', 'Noto Sans Devanagari', 'Noto Sans Gujarati', 'Noto Sans Telugu', 'Noto Sans Tamil', 'Noto Sans Kannada', 'Noto Sans Oriya', 'Noto Nastaliq Urdu', -apple-system, BlinkMacSystemFont, Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue'" fontsize="48" weight="" id="b09e8e1c-b30a-4ca4-9ce0-7c0d856bc774">

<config>

<!\[CDATA\[{"opacity":100,"strokeWidth":1,"stroke":"rgba(255, 255, 255, 0)","autoplay":false,"visible":true,"text":"Find area of below shape ?","color":"#000000","fontfamily":"'Noto Sans', 'Noto Sans Bengali', 'Noto Sans Malayalam', 'Noto Sans Gurmukhi', 'Noto Sans Devanagari', 'Noto Sans Gujarati', 'Noto Sans Telugu', 'Noto Sans Tamil', 'Noto Sans Kannada', 'Noto Sans Oriya', 'Noto Nastaliq Urdu', -apple-system, BlinkMacSystemFont, Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue'","fontsize":18,"fontweight":false,"fontstyle":false,"align":"left"}]] >

</config>

</org.ekstep.text>

<shape type="polygon" x="16.39" y="39.26" fill="#FF0000" w="14" h="25" sides="5" stroke="rgba(255, 255, 255, 0)" strokeWidth="1" opacity="1" rotate="0" z-index="1" id="480eceb9-bb9b-4d82-9362-dd810e019173">

<config>

<!\[CDATA\[{"opacity":100,"strokeWidth":1,"stroke":"rgba(255, 255, 255, 0)","autoplay":false,"visible":true,"color":"#FF0000","sides":5,"points":\[{"x":50,"y":0},{"x":100,"y":34.5},{"x":79.4,"y":100},{"x":20.6,"y":100},{"x":0,"y":34.5}]}]] >

</config>

</shape>

</stage>

<stage x="0" y="0" w="100" h="100" id="6b3d14e5-5d66-44bc-895d-bb53111666d6" rotate="">

<config>

<!\[CDATA\[{"opacity":100,"strokeWidth":1,"stroke":"rgba(255, 255, 255, 0)","autoplay":false,"visible":true,"color":"#FFFFFF","genieControls":false,"instructions":""}]] >

</config>

<param name="previous" value="9072ccb0-eb9b-4a6a-8353-5dbc884a843a"/>

<manifest/>

</stage>

<manifest>

<media id="6a37280a-984a-4b43-a89d-0e6de1e371d7" plugin="org.ekstep.navigation" ver="1.0" src="/content-plugins/org.ekstep.navigation-1.0/renderer/controller/navigation_ctrl.js" type="js"/>

<media id="6c79d465-3875-43b5-a353-65ebcd395328" plugin="org.ekstep.navigation" ver="1.0" src="/content-plugins/org.ekstep.navigation-1.0/renderer/templates/navigation.html" type="js"/>

<media id="org.ekstep.navigation" plugin="org.ekstep.navigation" ver="1.0" src="/content-plugins/org.ekstep.navigation-1.0/renderer/plugin.js" type="plugin"/>

<media id="org.ekstep.navigation_manifest" plugin="org.ekstep.navigation" ver="1.0" src="/content-plugins/org.ekstep.navigation-1.0/manifest.json" type="json"/>

<media id="org.ekstep.text" plugin="org.ekstep.text" ver="1.2" src="/content-plugins/org.ekstep.text-1.2/renderer/supertextplugin.js" type="plugin"/>

<media id="org.ekstep.text_manifest" plugin="org.ekstep.text" ver="1.2" src="/content-plugins/org.ekstep.text-1.2/manifest.json" type="json"/>

</manifest>

 **<plugin-manifest>** 

 **<plugin id="org.ekstep.navigation" ver="1.0" type="plugin" depends=""/>** 

 **<plugin id="org.ekstep.text" ver="1.2" type="plugin" depends=""/>** 

 **</plugin-manifest>** 

</theme> 

 **Solution** : 

Add outward relations with content to the plugins used in the content. This helps to quickly identify the contents which are using the specific plugin.


* plugins field is inserted in the metadata of old published resources using node script.
* This is been handled in the request header, while creation/updation.
* Both Scenarios i.e Content editor and CBSE program have been covered.

 **Format of plugins field in metadata of resource as follows** :

plugins: \[{ identifier: ' ' , semanticVersion: ' '  }]

For the above ECML content we have included new key 'plugins' in metadata of content as below:


```
"plugins":"\[{ "identifier ": "org.ekstep.stage ", "semanticVersion ": "1.0 "},

{ "identifier ": "org.ekstep.text ", "semanticVersion ": "1.2 "},

{ "identifier ": "org.ekstep.shape ", "semanticVersion ": "1.0 "},

"identifier ": "org.ekstep.navigation ", "semanticVersion ": "1.0 "}]"
```


*****

[[category.storage-team]] 
[[category.confluence]] 

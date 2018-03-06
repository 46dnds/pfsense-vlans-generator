# pfsense-vlans-generator
because i'm lazy and I want my vlans to be sorted

copy and paste in chrome developper tools (F12), replace your magic token and adjust numbers to fit your needs

```javascript
var
maxVlan = 500, // maximum vlan id (where to stop)
i       = 10, // minimum vlan id (where to start)
token   = '', //your magic token
iface   = '', // your interface (enp0,bge0,bxe1 etc)
pcp     = '1', // Qos priority (0 to 7)
doReq   = function(){
    if(i==maxVlan)
        return;
    $.post('/interfaces_vlan_edit.php',{
        '__csrf_magic'  : token,
        'if'            : iface,
        'tag'           : i+'',
        'pcp'           : pcp,
        'descr'         : ''+i,
        'vlanif'        : '',
        'save'          : 'Save'
    },function(){

      i++;
      doReq();
    });
};
doReq();
```

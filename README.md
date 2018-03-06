# pfsense-vlans-generator
because i'm lazy and I want my vlans to be sorted

copy and paste in chrome developper tools (F12), replace your interface and numbers to fit your needs

```javascript
var
verbose = false, //set to true to view the progress
maxVlan = 500, // maximum vlan id (where to stop)
i       = 10, // minimum vlan id (where to start)
step    = 1, // increment of X
iface   = 'bxe0', // your interface (enp0,bge0,bxe1 etc)
pcp     = '1', // Qos priority (0 to 7)
doReq   = function(){
    if(i>maxVlan){
        if(verbose) console.log('WE\'RE DONE.');
        return;
    }
    if(verbose) console.log('Setting vlan #'+i+'/'+maxVlan+'...');
    $.post('/interfaces_vlan_edit.php',{
        '__csrf_magic'  : csrfMagicToken,
        'if'            : iface,
        'tag'           : i+'',
        'pcp'           : pcp,
        'descr'         : ''+i,
        'vlanif'        : '',
        'save'          : 'Save'
    },function(){
        if(verbose) console.log('Vlan #'+i+'/'+maxVlan+' set.');
        i+=step;
        doReq();
    });
};
doReq();
```

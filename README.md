# DEMO-17-06-2022

Example: https://medium.com/@stephenpaynter/netbox-webhooks-with-ansible-tower-eaa6dd98320

On Ansible:
- On the Template, set Variables "Prompt on launch" checkbox 
- User icon -> User Details -> Tokens -> Add -> Scope=Write
- Token: zdfy7plqUzJWdm58gOA1PCJJ9okKcn


On Netbox
- User icon -> Profile -> API Tokens
- User icon -> Admin -> Webhooks -> Add (DCIM->Interface, Enabled)

Netbox Data Model

VLANs
{
'id': 4333,
'url': '/api/dcim/interfaces/4333/', 
'device': OrderedDict([('id', 318), ('url', '/api/dcim/devices/318/'), ('name', 'ios-sw1'), ('display_name', 'ios-sw1')])
'name': 'Ethernet1/0',
'label': '',
'type': OrderedDict([('value', 'virtual'), ('label', 'Virtual')]),
'enabled': True,
'lag': None,
'mtu': None,
'mac_address': '',
'mgmt_only': False,
'description': 'Ethernet1/0 description',
'connected_endpoint_type': None,
'connected_endpoint': None,
'connection_status': None,
'cable': None,
'mode': OrderedDict([('value', 'access'), ('label', 'Access')]),
'untagged_vlan': OrderedDict([('id', 491), ('url', '/api/ipam/vlans/491/'), ('vid', 20), ('name', 'twenty'), ('display_name', 'twenty (20)')]),
'tagged_vlans': [],
'tags': [],
'count_ipaddresses': 0
}

{ 
 "extra_vars": 
  {
     "device": "{{ data['device']['name'] }}"
     "interface": "{{ data['name'] }}",
     "vlan_id": "{{ data['untagged_vlan']['vid'] }}",
     "vlan_name": "{{ data['untagged_vlan']['name'] }}",
     "event": "{{ event }}",
     "timestamp": "{{ timestamp }}",
     "data": "{{ data }}"
  },
  "limit": "{{ data['device']['name'] }}"
}

IP


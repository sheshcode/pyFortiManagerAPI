# pyFortiManagerAPI

A Python wrapper for the FortiManager REST API.

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install pyFortiManagerAPI.

```bash
pip install pyFortiManagerAPI
```

## Getting Started

1. Creating Instance of the Module

```python
import pyFortiManagerAPI
fortimngr = pyFortiManagerAPI.FortiManager(host="", username="",password="")
```

- host: Management Ip address of your FortiManager
- username/password: Specify your credentials to log into the device.

# User Operations : Address Objects

### 1) Get all address objects from FortiManager.

```python
>>> fortimngr.get_firewall_address_objects()
```

### 2) Get specific address object from FortiManager using "name" Filter.

```python
>>> fortimngr.get_firewall_address_objects(name="YourObjectName")
```

- ## Parameters

* name: Specify object name that you want to see.

### 3) Create an address object.

```python
>>> fortimngr.add_firewall_address_object(name="TestObject",
                                          associated_interface="any",
                                          subnet=["1.1.1.1", "255.255.255.255"]
                                          )
```

- ## Parameters

* name: Specify object name that is to be created
* associated_interface: Provide interface to which this object belongs if any. {Default is kept any}
* subnet: Specify the subnet in a list format eg.["1.1.1.1", "255.255.255.255"]

### 4) Update address object.

```python
>>> fortimngr.update_firewall_address_object(name="TestObject",
                                             data={"subnet": ["2.2.2.2", "255.255.255.255"]}
                                             )
```

- ## Parameters

* name: Enter the name of the object that needs to be updated
* data: You can get the **kwargs parameters with "show_params_for_object_update()" method

### 5) Delete address object.

```python
>>> fortimngr.delete_firewall_address_object(object_name="TestObject")
```

- ## Parameters

* object_name: Specify the Object name you want to delete.

---

# User Operations : Address Groups

### 6) Get all address groups.

```python
>>> fortimngr.get_address_group()
```

### 7) Get specific address group.

```python
>>> fortimngr.get_address_group(name="TestGroup")
```

- ## Parameters

* name: Specify the name the address group.

### 8) Create your own address group.

```python
>>> fortimngr.add_address_group(name="Test_Group",
                                members=["TestObject1"])
```

- ## Parameters

* name: Enter the name of the address group. eg."Test_Group"
* members: pass your object names as members in a list eg. ["TestObject1", "TestObject2"]
  > Note: An address group should consist atleast 1 member.

### 9) Update the address group.

```python
>>> fortimngr.update_address_group(name="Test_Group",
                                   object_name="TestObject3",
                                   do="add")
```

- ## Parameters

* name: Specify the name of the Address group you want to update
* object_name: Specify name of the object you wish to update(add/remove) in Members List
* do: Specify if you want to add or remove the object from the members list
  do="add" will add the object in the address group
  do="remove" will remove the object from address group

### 10) Delete the address group.

```python
>>> fortimngr.delete_address_group(name="Test_group")
```

- ## Parameters

* name: Specify the name of the address group you wish to delete

---

# User Operations : Policies

### 11) Get all the policies in your Policy Package.

```python
>>> fortimngr.get_firewall_policies(policy_package_name="YourPolicyPackageName")
```

- ## Parameters

* policy_package_name: Enter the policy package name.

### 12) Get specific policiy in your Policy Package using PolicyID filter.

```python
>>> fortimngr.get_firewall_policies(policy_package_name="YourPolicyPackageName", policyid=3)
```

- ## Parameters

* policy_package_name: Enter the policy package name.
* policyid: Can filter and get the policy you want using policyID

### 13) Create your own policy in your Policy Package.

```python
>>> fortimngr.add_firewall_policy(policy_package_name="YourPolicyPackageName",
                                  name="YourPolicyName",
                                  source_interface="port1",
                                  source_address="all",
                                  destination_interface="port2",
                                  destination_address="all",
                                  service="ALL_TCP",
                                  logtraffic=2
                                  )

```

- ## Parameters

* policy_package_name: Enter the name of the policy package eg. "default"
* name: Enter the policy name in a string format eg. "Test Policy"
* source_interface: Enter the source interface in a string format eg. "port1"
* source_address: Enter the src. address object name in string format eg. "LAN_10.1.1.0_24"
* destination_interface: Enter the source interface in a string format eg. "port2"
* destination_address: Enter the dst. address object name eg. "WAN_100.25.1.63_32"
* service: Enter the service you want to permit or deny in string eg. "ALL_UDP"
* schedule: Schedule time is kept 'always' as default.
* action: Permit(1) or Deny(0) the traffic. Default is set to Permit.
* logtraffic: Specify if you need to log all traffic or specific in int format.
*                  logtraffic=0  Means No Log
                   logtraffic=1  Means Log Security Events
                   logtraffic=2  Means Log All Sessions

### 14) Update the policy in your Policy Package.

```python
>>> fortimngr.update_firewall_policy(policy_package_name="YourPolicyPackageName",
                                     policyid=10,
                                     data={
                                           "srcintf": "port2",
                                           "action": 0,
                                           "logtraffic": 0
                                           })
```

- ## Parameters

* policy_package_name: Enter the policy package name in which you policy belongs.
* policyid: Enter the Policy ID you want to edit
* data: You can get the **kwargs parameters with "show_params_for_policy_update()" method

### 15) Delete the policy in your Policy Package.

```python
>>> fortimngr.delete_firewall_policy(policy_package_name="YourPolicyPackageName",
                                     policyid=10)
```

- ## Parameters

* policy_package_name: Enter the policy package name in which you policy belongs
* policyid: Enter the policy ID of the policy you want to delete

---

# User Operations : Installing the Policy Package.

### 16) Installing the Policy Package.

```python
>>> fortimngr.install_policy_package(package_name="Your Policy Package name")

```

- ## Parameters

* package_name: Enter the package name you wish to install

---

## Future Tasks

- This module is tested on Fortimanager v6.2.2 on "root" adom. It still doesn't support multiple Adoms. So I will try to get this working for Multiple adoms too.
- To update any object or firewall policies we need to pass data in Dictonary and this seems to be slightly complicated. I will try to simplify this too. (This task is now achieved in version v0.0.4a) 

## Contributing

- Being new to Python and this being my first publish, to get this module fully working for all of us, the Pull requests are welcome.

## License

[MIT](https://choosealicense.com/licenses/mit/)

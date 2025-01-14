### Cisco sdk's

Pagination = a part of the dataset

# Model driven programmability

## YANG
Yet Another Next Generation

It is a model that defines how the structure of the device (network device) looks like.
It dictates how the schema of a device looks like.
It can then use XML as the markup of the data to manipulate the instance.

Parts in that model are:
- it defines the module
- the metadata
- A container that can hold a list (for example a list of interfaces)
- leaf nodes, these are the fields that can hold data for every item in the list
- there is also a operational state data container that can hold read-only data, for the read-out of statistics and metrics of the device.
##### Example of how the definition of a yang model looks like (in .yang format)
```yang
module simple-interface {
  namespace "urn:example:simple-interface";
  prefix si;

  organization "Example Organization";
  contact "support@example.com";

  description
    "A simple YANG model for configuring network interfaces.";

  revision "2025-01-11" {
    description "Initial revision.";
  }

  container interfaces {
    description "Top-level container for all interfaces.";
    
    list interface {
      key "name";
      description "List of network interfaces.";

      leaf name {
        type string;
        description "Name of the interface.";
      }

      leaf description {
        type string;
        description "A short description of the interface.";
      }

      leaf type {
        type string;
        description "Type of interface (e.g., Ethernet, VLAN, etc.).";
      }

      leaf enabled {
        type boolean;
        default true;
        description "Administrative status of the interface. True means enabled.";
      }

      container statistics {
        config false; // Read-only
        description "Operational state and statistics of the interface.";

        leaf in-octets {
          type uint64;
          description "Number of incoming octets.";
        }

        leaf out-octets {
          type uint64;
          description "Number of outgoing octets.";
        }
      }
    }
  }
}

```
##### Example of a YANG model instance in a XML format:
```XML
<interfaces xmlns="urn:example:simple-interface">
  <interface>
    <name>GigabitEthernet0/1</name>
    <description>Uplink to Router</description>
    <type>Ethernet</type>
    <enabled>true</enabled>
  </interface>
</interfaces>

```



## NETCONF

Netconf and YANG are practically always used together. 
Netconf uses SSH to establish a connection to the device. once connected it uses RPC calls to exchange data in the form of XML in YANG model form.

## RESTCONF

RESTfull compatible NETCONF

The same as NETCONF but uses HTTP / HTTPS instead of SSH.
This gives the ability to use all the HTTP methods: GET, POST, PUT, DELETE .

Data format is also XML but it can also hande JSON

It integrates better with modern web tools
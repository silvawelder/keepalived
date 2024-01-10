# keepalived
studing keepalived

KeepAlived file configurations

```
# Global defs
global_defs {
        router_id lb-k8s-dev
}

vrrp_script check_kubeapi {
    script "/usr/bin/nc -zv localhost 6443" 
    interval 3
    weight 5
}

vrrp_instance ens160 {
        state master
        interface ens160
        virtual_router_id 6
        priority 105
        advert_int 3
        authentication {
                auth_type PASS
                auth_pass lbdcqq99
        }
        track_script {
                check_kubeapi
        }
        virtual_ipaddress {
                10.0.6.81 dev ens160 label ens160:vip
        }
}

```
| Configuration        | Options        | Definition                                                                                                                  |
|----------------------|----------------|-----------------------------------------------------------------------------------------------------------------------------|
| vrrp_instance ens160 | N/A            | defines an individual instance of the VRRP protocol running on an interface. I have arbitrarily named this instance ens160. |
| state master         | master, backup | state defines the initial state that the instance should start in                                                           |
| interface            |                | defines the interface that VRRP runs on.                                                                                    |
| virtual_router_id    |                | is the unique identifier                                                                                                    |
|                      |                |                                                                                                                             |
|                      |                |                                                                                                                             |
|                      |                |                                                                                                                             |
|                      |                |                                                                                                                             |
|                      |                |                                                                                                                             |

# References

1. https://www.redhat.com/sysadmin/ha-cluster-linux
2. https://www.redhat.com/sysadmin/keepalived-basics

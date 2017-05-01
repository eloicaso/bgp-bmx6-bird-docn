# Manual Procedures

`Last update 01/05/2017`

## Introduction
This document aims to gather all the manual procedures not yet adopted by neither bird{4|6}-uci or luci-app-bird{4|6} packages and are relevant to most of the adminsitrators using them.

## Adding Custom Routing Tables
One of the most common elements in Bird{4|6} are Kernel tables. These tables are use to either store or share routes between Protocols and the OS. Because some of these protocols may want to tweak/hack the contents of what it receives or shares it is common to have hinge tables for this sort of operations.

If you need to do add any extra tables to your system, add them following this procedure:

### 1. Web UI (LUCI)
* Login to your system and follow this path:
  ```Network > Bird{4|6} > General Protocols```

* Find the target **Kernel** table you need to modify and the **kernel_table** setting (you may need to `Add` it). *kernel_table* requires you to add a numeric entry. As an example, this topic will cover **one** custom kernel table called *bgpTable* with ID *251*.

#### 1.1 How to identify which Kernel Table number you should use in the Web UI (Terminal)?
> Using LEDE v17.01.0-RC2 for reference, we can see that the OS allows us to use to up to 65535 possible options (this number may differ according to your LEDE/OpenWRT OS configuration):
```
root@LEDE-1701rc2:~# ip route list table 65535
root@LEDE-1701rc2:~# ip route list table 65536
ip: invalid argument '65536' to 'table'
```
As you can see in this snippet, the first execution output is empty, which means that the table exists, but is empty. The second execution shows an error, notifying you that this table is not valid. 

Now follow this steps:

* Open an SSH connection to your LEDE system and login.
* Execute the following command: `cat /etc/iproute2/rt_tables`
  Its contents will be similar to these:
```
root@LEDE-eloi:~# cat /etc/iproute2/rt_tables 
# reserved values
128	prelocal
255	local
254	main
253	default
0	unspec
# local
251	bgpTable
```
As you can see in this code snippet, there is a special section for local (custom) tables. Our example has a **custom** table called *bgpTable* with the Key ID *251*.

The only key rules is not to use reserved values. It varies according how many entries your LEDE/OpenWRT supports, but moving to high numbers will surely avoid collisions. An example of that would be to use this entry: `1000 myCustomTable`.

In order to add/edit/delete custom tables, add entries **in the bottom** of the file: `vim /etc/iproute2/rt_tables`.

> As good practice: check if your target Table is `Reserved` or out of your Kernel Table's range.

> Custom tables may not work immediately after adding them. In the event that your custom tables do not respond after a reasonable period of time, reboot your system.
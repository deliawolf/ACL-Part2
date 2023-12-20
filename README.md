# ACL Part 2

## Standart ACL
Standard IPv4 ACLs, whether numbered (1 to 99 and 1300 to 1999) or named, filter packets that are based on a source address and mask, and they permit or deny the entire TCP/IP protocol suite.
### Configure a numbered standard IPv4 ACL.
```
RouterX(config)# access-list 1 permit 172.16.0.0 0.0.255.255
```
1. The statement matches any source address that starts with 172.16.x.x.
2. Standard ACL configuration uses 1 to 99, or 1300 to 1999, for the ACL number (1 was used in the example).
3. The default wildcard mask is 0.0.0.0 (only standard ACL).

### Display the current ACLs configured on RouterX.
```
RouterX# show access-lists 
Standard IP access list 1
      10 permit 172.16.0.0, wildcard bits 0.0.255.255
```
### Delete a numbered standard IPv4 ACL.
```
RouterX(config)# no access-list 1 
RouterX(config)# exit 
RouterX# show access-lists 
RouterX#
```

## Extended ACL
Extended ACLs provide a greater range of control. In addition to verifying packet source addresses, extended ACLs also check destination addresses, protocols, and port numbers.

### Configure Numbered Extended IPv4 ACLs
1. The first line of the ACL denies FTP traffic from subnet 172.16.4.0/24 to subnet 172.16.3.0/24.
2. The second line of the ACL permits all other traffic.
3. Extended ACL configuration uses numbers from 100 to 199, or 2000 to 2699 (101 was used in the example).
```
RouterX(config)# access-list 101 deny tcp 172.16.4.0 0.0.0.255 172.16.3.0 0.0.0.255 eq 21
RouterX(config)# access-list 101 permit ip any any
```

For extended access lists, you can specify either the name or the number of the protocol. The most commonly used keywords are ip, tcp, udp, and icmp.

When TCP or UDP is specified as the protocol, it is possible to include lt (less than), gt (greater than), eq (equal), neq (not equal), and range (inclusive range) to match specific network applications by name (for example, www, FTP, SSH) or number (for example, 80, 21, 22).

Display the current ACL number 101 configured on RouterX.
```
RouterX# show access-lists 101
Extended IP access list 101
    10 deny tcp 172.16.4.0 0.0.0.255 172.16.3.0 0.0.0.255 eq ftp
    20 permit ip any any
```
The output of the show access-list 101 command displays only the newly added extended ACLs that were configured on RouterX.

Notice that the port number 21 that was initially configured was automatically replaced by the keyword FTP.

As was the case with the standard access-list, using the no access-list 101 command removes the entire extended ACL 101 from the router.

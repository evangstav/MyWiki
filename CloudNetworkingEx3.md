 = Question 1 =
 In scenario 1, while pinging between H1 and H2, capture traffic in the default network workspace. What do you see? Why?
 
 *Answer*
 We observed that we can't capture any traffic in the root network workspace. That is to be expected since the other two workspaces form an isolated network through the virtual ethernet interface, which isn't visible by the root namespace.
 
 = Question 2 =
 In scenario 1:
 a) Try to compare the filesystems of H1 and H2.
 b) What about the running processes
 
*Answer*
a) We can see that the filesystems are exactly the same and whatever we in one netspace filesystem is visible to the other. For example if we create a file in on space it is visible to the other as well. And if we delete, it it is deteleted in both network namespaces. That behaviour is to be expected, since both netowrk namespaces share the same mount namespace/filesystem.
b) The same situation was observed with the processes as processes created within one network namespace are visible and can be killed by the other network namespace and vice versa. That happens because both network namespaces share the same PID namespace. 
   
# Question 3
In scenario 3, when connecting to the outside, we have used IPTables. How can we use them to emulate application behaviour above layer 3 when loosing connectivity?

Given that iptables is a tool that filters, manages and modifies(?) ip packets, it is possible to emulate certain layer 3 conditions. For example by dropping every packet incoming from from a node, you can emulate a broken connection on that nodes side. Other examples could be allowing connections to be established but dropping any data packets, or blocking all access to specific ip addresses.


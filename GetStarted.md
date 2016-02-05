## Cluster Monitoring Tool ##

Cluster Monitoring Tool is a simple web application (war file) that enables you to monitor your running Hazelcast cluster. It is distributed with Hazelcast as of 1.8.1 version.

It is not using JMX, so the effect to your running cluster is negligible. You can only monitor cluster that runs the same version of Hazelcast. In order to use it, you should first upgrade to 1.8.1 and then use the tool.

To use it

1.  Download hazelcast-`<`version`>`.zip.

2.  Locate hazelcast-monitor-`<`version`>`.war under main directory of unzipped directory.

3.  Deploy it to your web container. For Tomcat, simply copy the war file to webapps directory.

4.  Go to http://localhost:8080/hazelcast-monitor-1.8.1/

5.  You need to add a cluster to monitor.

![http://www.hazelcast.com/resources/monitor-login.png](http://www.hazelcast.com/resources/monitor-login.png)

> To add a cluster, type
    * cluster-group-name (default is dev),
    * cluster-group-password (default is dev-pass)
    * ip:port of the one of the members.(ex 10.10.1.1, 10.10.1.2:5702). Default port is 5701.
    * and press Add Cluster button.

> Note that you can add more than one cluster to monitor.

![http://www.hazelcast.com/resources/monitor-cluster-view.png](http://www.hazelcast.com/resources/monitor-cluster-view.png)

> You can see
    * Cluster members
    * Map, Queue, ... instances. On 1.8.1 only Map instances can be monitored.
    * Internals

6. Expand Maps tree and click on any map instance. If you can't see any instance then your cluster does not use any map.

![![](http://www.hazelcast.com/resources/monitor-screen-small.png)](http://www.hazelcast.com/resources/monitor-screen.png)

> On right side following panels will be displayed

  * **Charts**:
> When you click on a map instance you will see two charts displaying:
    1. Size&Memory
    1. Throughput chart

_Size& Memory_

It shows the number of entries in your map and the memory that those entries occupy. The values are aggregation of all members. To see the details, like how the entries are partitioned among members, see Size&Memory Details panel.
_Throughput_

This chart shows how many map operations per second your cluster is doing in total. Again it is aggregation of all members. To see how each member is doing see Throughput Details panel.

  * **Table Panels**:
> > Under charts there is three table panels.
      1. Throughput Details
      1. Size&Memory Details
      1. Times Details

These tables show you the details per member.


_Throughput Details_

Shows the number of map operations;gets, puts, removes and others per second for each member.

_Size&Memory Details_

Displays how your entries are partitioned among members. How many entries and backups each member owns. In Hazelcast the preceding member is the backup of the previous. So you can watch how your entries are backed up and what happens when a member leaves the cluster. If your cluster is doing lots of puts and removes, you will notice that the owned and backup numbers will not exactly match.
This doesn't mean that Hazelcast does not backup properly. The mismatch happens because tool makes a call to each node, asking their internal details. It is a distributed task and not all members reply at the same time. That's why the numbers may not be exactly same. But they should be very very close.

Also notice the marked as remove part. When you remove an entry, hazelcast will mark it as removed but will delay the actual removal process. Those columns show number of entries waiting for removal and their memory size.

You also can see total number of locked entries on each member and total number of threads at all members waiting for those entries.

_Times Details_

This table displays several timing details on each member.

  * **Map Browser**

> Enables you to perform get operation on the map. Gives the details of the entry. To browse the map the key of your map have to be String. See the picture for more details.

![http://www.hazelcast.com/resources/monitor-map-browser.png](http://www.hazelcast.com/resources/monitor-map-browser.png)





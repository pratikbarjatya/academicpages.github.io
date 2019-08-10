---
title: "Best practices for YARN resource managements"
excerpt: "Best practices for YARN resource management"
collection: learning
date: 2019-07-29

---

Best practices for YARN resource management
======

- The fundamental idea of MRv2(YARN) is to split up the two major functionalities—resource management and job scheduling/monitoring, into separate daemons.
- The idea is to have a global ResourceManager (RM) and per-application ApplicationMaster (AM).
- The ResourceManager(RM) and per-node slave, the NodeManager (NM), form the data-computation framework.
- The ResourceManager is the ultimate authority that arbitrates resources among all the applications in the system.

- How does warden calculate and allocate resources to YARN?
=======
    - YARN can manage 3 system resources— memory, CPU and disks.
    Once warden finishes calculations, it will set environment variable YARN_NODEMANAGER_OPTS for starting NM.
    - For example, if you “vi /proc/<pid_for_NM>/environ” you can find the settings below:
        {

            YARN_NODEMANAGER_OPTS= -Dnodemanager.resource.memory-mb=10817
            -Dnodemanager.resource.cpu-vcores=4
            -Dnodemanager.resource.io-spindles=2.0

        }
    - They can be overridden by setting the three configurations below in yarn-site.xml on NM nodes and restarting NM.
        - yarn.nodemanager.resource.memory-mb
        - yarn.nodemanager.resource.cpu-vcores
        - yarn.nodemanager.resource.io-spindles
    - To view the available resources from each node, you can go to RM UI(http://<IP_of_RM>:8088/cluster/nodes), and find out the “Mem Avail”, “Vcores Avail” and “Disk Avail” from each node.
- Minimum and maximum allocation unit in YARN
=======
    - Two resources—memory and CPU, as of in Hadoop 2.5.1, have minimum and maximum allocation unit in YARN, as set by the configurations in yarn-site.xml.
    - Basically, it means RM can only allocate memory to containers in increments of "yarn.scheduler.minimum-allocation-mb" and not exceed "yarn.scheduler.maximum-allocation-mb"
    - It can only allocate CPU vcores to containers in increments of "yarn.scheduler.minimum-allocation-vcores" and not exceed "yarn.scheduler.maximum-allocation-vcores"
    - If changes required, set above configurations in yarn-site.xml on RM nodes, and restart RM.
- Virtual/physical memory checker
=======
    - NodeManager can monitor the memory usage(virtual and physical) of the container.
    - If its virtual memory exceeds “yarn.nodemanager.vmem-pmem-ratio” times the "mapreduce.reduce.memory.mb" or "mapreduce.map.memory.mb", then the container will be killed if “yarn.nodemanager.vmem-check-enabled” is true
    - If its physical memory exceeds "mapreduce.reduce.memory.mb" or "mapreduce.map.memory.mb", the container will be killed if “yarn.nodemanager.pmem-check-enabled” is true
- Mapper,Reducer and AM’s resource request
=======
    - MapReduce v2 job has 3 different container types—Mapper, Reducer and AM.
    - Mapper and Reducer can ask for resources—memory, CPU and disk, while AM can only ask for memory and CPU.
    - Each container is actually a JVM process, and above “-Xmx” of java-opts should fit in the allocated memory size. One best practice is to set it to 0.8 * (container memory allocation)
    - Any type of the container can run out of memory and be killed by physical/virtual memory checker, if it doesn't meet the minimum memory requirement
    - if the MapReduce job sorts parquet files, Mapper needs to cache the whole Parquet row group in memory. In this case, make sure the Mapper memory is large enough without triggering OOM.
- Bottleneck resource
=======
    - Since there are three types of resources, different containers from different jobs may ask for different amount of resources. This can result in one of the resources becoming the bottleneck.
    - Suppose we have a cluster with capacity (1000G RAM,16 Cores,16 disks) and each Mapper container needs (10G RAM,1 Core, 0.5 disks): at most, 16 Mappers can run in parallel because CPU cores become the bottleneck here
    - If you meet this situation, just check the RM UI(http://<ip_of_rm>:8088/cluster/nodes) to figure out which resource is the bottleneck
    - You can allocate the leftover resources to jobs which can improve performance with such resource\

- Key takeaways:
=======
    - Make sure warden considers all services when allocating system resources.
    - Be familiar with lower and upper bound of resource requirements for mapper and reducer.
    - Be aware of the virtual and physical memory checker.
    - Set -Xmx of java-opts of each container to 0.8 * (container memory allocation).
    - Make sure each type of container meets proper resource requirement.
    - Fully utilize bottleneck resource.
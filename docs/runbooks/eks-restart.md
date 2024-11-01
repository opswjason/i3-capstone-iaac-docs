# Restart  EKS  Cluster

## Purpose

This  runbook  details  the  steps  required  to  safely  restart  an  Amazon  EKS  cluster.

## Prerequisites

-   AWS  IAM  user  with  sufficient  permissions  to  manage  EKS  clusters.   
-   AWS  CLI  installed  and  configured  with  appropriate  credentials.  
-   kubectl  installed  and  configured  to  interact  with  your  EKS  cluster.
    

## Steps

**1.  Identify  the  EKS  Cluster**

-   Log  in  to  the  AWS  Management  Console.   
-   Navigate  to  the  EKS  Dashboard.  
-   Identify  the  cluster  to  be  restarted.  Note  its  Cluster  Name  and  Region.
    

**2.  Drain  Nodes  in  the  Cluster**

-   Use  kubectl  to  drain  each  node  to  safely  evict  all  pods,  ignoring  daemonsets  and  deleting  local  data.  
-   Repeat  for  each  node  in  the  cluster.
    

**3.  Delete  Worker  Nodes  (Optional)**

-   If  you  need  to  terminate  worker  nodes,  use  the  AWS  CLI  to  terminate  the  instances.  
-   Ensure  new  worker  nodes  are  launched  automatically  if  configured  with  an  Auto  Scaling  Group.
    

**4.  Restart  the  EKS  Control  Plane**

-   Restarting  the  control  plane  involves  stopping  and  starting  the  EKS  cluster  through  the  AWS  Management  Console.  
-   In  the  EKS  Dashboard,  select  the  cluster  to  restart,  choose  Stop,  and  then  Start  to  restart  the  control  plane.
    

**5.  Re-join  Worker  Nodes  to  the  Cluster**

-   Ensure  that  worker  nodes,  either  existing  or  newly  launched,  are  re-joined  to  the  cluster. 
-   Use  kubectl  to  uncordon  the  nodes. 
-   Repeat  for  each  node  in  the  cluster.
    

**6.  Verify  Cluster  State**

-   Ensure  that  all  nodes  are  in  a  ready  state  using  kubectl.
-   Check  the  status  of  all  pods  to  ensure  they  are  running  correctly.
    

**7.  Notifications**
-   Notify  relevant  team  members  or  stakeholders  that  the  EKS  cluster  has  been  restarted.

## Post-conditions

-   The  EKS  cluster  should  be  fully  operational.
-   All  nodes  should  be  in  a  ready  state.
-   All  services  and  pods  should  be  running  correctly.
# Distributed Scheduling

Please write a design document about distributed scheduling and impeachment it.

Evaluation aspects:
- Learning ability
- Depth of thinking on single-point issues
- Hands-on ability

## Background

In all cloud providers, like AWS, Google, and others, there are many spot instances.
They are quite cheap (10% of the on-demand instances' price), but after you buy them,
they could be terminated with only two minutes' notice in advance (in most scenarios,
we don't set PDB, and we should perform the graceful drain).

So I want you to design a way to maximize the use of spot instances without service
interruption instead of on-demand instances, to cut costs, by using distributed scheduling
in a single cluster (on-demand/spot mixed or other methods for one workload).
This is important because all spot instances being terminated at the same time could
cause interruptions for different kinds of workloads (single replica workload, multiple replica workload).

Also, I don't want to change the scheduler already used in the K8s cluster and want to
ensure the minimal components necessary in the cluster.

Notes:
> 1. On demand nodes has label: node.kubernetes.io/capacity: on-demand.
> 2. Spot node has label: node.kubernetes.io/capacity: spot.
> 3. Workloads represented as Deployments and StatefulSets.
> 4. on-demand/spot instance represented as K8s nodes in the cluster.
> 5. Only focus on scheduling control; the graceful drain after receiving the terminal notification is handled by other components.

## Output

- A rough design document (English)
- An easy implementation (After talking to the interviewer)


背景
在所有云服务提供商中，比如AWS和Google等，存在许多临时实例（spot instances）。这些实例相对便宜（只有按需实例价格的10%），
但购买后可能会在仅提前两分钟的通知下被终止（在大多数情况下，我们不设置保护性中断预算PDB，并且应该执行优雅的资源释放）。

设计目标是在不中断服务的情况下最大化使用临时实例以替代按需实例，以此降低成本。
需要使用分布式调度在单个集群中实现（可能是按需/临时混合或其他方式处理单一工作负载）。
这一点非常重要，因为所有临时实例同时被终止可能会导致不同类型的工作负载（单副本工作负载、多副本工作负载）中断。

此外，设计中不希望改变已经在K8s集群中使用的调度器，并且希望确保集群中的组件尽可能简洁。

注释
- 按需节点的标签为：node.kubernetes.io/capacity: on-demand.
- 临时节点的标签为：node.kubernetes.io/capacity: spot.
- 工作负载以Deployments和StatefulSets表示。
- 按需/临时实例在集群中表示为K8s节点。
- 只关注调度控制；在接收到终止通知后的优雅资源释放由其他组件处理。









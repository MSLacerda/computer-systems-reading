# **[Serverless in the Wild: Characterizing and Optimizing the Serverless Workload at a Large Cloud Provider](https://arxiv.org/pdf/2003.03423.pdf)**

## Abstract
Function as a Service (FaaS) has been gaining popularity as a way to deploy computations to serverless backends in the cloud. This paradigm shifts the complexity of allocating and provisioning resources to the cloud provider, which has to provide the illusion of always-available resources (i.e., fast function invocations without cold starts) at the lowest possible resource cost. Doing so requires the provider to deeply understand the characteristics of the FaaS workload. Unfortunately, there has been little to no public information on these characteristics. Thus, in this paper, we first characterize the entire production FaaS workload of Azure Functions. We show for example that most functions are invoked very infrequently, but there is an 8-order-of-magnitude range of invocation frequencies. Using observations from our characterization, we then propose a practical resource management policy that significantly reduces the number of function cold starts, while spending fewer resources than state-of-the-practice policies.

## Problem
Function as a Service (FaaS) is a recent approach to doing Serverless applications. Since it is quite new, we hadn't yet public data describing a typical workload of these applications. These workloads are essential for benchmarking purposes, once this enables more precise tests for design/architecture changes. This work not only provides the workload publicly but also performed a deep characterization of it.

## Contribution
- A detailed characterization of the entire production FaaS workload at a large cloud provider;
- A new policy for reducing the number of cold start function executions at a low resource provisioning cost;
- Extensive simulation and experimental results based on real traces showing the benefits of the policy;
- An overview of our implementation in Azure Functions;
- A large sanitized dataset containing production FaaS traces.

## Conclusion
In this paper, we characterized the entire production FaaS workload of Azure Functions. The characterization unearthed several key observations for cold start and resource management. Based on them, we proposed a practical policy for reducing the number of cold starts at a low resource cost. We evaluated the policy using both simulations and a real implementation, and real workload traces. Our results showed that the policy can achieve the same number of cold starts at much lower resource cost, or keep the same resource cost but reduce the number of cold starts significantly. Finally, we overviewed our policy’s implementation in Azure Functions. We released sanitized traces from our characterization data at [Azure Functions Traces](https://github.com/Azure/AzurePublicDataset).

## Review
This paper provides a deep characterization of a production workload of FaaS applications and publicly shares a large dataset containing traces of this workload. The work is exquisitely well written and the main contribution is a watershed for future performance researches once now they have available an example of how applications behave in the real world. Thus, this article is strenuously relevant. I can't see any relevant flaw which is a worthy comment and I don't want to go nitpick on it.

## Related Work
- **FaaS characterization**. A few studies [7,15,24–26,44] have characterized the main commercial FaaS providers, but only from the perspective of external users. They typically reverse engineer aspects of FaaS offerings, by running benchmark functions to collect various externally visible metrics. Another class of studies looks at the ways developers are using FaaS offerings, by looking at public application repositories [41]. While valuable, this approach cannot offer insights on the aggregate workload seen by a provider
- **Optimizing FaaS serving**. Another set of relevant work considers optimizing different aspects of FaaS systems. Van Eyk et al. [42] identify performance-related challenges, including scheduling policies that minimize cold starts. For optimizing each cold start, Mohan et al. [32] find that pre-allocating virtual network interfaces that are later bound to new function containers can significantly reduce cold start times. SOCK [33] proposes to optimize the loading of Python functions in OpenLambda by smart caching of sets of libraries, and by using lightweight isolation mechanisms for functions. Replayable Execution [43] proposes checkpointing and sharing of memory among containers to speed up the startup times of a JVM-based FaaS system. 
- **Cache management**. Finally, one might think that the problem of managing cold starts is similar to managing caches of variable-sized objects, such as Web page caches and others [4,8,36].

For more related work, check it out in the paper.

## Links
- [Azure Functions Traces](https://github.com/Azure/AzurePublicDataset).
- [Paper publication](https://arxiv.org/abs/2003.03423)
- [Paper PDF](https://arxiv.org/pdf/2003.03423.pdf).

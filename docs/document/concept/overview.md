# 概览

## 什么是 Tekton ?
`Tekton`是用于构建CI/CD系统的云原生解决方案。它由提供构建模块的Tekton pipeline和支持组件(如Tekton CLI和Tekton Catalog)组成，这些组件使Tekton成为一个完整的生态系统。Tekton还是[Linux基金会项目](https://www.linuxfoundation.org/projects/)和[CD基金会](https://cd.foundation/)的一员。

`Tekton`会在 kubernetes(以下简称k8s) 集群上安装和运行一个扩展同时 `tekton` 也会提供一系列的k8s
用户自定义资源，这些自定义资源定义了一些您可以创建和重用的构建块。一旦安装成功，您就可以通过`kubectl`或
调用api来使用 Tekton 流水线来构建pod或其它资源。

## 面向人群
Tekton 面向的使用者如下:
- 那些为组织中的开发人员构建 CI/CD 系统的平台工程师。
- 那些使用那些CI/CD系统来完成工作的开发人员。

## Tekton 有何优势？
Tekton 为构建者和 CI/CD 系统的使用者提供了如下帮助:
- 可自定义。Tekton实体是完全可定制的，允许高度的灵活性。平台工程师可以定义一个非常详细的构建模块目录，供开发人员在各种场景中使用。
- 可重用。Tekton实体是完全可重用的，因此一旦定义，组织内的任何人都可以使用给定的管道并重用其构建块。这允许开发人员快速构建复杂的管道，而无需“重新造轮子”。
- 可拓展。Tekton Catalog是一个社区驱动的Tekton构建块存储库。您可以使用来自Tekton Catalog的预制组件快速创建新的和扩展现有的管道。
- 符合k8s标准。Tekton作为扩展在Kubernetes集群上安装和运行，并使用完善的Kubernetes资源模型。Tekton工作负载在Kubernetes容器内执行。
- 弹性。要增加工作负载容量，只需向集群中添加节点即可。Tekton可以根据您的集群进行扩展，而无需重新定义资源分配或对管道进行任何其他修改。

## Tekton 由哪些组件构成?
Tekton 的主要组成部分如下:
- [Tekton 流水线(pipelines)](https://github.com/tektoncd/pipeline/blob/main/docs/README.md)是整个 Tekton 的基础，它定义了一系列的k8s[自定义资源](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/),通过这些自定义资源，你可以将它们作为基本的构建块来组装您的 CI/CD 流水线。
- [Tekton 触发器(trigger)](https://github.com/tektoncd/triggers/blob/main/README.md)允许您基于事件执行管道。例如，您可以在每次PR与GitHub存储库合并时触发管道的实例化和执行。您还可以构建一个启动特定Tekton触发器的用户接口。
- [Tekton 命令行接口(CLI)](https://github.com/tektoncd/cli/blob/main/README.md)提供了一个名为`tkn`的命令行接口，该命令行工具基于 k8s 命令行接口构建，可以使用它来和 Tekton 进行交互。
- [Tekton Catalog](https://github.com/tektoncd/catalog/blob/v1beta1/README.md)是由社区贡献的高质量Tekton构建块(任务、管道等)的存储库，可以在您自己的管道中使用。
- [Tekton Hub](https://github.com/tektoncd/hub/blob/main/README.md)是一个用于访问 Tekton catalog 的 web 界面。
- [Tekton Operator](https://github.com/tektoncd/operator/blob/main/README.md)运行您在 k8s 集群上安装，升级和卸载 Tekton 项目。
- [Tekton Chain](https://github.com/tektoncd/chains/blob/main/README.md)为使用Tekton pipeline构建的制品提供生成、存储和签名来源的工具。
  
## 我该通过什么工具使用 Tekton?
要安装 Tekton，你需要一个 k8s 集群，运行为当前 Tekton 版本[指定的 k8s 版本](https://github.com/tektoncd/pipeline/#want-to-start-using-pipelines)。安装后，您可以使用以下方式之一与 Tekton 交互:
- [tkn cli](https://github.com/tektoncd/cli/blob/main/README.md)，也称为Tekton CLI，是与 Tekton交互 的首选命令行方法。`tkn` 提供了快速与便捷的体验，包括高级命令和颜色编码。要使用它，您只需要熟悉Tekton。
- [kubectl cli](https://kubernetes.io/docs/reference/kubectl/overview/),也被称为Kubernetes CLI，以更高的复杂性为代价为控制Tekton提供了更多的粒度。通过kubectl与Tekton交互通常用于调试管道和对构建进行故障排查。
- [Tekton API](https://kubernetes.io/docs/tasks/access-kubernetes-api/custom-resources/custom-resource-definitions/),目前可用于管道和触发器，允许您以编程方式与 Tekton 组件进行交互。这通常是为高度定制的 CI/CD 系统保留的。在大多数情况下，tkn和kubectl是控制Tekton的首选方法。

我们还建议在Kubernetes集群上配置以下项目:
- 用于指定输入和输出的持久卷声明。
- 适合您的环境和业务需求的权限。
- 用于构建和推送映像的存储(如果适用)。
  
  
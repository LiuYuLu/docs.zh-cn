---
title: "NetNamedPipeBinding | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "网络配置文件命名管道"
ms.assetid: e78e845f-c325-46e2-927d-81616f97f7d5
caps.latest.revision: 34
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 34
---
# NetNamedPipeBinding
本示例演示在同一台计算机上提供跨进程通信的 `netNamedPipeBinding` 绑定。  命名管道不能跨计算机工作。  本示例基于[入门](../../../../docs/framework/wcf/samples/getting-started-sample.md)计算器服务。  
  
 在本示例中，服务是自承载服务。  客户端和服务都是控制台应用程序。  
  
> [!NOTE]
>  本主题的最后介绍了此示例的设置过程和生成说明。  
  
 绑定是在客户端和服务的配置文件中指定的。  绑定类型是在 [\<endpoint\>](http://msdn.microsoft.com/zh-cn/13aa23b7-2f08-4add-8dbf-a99f8127c017) 元素的 `binding` 属性中指定的，如下面的示例配置所示：  
  
```  
<endpoint address="net.pipe://localhost/ServiceModelSamples/service"  
          binding="netNamedPipeBinding"  
          contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
 前面的示例演示如何配置终结点以使用具有默认设置的 `netNamedPipeBinding` 绑定。  如果要配置 `netNamedPipeBinding` 绑定并更改它的一些设置，则必须定义绑定配置。  终结点必须使用 `bindingConfiguration` 属性按名称来引用绑定配置。  
  
```  
<endpoint address="net.pipe://localhost/ServiceModelSamples/service"  
          binding="netNamedPipeBinding"  
          bindingConfiguration="Binding1"   
          contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
 在本示例中，绑定配置的名称为 `Binding1` 并具有以下定义：  
  
```  
<bindings>  
  <!--   
        Following is the expanded configuration section for a NetNamedPipeBinding.  
        Each property is configured with the default value.  
     -->  
  <netNamedPipeBinding>  
    <binding name="Binding1"   
             closeTimeout="00:01:00"  
             openTimeout="00:01:00"   
             receiveTimeout="00:10:00"   
             sendTimeout="00:01:00"  
             transactionFlow="false"   
             transferMode="Buffered"   
             transactionProtocol="OleTransactions"  
             hostNameComparisonMode="StrongWildcard"   
             maxBufferPoolSize="524288"  
             maxBufferSize="65536"   
             maxConnections="10"   
             maxReceivedMessageSize="65536">  
      <security mode="Transport">  
        <transport protectionLevel="EncryptAndSign" />  
      </security>  
    </binding>  
  </netNamedPipeBinding>  
</bindings>  
  
```  
  
 运行示例时，操作请求和响应将显示在客户端控制台窗口中。  在客户端窗口中按 Enter 可以关闭客户端。  
  
```  
  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### 设置、生成和运行示例  
  
1.  确保已经执行了[Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  若要用单一计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Binding\Net\NamedPipe`  
  
## 请参阅
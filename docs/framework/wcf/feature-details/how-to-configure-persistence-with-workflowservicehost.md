---
title: '방법: WorkflowServiceHost를 사용하여 지속성 구성'
ms.date: 03/30/2017
ms.assetid: e31cd4df-13a3-4a9a-9be8-5243e0055356
ms.openlocfilehash: 93397923154d780ed3b714bf0bb95c15bc71bbfb
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90556312"
---
# <a name="how-to-configure-persistence-with-workflowservicehost"></a>방법: WorkflowServiceHost를 사용하여 지속성 구성
이 항목에서는 구성 파일을 사용하여 <xref:System.ServiceModel.Activities.WorkflowServiceHost>에 호스트된 워크플로에 대해 지속성을 사용하도록 SQL 워크플로 인스턴스 저장소 기능을 구성하는 방법에 대해 설명합니다. SQL 워크플로 인스턴스 저장소 기능을 사용하려면 먼저 워크플로 인스턴스를 유지하는 데 사용되는 SQL 데이터베이스를 만들어야 합니다. 자세한 내용은 [방법: 워크플로 및 워크플로 서비스에 SQL 지 속성 사용](../../windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)을 참조 하세요.  
  
### <a name="to-configure-the-sql-workflow-instance-store-in-configuration"></a>구성에서 SQL 워크플로 인스턴스 저장소를 구성하려면  
  
1. SQL 워크플로 인스턴스 저장소의 속성은 XML 구성을 통해 설정을 변경하는 데 사용할 수 있는 서비스 동작인 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>를 통해 구성할 수 있습니다. 다음 구성 예제에서는 `sqlWorkflowInstanceStore` 구성 파일의 <> behavior 요소를 사용 하 여 SQL 워크플로 인스턴스 저장소를 구성 하는 방법을 보여 줍니다.  
  
    ```xml  
    <serviceBehaviors>  
        <behavior name="">  
            <sqlWorkflowInstanceStore
                 connectionString="provider=System.Data.SqlClient;Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true"  
                 instanceEncodingOption="GZip | None"  
                 instanceCompletionAction="DeleteAll | DeleteNothing"  
                 instanceLockedExceptionAction="NoRetry | SimpleRetry | AggressiveRetry"  
                 hostLockRenewalPeriod="00:00:30"
                 runnableInstancesDetectionPeriod="00:00:05">  
            </sqlWorkflowInstanceStore>  
        </behavior>  
    </serviceBehaviors>  
    ```  
  
     SQL 워크플로 인스턴스 저장소를 구성 하는 방법에 대 한 자세한 내용은 [방법: 워크플로 및 워크플로 서비스에 Sql 지 속성 사용](../../windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)을 참조 하세요. <> behavior 요소의 개별 설정에 대 한 자세한 내용은 `sqlWorkflowInstanceStore` [SQL 워크플로 인스턴스 저장소](../../windows-workflow-foundation/sql-workflow-instance-store.md)를 참조 하세요. Windows Server AppFabric에서는 자체적으로 지속성 저장소를 제공합니다. 자세한 내용은 [Windows Server App Fabric 지 속성](/previous-versions/appfabric/ee677272(v=azure.10))을 참조 하세요.  
  
    > [!NOTE]
    > 위의 예제에서 사용하는 구성은 단순화된 구성입니다. 자세한 내용은 [간소화 된 구성](../simplified-configuration.md) 을 참조 하세요.  
  
### <a name="to-configure-the-sql-workflow-instance-store-in-code"></a>코드에서 SQL 워크플로 인스턴스 저장소를 구성하려면  
  
1. SQL 워크플로 인스턴스 저장소의 속성은 코드를 통해 설정을 변경하는 데 사용할 수 있는 서비스 동작인 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>를 통해 구성할 수 있습니다. 다음 예제에서는 코드에서 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 동작 요소를 사용하여 SQL 워크플로 인스턴스 저장소를 구성하는 방법을 보여 줍니다.  
  
    ```csharp  
    host.Description.Behaviors.Add(new SqlWorkflowInstanceStoreBehavior  
    {  
       ConnectionString = "provider=System.Data.SqlClient;Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true",  
       InstanceEncodingOption = "GZip | None",  
       InstanceCompletionAction = "DeleteAll | DeleteNothing",  
       InstanceLockedExceptionAction = "NoRetry | SimpleRetry | AggressiveRetry",  
       HostLockRenewalPeriod = new TimeSpan(00, 00, 30),  
       RunnableInstancesDetectionPeriod = new TimeSpan(00, 00, 05)  
    });  
    ```  
  
     SQL 워크플로 인스턴스 저장소를 구성 하는 방법에 대 한 자세한 내용은 [방법: 워크플로 및 워크플로 서비스에 Sql 지 속성 사용](../../windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)을 참조 하세요. 동작 요소의 개별 설정에 대 한 자세한 내용은 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> [SQL 워크플로 인스턴스 저장소](../../windows-workflow-foundation/sql-workflow-instance-store.md)를 참조 하세요. Windows Server AppFabric에서는 자체적으로 지속성 저장소를 제공합니다. 자세한 내용은 [Windows Server App Fabric 지 속성](/previous-versions/appfabric/ee677272(v=azure.10))을 참조 하세요.  
  
    > [!NOTE]
    > 위의 예제에서 사용하는 구성은 단순화된 구성입니다. 자세한 내용은 [간소화 된 구성](../simplified-configuration.md) 을 참조 하세요.  
  
     지 속성을 프로그래밍 방식으로 구성 하는 방법에 대 한 예제는 [방법: 워크플로 및 워크플로 서비스에 지 속성 사용](../../windows-workflow-foundation/how-to-enable-persistence-for-workflows-and-workflow-services.md)을 참조 하세요.  
  
## <a name="see-also"></a>참조

- [워크플로 서비스](workflow-services.md)
- [워크플로 유지](../../windows-workflow-foundation/workflow-persistence.md)
- [지속성 개념](/previous-versions/appfabric/ee677272(v=azure.10))

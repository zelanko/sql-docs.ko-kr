---
title: 가용성 그룹 내 복제본의 가용성 모드 변경
description: T-SQL(Transact-SQL), PowerShell 또는 SQL Server Management Studio를 사용하여 Always On 가용성 그룹 내 가용성 복제본의 가용성 모드를 변경하는 방법에 대한 설명입니다.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], availability modes
ms.assetid: c4da8f25-fb1b-45a4-8bf2-195df6df634c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c17beebfd689e5e768450d92353b87f8fcfa1ae2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988595"
---
# <a name="change-the-availability-mode-of-a-replica-within-an-always-on-availability-group"></a>Always On 가용성 그룹 내 복제본의 가용성 모드 변경
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]또는 PowerShell을 사용하여 Always On 가용성 그룹의 가용성 복제본에 대한 가용성 모드를 변경하는 방법에 대해 설명합니다. 가용성 모드는 복제본이 비동기적 또는 동기적으로 커밋되는지 여부를 제어하는 복제본 속성입니다. *비동기-커밋 모드* 는 성능을 극대화하지만 가용성이 저하되며 *강제 장애 조치(failover)* 라고 하는 강제 수동 장애 조치(failover)만 지원하여 데이터가 손실될 수 있습니다. *동기-커밋 모드* 는 성능에 비해 고가용성을 강조하고 보조 복제본이 동기화되면 수동 장애 조치(failover)를 지원하고 자동 장애 조치(failover)를 선택적으로 지원합니다.  
    
##  <a name="Prerequisites"></a> 사전 요구 사항  
  
주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  

##  <a name="Permissions"></a> 사용 권한  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **가용성 그룹의 가용성 모드를 변경하려면**  
  
1.  개체 탐색기에서 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  복제본을 변경할 가용성 그룹을 클릭합니다.  
  
4.  복제본을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
5.  **가용성 복제본 속성** 대화 상자에서 **가용성 모드** 드롭 목록을 사용하여 이 복제본의 가용성 모드를 변경합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 그룹의 가용성 모드를 변경하려면**  
  
1.  주 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  다음과 같은 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) 문을 사용합니다.  
  
     ALTER AVAILABILITY GROUP *group_name* MODIFY REPLICA ON '*server_name*'  
  
     WITH ( {  
  
     AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
  
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }  
  
     } )  
  
     여기서 *group_name* 은 가용성 그룹의 이름이고 *server_name* 은 수정할 복제본을 호스트하는 서버 인스턴스의 이름입니다.  
  
    > [!NOTE]  
    >  FAILOVER_MODE = AUTOMATIC은 AVAILABILITY_MODE = SYNCHRONOUS_COMMIT을 지정한 경우에만 지원됩니다.  
  
     `AccountsAG` 가용성 그룹의 주 복제본에 입력된 다음 예는 `INSTANCE09` 서버 인스턴스에 호스팅된 복제본에 대해 가용성 및 장애 조치(failover) 모드를 동기 커밋 및 자동 장애 조치(failover)로 각각 변경합니다.  
  
    ```  
  
    ALTER AVAILABILITY GROUP AccountsAG MODIFY REPLICA ON 'INSTANCE09'  
       WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);  
    ALTER AVAILABILITY GROUP AccountsAG MODIFY REPLICA ON 'INSTANCE09'  
       WITH (FAILOVER_MODE = AUTOMATIC);  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **가용성 그룹의 가용성 모드를 변경하려면**  
  
1.  주 복제본을 호스트하는 서버 인스턴스로 디렉터리(**cd**)를 변경합니다.  
  
2.  **Set-SqlAvailabilityReplica** cmdlet을 **AvailabilityMode** 매개 변수와 함께 사용하고 필요에 따라 **FailoverMode** 매개 변수를 함께 사용합니다.  
  
     예를 들어 다음 명령은 `MyReplica` 가용성 그룹의 `MyAg` 복제본이 동기-커밋 가용성 모드를 사용하고 자동 장애 조치(failover)를 지원하도록 수정합니다.  
  
    ```  
    Set-SqlAvailabilityReplica -AvailabilityMode "SynchronousCommit" -FailoverMode "Automatic" `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 **PowerShell 환경에서** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 모드&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [장애 조치 및 장애 조치 모드&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)  
  
  

---
title: 가용성 그룹 내 복제본에 대한 세션 제한 시간 변경
description: Always On 가용성 내에서 복제본의 세션 제한 시간을 구성하는 방법을 설명합니다.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], session timeout
- session timeout [SQL Server]
ms.assetid: e23c6e06-1cd1-4d4a-9bc2-e3e06ab2933d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 49c2c6e7f607717ed9639e11d9513f486b5585ff
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207642"
---
# <a name="change-the-session-timeout-period-for-a-replica-within-an-always-on-availability-group"></a>Always On 가용성 그룹 내 복제본에 대한 세션 제한 시간 변경
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]또는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]의 PowerShell을 사용하여 Always On 가용성 복제본의 세션 제한 시간을 구성하는 방법에 대해 설명합니다. 세션 제한 시간은 가용성 복제본이 연결이 실패한 것으로 간주되기 전에 연결된 복제본에서 ping 응답을 받기 위해 기다리는 최대 시간(초)을 제어하는 복제본 속성입니다. 기본적으로 복제본은 ping 응답을 받기 위해 10초 동안 기다립니다. 이 복제본 속성은 지정된 보조 복제본과 가용성 그룹의 주 복제본 사이의 연결에만 적용됩니다. 세션 제한 시간에 대한 자세한 내용은 [AlwaysOn 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)를 참조하세요.  
  
-   **시작하기 전 주의 사항:**  
  
     [필수 구성 요소](#Prerequisites)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **세션 제한 시간을 변경하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
 제한 시간을 10초 이상으로 유지하는 것이 좋습니다. 10초 미만의 값을 설정하면 로드가 많은 시스템에서 PING을 누락하여 잘못된 실패를 선언할 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **가용성 복제본에 대한 세션 제한 시간을 변경하려면**  
  
1.  개체 탐색기에서 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  가용성 복제본을 구성할 가용성 그룹을 클릭합니다.  
  
4.  구성할 복제본을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
5.  **가용성 복제본 속성** 대화 상자에서 **세션 제한 시간(초)** 필드를 사용하여 이 복제본에 대한 세션 제한 시간(초)을 변경합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 복제본에 대한 세션 제한 시간을 변경하려면**  
  
1.  주 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  다음과 같은 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) 문을 사용합니다.  
  
     ALTER AVAILABILITY GROUP *group_name*  
  
     MODIFY REPLICA ON '*instance_name*' WITH ( SESSION_TIMEOUT =*seconds* )  
  
     여기서 *group_name* 은 가용성 그룹의 이름이고, *instance_name* 은 수정할 가용성 복제본을 호스팅하는 서버 인스턴스의 이름이고, *seconds* 는 복제본이 보조 복제본 역할을 할 때 데이터베이스에 로그를 적용하기 전에 기다리는 최소 시간(초)을 지정합니다. 기본값은 0초이며 지연 적용이 없음을 의미합니다.  
  
     `AccountsAG` 가용성 그룹의 주 복제본에 입력된 다음 예는 `15` 서버 인스턴스에 있는 복제본에 대한 세션 제한 시간 값을 `INSTANCE09` 초로 변경합니다.  
  
    ```  
    ALTER AVAILABILITY GROUP AccountsAG   
       MODIFY REPLICA ON 'INSTANCE09' WITH (SESSION_TIMEOUT = 15);  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **가용성 복제본에 대한 세션 제한 시간을 변경하려면**  
  
1.  주 복제본을 호스트하는 서버 인스턴스로 디렉터리(**cd**)를 변경합니다.  
  
2.  **Set-SqlAvailabilityReplica** cmdlet을 **SessionTimeout** 매개 변수와 함께 사용하여 지정된 가용성 복제본에 대한 세션 제한 시간(초)을 변경할 수 있습니다.  
  
     예를 들어 다음 명령은 세션 제한 시간을 15초로 설정합니다.  
  
    ```  
    Set-SqlAvailabilityReplica -SessionTimeout 15 `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 **PowerShell 환경에서** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  

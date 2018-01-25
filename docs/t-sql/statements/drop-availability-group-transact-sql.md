---
title: DROP AVAILABILITY GROUP (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_AVAILABILITY_GROUP_TSQL
- DROP AVAILABILITY GROUP
dev_langs: TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], Transact-SQL statements
- DROP AVAILABILITY GROUP statement
- Availability Groups [SQL Server], dropping
ms.assetid: c1600289-c990-454a-b279-dba0ebd5d63e
caps.latest.revision: "44"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82fdb4b104a0be0aa0d6469ccdd23f361f55618b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="drop-availability-group-transact-sql"></a>DROP AVAILABILITY GROUP(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  지정된 가용성 그룹과 모든 복제본을 제거합니다. 가용성 복제본 중 하나를 호스팅하는 서버 인스턴스가 오프라인 상태일 때 가용성 그룹을 삭제하면 나중에 서버 인스턴스가 온라인 상태가 되었을 때 서버 인스턴스에서 로컬 가용성 복제본을 삭제합니다. 가용성 그룹을 삭제하면 관련 가용성 그룹 수신기(있는 경우)도 삭제됩니다.  
  
> [!IMPORTANT]  
>  가능하면 주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있는 동안에만 가용성 그룹을 제거하세요. 주 복제본에서 가용성 그룹을 제거하면 이전 주 데이터베이스에서 변경이 허용됩니다(고가용성 보호 없이). 주 복제본을 유지 하는 보조 복제본에서 가용성 그룹을 삭제는 **RESTORING** 상태 및 변경 내용을 데이터베이스에 허용 되지 않습니다.  
  
 가용성 그룹을 삭제 하는 다른 방법에 대 한 정보를 참조 하세요. [가용성 그룹 &#40; 제거 SQL Server &#41; ](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP AVAILABILITY GROUP group_name   
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *group_name*  
 삭제할 가용성 그룹의 이름을 지정합니다.  
  
## <a name="limitations-and-recommendations"></a>제한 사항 및 권장 사항  
  
-   실행 **DROP AVAILABILITY GROUP** 서버 인스턴스에서 Always On 가용성 그룹 기능이 설정 되어 있음이 필요 합니다. 자세한 내용은 [AlwaysOn 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)를 참조하세요.  
  
-   **DROP AVAILABILITY GROUP** 트랜잭션 된 일괄 처리의 일부로 실행할 수 없습니다. 또한 식 및 변수는 지원되지 않습니다.  
  
-   가용성 그룹에 대한 올바른 보안 자격 증명이 있는 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 노드에서 가용성 그룹을 삭제할 수 있습니다. 이렇게 하면 가용성 복제본이 더 이상 없을 때 가용성 그룹을 삭제할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터에 쿼럼이 없을 때 가용성 그룹이 삭제되지 않도록 합니다. 클러스터에 쿼럼이 부족할 때 가용성 그룹을 삭제해야 하는 경우 클러스터에 저장된 메타데이터 가용성 그룹은 제거되지 않습니다. 클러스터가 쿼럼을 다시 얻은 후에는 가용성 그룹을 다시 삭제하여 WSFC 클러스터에서 제거해야 합니다.  
  
-   보조 복제본에서 **DROP AVAILABILITY GROUP** 만 응급 용 으로만 사용 해야 합니다. 이는 가용성 그룹을 삭제하면 가용성 그룹이 오프라인 상태로 전환되기 때문입니다. 보조 복제본에서 가용성 그룹을 삭제 하면 주 복제본 확인할 수 없습니다 여부는 **오프 라인** 쿼럼 손실, 강제 장애 조치 때문에 발생 한 상태 또는 **DROP AVAILABILITY GROUP**명령입니다. 주 복제본으로 전환 된 **RESTORING** 가능한 스플릿 브레인 상황을 방지 하기 위해 상태입니다. 자세한 내용은 [작동 방식: DROP AVAILABILITY GROUP 동작](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (CSS SQL Server 엔지니어 블로그)을 참조하세요.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 필요한 **ALTER AVAILABILITY GROUP** 가용성 그룹에 대 한 권한이 **CONTROL AVAILABILITY GROUP** 권한, **ALTER ANY AVAILABILITY GROUP** 권한, 또는 **제어 서버** 권한. 필요한 로컬 서버 인스턴스에서 호스팅되지 않는 가용성 그룹을 삭제 하려면 **제어 서버** 권한 또는 **제어** 해당 가용성 그룹에 대 한 권한이 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AccountsAG` 가용성 그룹을 삭제합니다.  
  
```  
DROP AVAILABILITY GROUP AccountsAG;  
```  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [작동 방식: DROP AVAILABILITY GROUP 동작](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (CSS SQL Server 엔지니어 블로그)  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [가용성 그룹 만들기&#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [가용성 그룹 &#40; 제거 SQL Server &#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
  

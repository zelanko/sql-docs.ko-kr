---
title: DROP AVAILABILITY GROUP(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_AVAILABILITY_GROUP_TSQL
- DROP AVAILABILITY GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], Transact-SQL statements
- DROP AVAILABILITY GROUP statement
- Availability Groups [SQL Server], dropping
ms.assetid: c1600289-c990-454a-b279-dba0ebd5d63e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 613841598b153dbe502f0267ed85197973bf706a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67898300"
---
# <a name="drop-availability-group-transact-sql"></a>DROP AVAILABILITY GROUP(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  지정된 가용성 그룹과 모든 복제본을 제거합니다. 가용성 복제본 중 하나를 호스팅하는 서버 인스턴스가 오프라인 상태일 때 가용성 그룹을 삭제하면 나중에 서버 인스턴스가 온라인 상태가 되었을 때 서버 인스턴스에서 로컬 가용성 복제본을 삭제합니다. 가용성 그룹을 삭제하면 관련 가용성 그룹 수신기(있는 경우)도 삭제됩니다.  
  
> [!IMPORTANT]  
>  가능하면 주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있는 동안에만 가용성 그룹을 제거하세요. 주 복제본에서 가용성 그룹을 제거하면 이전 주 데이터베이스에서 변경이 허용됩니다(고가용성 보호 없이). 보조 복제본에서 가용성 그룹을 삭제하면 주 복제본이 **RESTORING** 상태로 유지되고 데이터베이스에서 변경이 허용되지 않습니다.  
  
 가용성 그룹 삭제에 대한 자세한 내용은 [가용성 그룹 제거&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP AVAILABILITY GROUP group_name   
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *group_name*  
 삭제할 가용성 그룹의 이름을 지정합니다.  
  
## <a name="limitations-and-recommendations"></a>제한 사항 및 권장 사항  
  
-   **DROP AVAILABILITY GROUP**을 실행하려면 서버 인스턴스에서 AlwaysOn 가용성 그룹 기능을 사용하도록 설정해야 합니다. 자세한 내용은 [AlwaysOn 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)를 참조하세요.  
  
-   **DROP AVAILABILITY GROUP**을 일괄 처리의 일부로 또는 트랜잭션 내에서 실행할 수 없습니다. 또한 식 및 변수는 지원되지 않습니다.  
  
-   가용성 그룹에 대한 올바른 보안 자격 증명이 있는 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 노드에서 가용성 그룹을 삭제할 수 있습니다. 이렇게 하면 가용성 복제본이 더 이상 없을 때 가용성 그룹을 삭제할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터에 쿼럼이 없을 때 가용성 그룹이 삭제되지 않도록 합니다. 클러스터에 쿼럼이 부족할 때 가용성 그룹을 삭제해야 하는 경우 클러스터에 저장된 메타데이터 가용성 그룹은 제거되지 않습니다. 클러스터가 쿼럼을 다시 얻은 후에는 가용성 그룹을 다시 삭제하여 WSFC 클러스터에서 제거해야 합니다.  
  
-   보조 복제본에서 **DROP AVAILABILITY GROUP**은 응급용으로만 사용해야 합니다. 이는 가용성 그룹을 삭제하면 가용성 그룹이 오프라인 상태로 전환되기 때문입니다. 보조 복제본에서 가용성 그룹을 삭제하면 주 복제본에서 쿼럼 손실, 강제 장애 조치(failover) 또는 **DROP AVAILABILITY GROUP** 명령으로 인해 **OFFLINE** 상태가 발생했는지 여부를 확인할 수 없습니다. 주 복제본은 분리 장애(split-brain)가 발생하는 것을 방지하기 위해 **RESTORING** 상태로 전환됩니다. 자세한 내용은 [작동 방식: DROP AVAILABILITY GROUP 동작](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (CSS SQL Server 엔지니어 블로그)을 참조하세요.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 가용성 그룹에 대한 **ALTER AVAILABILITY GROUP** 권한, **CONTROL AVAILABILITY GROUP** permission, **ALTER ANY AVAILABILITY GROUP** 권한 또는 **CONTROL SERVER** 권한이 필요합니다. 로컬 서버 인스턴스에서 호스팅되지 않는 가용성 그룹을 삭제하려면 해당 가용성 그룹에 대한 **CONTROL SERVER** 권한이나 **CONTROL** 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AccountsAG` 가용성 그룹을 삭제합니다.  
  
```  
DROP AVAILABILITY GROUP AccountsAG;  
```  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 관련 내용  
  
-   [작동 방식: DROP AVAILABILITY GROUP 동작](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (CSS SQL Server 엔지니어 블로그)  
  
## <a name="see-also"></a>참고 항목  
 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [가용성 그룹 제거&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
  

---
title: '가용성 그룹 속성: 새 가용성 그룹(백업 기본 설정 페이지)'
description: SQL Server Management Studio의 '새 가용성 그룹 ' 마법사의 '백업 기본 설정' 페이지에 있는 다양한 속성에 대한 설명입니다.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroupproperties.backuppreferences.f1
helpviewer_keywords:
- read-only routing
ms.assetid: 65fff22d-5963-4a8c-8b31-fe9ab247a03e
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 275b48491ddf5c868e467043c57c64e0936e36d7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66761828"
---
# <a name="availability-group-properties-new-availability-group-backup-preferences-page"></a>가용성 그룹 속성: 새 가용성 그룹(백업 기본 설정 페이지)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 대화 상자를 사용하여 선택한 가용성 그룹의 백업 기본 설정을 보고 변경할 수 있습니다.  
  
 **가용성 그룹 속성을 보려면**  
  
-   [가용성 그룹 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
-   [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](~/database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="where-should-backups-occur"></a>백업 수행 위치  
 **보조 사용**  
 백업이 보조 복제본에서 수행되도록 지정합니다. 주 복제본이 유일한 온라인 복제본인 경우는 예외로, 이 경우에는 백업이 주 복제본에서 수행되어야 합니다. 이 옵션이 기본 옵션입니다.  
  
 **보조만**  
 백업이 주 복제본에서 수행되지 않도록 지정합니다. 주 복제본이 유일한 온라인 복제본인 경우에는 백업이 수행되지 않아야 합니다.  
  
 **주**  
 백업이 항상 주 복제본에서 수행되도록 지정합니다. 이 옵션은 백업이 보조 복제본에서 실행될 때 지원되지 않는 차등 백업 만들기와 같은 백업 기능이 필요한 경우에 유용합니다.  
  
 **임의의 복제본**  
 백업을 수행할 복제본을 선택할 때 백업 작업에서 가용성 복제본의 역할을 무시하도록 지정합니다. 백업 작업에서는 각 가용성 복제본의 작동 상태 및 연결 상태와 함께 백업 우선 순위 등의 기타 요인을 평가할 수 있습니다.  
  
> [!IMPORTANT]  
>  백업 기본 설정은 적용되지 않습니다. 이 기본 설정의 해석은 지정된 가용성 그룹의 데이터베이스에 대한 백업 작업으로 스크립팅하는 논리(있는 경우)에 따라 달라집니다. 자세한 내용은 [활성 보조 복제본: 보조 복제본에 백업&#40;Always On 가용성 그룹&#41;](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)을 참조하세요.  
  
## <a name="replica-backup-priorities"></a>복제본 백업 우선 순위  
 이 표는 가용성 그룹에 대한 복제본을 호스팅하는 각 서버 인스턴스의 현재 백업 우선 순위를 표시합니다. 이 표를 사용하여 하나 이상의 가용성 복제본에 대한 백업 우선 순위를 변경할 수 있습니다.  
  
 **서버 인스턴스**  
 가용성 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인스턴스 이름입니다.  
  
 **백업 우선 순위(최저 = 1, 최고 = 100)**  
 이 복제본에 대한 백업을 수행하기 위한 우선 순위를 지정하며 동일한 가용성 그룹의 다른 복제본을 기준으로 합니다. 이 값은 0에서 100  사이의 정수입니다. 1은 가장 낮은 우선 순위를 나타내고 100은 가장 높은 우선 순위를 나타냅니다. **백업 우선 순위** 가 1이면 현재 사용 가능한 더 높은 우선 순위의 가용성 복제본이 없는 경우에만 해당 가용성 복제본이 백업 수행을 위해 선택됩니다.  
  
 **복제본 제외**  
 백업 수행을 위해 이 가용성 백업을 선택하지 않으려는 경우에 선택합니다. 이 값은 예를 들어 백업을 장애 조치할 대상으로 사용하지 않을 원격 가용성 복제본의 경우에 유용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [활성 보조 복제본: 보조 복제본에 백업&#40;Always On 가용성 그룹&#41;](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)   
 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  


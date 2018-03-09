---
title: "사용 권한 또는 보안 개체 페이지 | Microsoft 문서"
ms.custom: 
ms.date: 01/07/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.common.permissions.f1
- sql13.swb.SecurableAndEffectPermissions.f1
- sql13.swb.common.columnperm.f1
- sql13.swb.availabilitygroupproperties.permission.f1
- sql13.swb.SecurableAndEffectivePermission.f1
ms.assetid: b3bf077a-bec2-4161-ac0c-460586199906
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6dc65e94e95e978d47e9cb454337a52d0a6cc622
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="permissions-or-securables-page"></a>사용 권한 또는 보안 개체 페이지
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] **사용 권한** 페이지 또는 **보안 개체** 페이지를 사용하여 보안 개체에 대한 사용 권한을 보거나 설정할 수 있습니다. 이 페이지는 여러 위치에서 열 수 있으며 페이지의 내용은 페이지를 연 방법과 페이지에 포함된 항목에 따라 조금씩 다를 수 있습니다. 페이지가 열릴 때 해당 페이지의 위쪽 표는 채워져 있거나 비어 있을 수 있습니다. 상단 표에 항목을 추가하려면 **검색**을 클릭합니다. 상단 표에서 항목을 선택한 다음 **명시적** 탭에서 적절한 사용 권한을 설정합니다. 집계된 사용 권한을 보려면 **유효** 탭을 사용합니다.  
  
 가능한 보안 개체와 보안 주체의 조합에 대한 자세한 내용은 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md) 항목에서 보안 개체별 구문 링크를 참조하세요. 자세한 내용은 [Securables](../../relational-databases/security/securables.md)을 참조하세요.  
  
## <a name="page-header"></a>페이지 머리글  
 **사용 권한** 또는 **보안 개체** 페이지의 머리글은 보안 개체나 보안 주체에 따라 달라집니다. 이 페이지의 머리글에서는 항목 이름 등 항목과 관련된 정보를 표시합니다.  
  
## <a name="upper-grid"></a>상단 표  
 상단 표에는 사용 권한을 설정할 수 있는 항목이 하나 이상 포함됩니다. 이 대화 상자에는 상단 표에 추가할 개체나 보안 주체를 선택할 수 있는 **검색** 단추가 제공됩니다. 표의 이름은 **보안 개체** 나 하나 이상의 보안 개체/보안 주체 유형을 나타낼 수 있습니다. 상단 표에 표시되는 열은 보안 주체 또는 보안 개체에 따라 달라집니다.  
  
 **이름**  
 표에 추가된 각 보안 주체 또는 보안 개체의 이름입니다.  
  
 **형식**  
 각 항목의 유형입니다.  
  
## <a name="explicit-tab"></a>명시적 탭  
 **명시적** 탭에서는 상단 표에서 선택된 보안 개체의 가능한 사용 권한을 나열합니다. 사용 권한을 구성하려면 **권한 부여** (또는 **허용**), **허용 권한 소유**및 **거부** 확인란을 선택하거나 선택 취소합니다. 모든 명시적 사용 권한에 대해 모든 옵션을 사용할 수 있는 것은 아닙니다.  
  
 **사용 권한**  
 사용 권한의 이름입니다.  
  
 **Grantor**  
 사용 권한을 부여한 보안 주체입니다.  
  
 **허용**  
 로그인에 이 사용 권한을 허용하려면 선택하고 사용 권한을 해제하려면 선택을 취소합니다.  
  
 **허용 권한 소유**  
 나열된 사용 권한에 대한 WITH GRANT 옵션 상태를 나타냅니다. 이 부분은 읽기 전용입니다. 이 사용 권한을 적용하려면 [GRANT](../../t-sql/statements/grant-transact-sql.md) 문을 사용합니다.  
  
 **거부**  
 로그인에 이 사용 권한을 거부하려면 선택하고 사용 권한을 해제하려면 선택을 취소합니다.  
  
 **열 사용 권한**  
 열(예: 테이블, 뷰, 테이블 반환 함수)을 포함하는 개체의 경우 **열 사용 권한** 단추를 누르면 **열 사용 권한** 대화 상자가 열립니다. 이 대화 상자에서 각 테이블 또는 뷰 열에 **권한 부여**, **허용**또는 **거부** 권한을 설정할 수 있습니다. 일부 개체 유형 또는 사용 권한의 경우 이 옵션을 사용할 수 없습니다.  
  
## <a name="effective-tab"></a>유효 탭  
 보안 개체와 관련된 보안 주체의 사용 권한은 여러 가지 보안 주체에 대해 설정된 사용 권한에서 가져온 것일 수 있습니다. 예를 들어 로그인에 사용 권한을 개별적으로 부여할 수 있으며 그룹 멤버로서 부여할 수도 있습니다. **유효** 탭에서는 명시적 사용 권한과 그룹 또는 역할 멤버 자격으로부터 가져온 사용 권한을 조합한 결과를 보여 줍니다. 허용 권한은 집계되며 거부 권한은 모든 허용 권한보다 우선합니다.  
  
 **사용 권한**  
 사용 권한의 이름입니다.  
  
 **열**  
 사용 권한의 영향을 받은 열의 이름입니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)   
 [SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대한 보안 센터](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  

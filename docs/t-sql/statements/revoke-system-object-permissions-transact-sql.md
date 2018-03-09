---
title: "REVOKE 시스템 개체 사용 권한 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statement, system objects
- permissions [SQL Server], system objects
ms.assetid: 84983238-dd7d-45bd-99bb-52c9d8e96a87
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 461cde90e42168333f5c2cd700c25cc1a396fabe
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="revoke-system-object-permissions-transact-sql"></a>REVOKE 시스템 개체 사용 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  보안 주체의 저장 프로시저, 확장 저장 프로시저, 함수 및 뷰와 같은 시스템 개체에 대한 권한을 취소합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
REVOKE { SELECT | EXECUTE } ON [sys.]system_object FROM principal   
```  
  
## <a name="arguments"></a>인수  
 [**sys.** ] .  
 **sys** 한정자는 카탈로그 뷰 및 동적 관리 뷰를 참조 하는 경우에 필요 합니다.  
  
 *system_object*  
 사용 권한을 취소할 개체를 지정합니다.  
  
 *보안 주체*  
 사용 권한을 취소할 보안 주체를 지정합니다.  
  
## <a name="remarks"></a>주의  
 이 문을 사용하면 특정 저장 프로시저, 확장 저장 프로시저, 테이블 반환 함수, 스칼라 함수, 뷰, 카탈로그 뷰, 호환성 뷰, INFORMATION_SCHEMA 뷰, 동적 관리 뷰 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 설치된 시스템 테이블에 대한 사용 권한을 취소할 수 있습니다. 리소스 데이터베이스에 고유한 레코드로 존재 하는 각 시스템 개체 (**mssqlsystemresource**). 리소스 데이터베이스는 읽기 전용입니다. 개체에 대 한 링크에 레코드로 표시 되는 **sys** 모든 데이터베이스의 스키마입니다.  
  
 기본 이름 확인은 정규화되지 않은 프로시저 이름을 리소스 데이터베이스로 확인합니다. 따라서는 **sys.** 한정자는 카탈로그 뷰 및 동적 관리 뷰를 지정 하는 경우에 필요 합니다.  
  
> [!CAUTION]  
>  시스템 개체에 대한 사용 권한을 취소하면 이러한 개체에 종속된 응용 프로그램이 실패합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]는 카탈로그 뷰를 사용하며 카탈로그 뷰에 대한 기본 사용 권한을 변경하면 정상적으로 작동하지 않을 수 있습니다.  
  
 트리거 및 시스템 개체의 열에 대한 사용 권한은 취소할 수 없습니다.  
  
 시스템 개체에 대한 사용 권한은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업그레이드 시 유지됩니다.  
  
 시스템 개체는 [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) 카탈로그 뷰에 표시됩니다.  
  
## <a name="permissions"></a>Permissions  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `EXECUTE`으로부터 `sp_addlinkedserver`에 대한 `public` 권한을 취소합니다.  
  
```  
REVOKE EXECUTE ON sys.sp_addlinkedserver FROM public;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.system_objects &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [sys.database_permissions&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [GRANT 시스템 개체 사용 권한 &#40; Transact SQL &#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)   
 [시스템 개체 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)  
  
  

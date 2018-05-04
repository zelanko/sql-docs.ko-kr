---
title: sys.fn_translate_permissions (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fn_translate_permissions
- sys.fn_translate_permissions_TSQL
- fn_translate_permissions
- fn_translate_permissions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permissions bitmask [SQL Server]
- sys.fn_translate_permissions function
- fn_translate_permissions function
ms.assetid: ac97121f-2bd0-4f71-8e45-42c8584edbc5
caps.latest.revision: 18
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 33aa7684e95d2fecdd9f28f497c8ca2d68ce1115
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysfntranslatepermissions-transact-sql"></a>sys.fn_translate_permissions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  SQL 추적에서 반환된 사용 권한 비트 마스크를 사용 권한 이름 테이블로 변환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_translate_permissions ( level , perms )  
```  
  
## <a name="arguments"></a>인수  
 *level*  
 사용 권한이 적용되는 보안 개체 종류입니다. *수준* 은 **nvarchar (60)** 합니다.  
  
 *perms*  
 사용 권한 열에 반환되는 비트 마스크입니다. *사용 권한을 확인 하십시오* 은 **varbinary (16)** 합니다.  
  
## <a name="returns"></a>반환 값  
 **table**  
  
## <a name="remarks"></a>주의  
 에 반환 된 값의 **사용 권한** SQL 추적의 열에서 사용 하는 비트 마스크의 정수 표현이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유효 사용 권한을 계산을 합니다. 25가지 종류의 보안 개체에는 각각 해당 숫자 값을 가진 사용 권한 집합이 있습니다. **sys.fn_translate_permissions** 이 비트 마스크 사용 권한 이름 테이블로 변환 합니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="example"></a>예제  
 다음 쿼리에서 `sys.fn_builtin_permissions` 다음 사용 하 여 및 인증서에 적용 되는 사용 권한을 표시 `sys.fn_translate_permissions` 사용 권한 비트 마스크의 결과를 반환 합니다.  
  
```  
SELECT * FROM sys.fn_builtin_permissions('CERTIFICATE');  
SELECT '0001' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0001);  
SELECT '0010' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0010);  
SELECT '0011' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0011);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [sys.server_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [sys.database_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)  
  
  

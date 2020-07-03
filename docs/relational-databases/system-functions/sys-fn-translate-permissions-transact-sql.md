---
title: sys. fn_translate_permissions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
ms.openlocfilehash: aec909b59a6e174269a14a330ad839d3e3ff4faa
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898256"
---
# <a name="sysfn_translate_permissions-transact-sql"></a>sys.fn_translate_permissions(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  SQL 추적에서 반환된 사용 권한 비트 마스크를 사용 권한 이름 테이블로 변환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_translate_permissions ( level , perms )  
```  
  
## <a name="arguments"></a>인수  
 *수준*  
 사용 권한이 적용되는 보안 개체 종류입니다. *level* 은 **nvarchar (60)** 입니다.  
  
 *perms*  
 사용 권한 열에 반환되는 비트 마스크입니다. *perms* 는 **varbinary (16)** 입니다.  
  
## <a name="returns"></a>반환  
 **table**  
  
## <a name="remarks"></a>설명  
 SQL 추적의 **사용 권한** 열에 반환 되는 값은에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유효 사용 권한을 계산 하는 데 사용 하는 비트 마스크의 정수 표현입니다. 25가지 종류의 보안 개체에는 각각 해당 숫자 값을 가진 사용 권한 집합이 있습니다. **fn_translate_permissions** 는이 비트 마스크를 사용 권한 이름 테이블로 변환 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="example"></a>예제  
 다음 쿼리에서는를 사용 하 여 `sys.fn_builtin_permissions` 인증서에 적용 되는 사용 권한을 표시 한 다음를 사용 하 여 `sys.fn_translate_permissions` 사용 권한 비트 마스크의 결과를 반환 합니다.  
  
```  
SELECT * FROM sys.fn_builtin_permissions('CERTIFICATE');  
SELECT '0001' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0001);  
SELECT '0010' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0010);  
SELECT '0011' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0011);  
```  
  
## <a name="see-also"></a>참고 항목  
 [권한 &#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [server_permissions &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [sys.database_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)  
  
  

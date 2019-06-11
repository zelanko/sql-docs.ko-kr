---
title: sys.sql_feature_restrictions (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/07/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sql_sql_feature_restrictions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_feature_restrictions catalog view
author: vainolo
ms.author: arib
manager: tomerw
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b583afef9f52da7801384d4a7a9c76deaf8d4ee4
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822680"
---
# <a name="syssqlfeaturerestrictions-transact-sql"></a>sys.sql_feature_restrictions (Transact SQL)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

데이터베이스의 모든 제한에 대 한 하나의 행을 반환 합니다.
  
| 열 이름 | 데이터 형식 | Description |
|-------------|-----------|-------------|
| class       | nvarchar(128) | 제한이 적용 되는 개체의 클래스 |
| 개체(object)      | nvarchar(256) | 제한이 적용 되는 개체의 이름 |
| 기능     | nvarchar(128) | 제한 된 기능 |
  
## <a name="remarks"></a>Remarks

현재 다음과 같은 기능이 제한 될 수 있습니다.

| 기능          | Description |
|------------------|-------------|
| N'ErrorMessages' | 제한, 오류 메시지 내에서 사용자 데이터가 마스킹됩니다. |
| N'Waitfor'       | 제한, 지연 없이 명령이 즉시 반환 됩니다. |
  
## <a name="permissions"></a>사용 권한

실행 보안 주체 있어야를 `CONTROL` 데이터베이스에 대 한 권한이 있습니다.
  
## <a name="see-also"></a>관련 항목

 [기능 제한 사항](../../relational-databases/security/feature-restrictions.md)

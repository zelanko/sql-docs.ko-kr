---
description: DROP WORKLOAD 분류자(Transact-SQL)
title: DROP WORKLOAD 분류자(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD CLASSIFIER
- WORKLOAD_CLASSIFIER_TSQL
- DROP_WORKLOAD_CLASSIFIER_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD CLASSIFIER statement
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 3382c3b63180cbccb091442820ed99d7882382d1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88496746"
---
# <a name="drop-workload-classifier-transact-sql"></a>DROP WORKLOAD CLASSIFIER(Transact-SQL)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

기존 사용자 정의 작업 관리 분류자를 삭제합니다.  요청이 실행 중이거나 일시 중단 상태의 요청 큐가 있는 경우 해당 분류가 유지되고 분류자를 즉시 삭제할 수 있습니다. 중요도가 다른 분류자를 삭제하고 다시 생성해도 이미 분류된 요청에는 영향을 주지 않습니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>구문  

```syntaxsql
DROP WORKLOAD CLASSIFIER classifier_name;
```

## <a name="arguments"></a>인수

*classifier_name*  
워크로드 분류자를 식별하는 이름을 지정합니다.
  
## <a name="permissions"></a>사용 권한

CONTROL DATABASE 권한이 필요합니다.  
  
## <a name="examples"></a>예

다음 예제에서는 `wgcELTROLE`라는 작업 분류자를 삭제합니다.  

```sql
DROP WORKLOAD CLASSIFIER wgcELTRole;
```

> [!NOTE]
> 일치하는 분류자 없이 제출된 요청은 기본 작업 그룹으로 분류됩니다.  기본 작업 그룹은 smallrc 리소스 클래스입니다.
  
## <a name="see-also"></a>참고 항목

[CREATE WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-classifier-transact-sql.md)</br>
[SQL Data Warehouse 작업 분류](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)

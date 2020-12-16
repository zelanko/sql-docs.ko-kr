---
description: DROP EXTERNAL RESOURCE POOL(Transact-SQL)
title: DROP EXTERNAL RESOURCE POOL(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: machine-learning-services
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL RESOURCE POOL
- DROP_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL RESOURCE POOL statement
ms.assetid: e2fa01bd-96ff-4ea9-bb08-6cb6b6adf68c
author: dphansen
ms.author: davidph
manager: cgronlund
ms.openlocfilehash: 5dc0bbd4ed86ad0c114b8dd6e66b1d4c8a2a87cc
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476614"
---
# <a name="drop-external-resource-pool-transact-sql"></a>DROP EXTERNAL RESOURCE POOL(Transact-SQL)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

외부 프로세스에 대한 리소스를 정의하는 데 사용된 Resource Governor 외부 리소스 풀을 삭제합니다. 

::: moniker range="=sql-server-2016||>=sql-server-linux-ver15"
[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]에서 [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]의 경우 외부 풀은 `rterm.exe`, `BxlServer.exe`, 이들에 의해 생성된 기타 프로세스를 제어합니다.
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15"
[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]의 경우 외부 풀은 `rterm.exe`, `python.exe`, `BxlServer.exe` 및 이들에 의해 생성된 기타 프로세스를 제어합니다.
::: moniker-end

외부 리소스 풀은 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)를 사용하여 만들어지고 [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)를 사용하여 수정됩니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
DROP EXTERNAL RESOURCE POOL pool_name  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수

*pool_name*  
삭제될 외부 리소스 풀 이름입니다.  
  
## <a name="remarks"></a>설명

작업 그룹이 들어 있으면 해당 외부 리소스 풀을 삭제할 수 없습니다.  

리소스 관리자 기본 풀 또는 내부 풀을 삭제할 수 없습니다.  

DDL 문을 실행할 경우 리소스 관리자 상태에 대해 잘 알고 있는 것이 좋습니다. 자세한 내용은 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)를 참조하세요.  

## <a name="permissions"></a>사용 권한

`CONTROL SERVER` 권한이 필요합니다.  

## <a name="examples"></a>예

다음 예에서는 `ex_pool`이라는 외부 리소스 풀을 삭제합니다.  

```sql
DROP EXTERNAL RESOURCE POOL ex_pool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  

## <a name="see-also"></a>참고 항목

+ [외부 스크립트 설정 서버 구성 옵션](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)
+ [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)
+ [ALTER EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
+ [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)
+ [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)

---
description: ISJSON(Transact-SQL)
title: ISJSON(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2020
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ISJSON
- ISJSON_TSQL
helpviewer_keywords:
- ISJSON function
- JSON, validating
ms.assetid: c836f3d3-3e17-44ae-92bf-f341918896c3
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017
ms.openlocfilehash: 49d1bcd94ed12e0b9bb22e63018b0867f680dd41
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464304"
---
# <a name="isjson-transact-sql"></a>ISJSON(Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  문자열에 유효한 JSON이 포함되어 있는지 테스트합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
ISJSON ( expression )  
```  
  
## <a name="arguments"></a>인수
 *expression*  
 테스트할 문자열입니다.  
  
## <a name="return-value"></a>반환 값  
 문자열에 유효한 JSON이 포함되어 있으면 1을 반환하고 그렇지 않으면 0을 반환합니다. *expression* 이 null이면 null을 반환합니다.  
  
 오류를 반환하지 않습니다.  
  
## <a name="remarks"></a>설명  
 **ISJSON** 은 동일한 수준에서 키의 고유성을 확인하지 않습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="example-1"></a>예 1  
다음 예제에서는 매개 변수 값 `@param`에 유효한 JSON이 포함되어 있으면 조건부로 명령문 블록을 실행합니다.  
  
```sql  
DECLARE @param <data type>
SET @param = <value>

IF (ISJSON(@param) > 0)  
BEGIN  
     -- Do something with the valid JSON value of @param.  
END
```  
  
### <a name="example-2"></a>예제 2  
다음 예제는 `json_col` 열에 유효한 JSON이 포함된 행을 반환합니다.  
  
```sql  
SELECT id, json_col
FROM tab1
WHERE ISJSON(json_col) > 0 
```  
  
## <a name="see-also"></a>참고 항목  
 [JSON 데이터&#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  

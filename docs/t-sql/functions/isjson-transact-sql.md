---
title: ISJSON (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISJSON
- ISJSON_TSQL
helpviewer_keywords:
- ISJSON function
- JSON, validating
ms.assetid: c836f3d3-3e17-44ae-92bf-f341918896c3
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9b641847387801097bce59e78cf75255cc7217be
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="isjson-transact-sql"></a>ISJSON (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  문자열에 유효한 JSON이 포함 되어 있는지 테스트 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
ISJSON ( expression )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 테스트할 문자열입니다.  
  
## <a name="return-value"></a>반환 값  
 문자열에 유효한 JSON; 포함 되어 있으면 1 반환 그렇지 않으면 0을 반환합니다. 경우 null을 반환 *식* null입니다.  
  
 오류를 반환 하지 않습니다.  
  
## <a name="remarks"></a>주의  
 **ISJSON** 같은 수준에 키의 고유성을 확인 하지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="example-1"></a>예제 1  
다음 예제에서는 문 블록 조건부로 경우 실행 매개 변수 값은 `@param` 유효한 JSON이 포함 되어 있습니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [JSON 데이터 &#40; SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  


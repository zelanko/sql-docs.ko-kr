---
title: CONCAT_WS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CONCAT_WS
- CONCAT_WS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_WS function
ms.assetid: f1375fd7-a2fd-48bf-922a-4f778f0deb1f
caps.latest.revision: 5
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 171d063e746393709629720dae40eb207d45d584
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="concatws-transact-sql"></a>CONCAT_WS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

첫 번째 인수에 지정된 구분 기호를 사용하여 다양한 개수의 인수를 연결합니다. (`CONCAT_WS`는 *구분 기호를 이용한 연결*을 나타냅니다.)

##  <a name="syntax"></a>구문   
```sql
CONCAT_WS ( separator, argument1, argument1 [, argumentN]… ) 
```

## <a name="arguments"></a>인수   
구분 기호  
모든 문자 형식(`nvarchar`, `varchar`, `nchar` 또는 `char`)의 식입니다.

argument1, argument2, argument*N*  
모든 형식의 식입니다.

## <a name="return-types"></a>반환 형식
문자열입니다. 길이와 형식은 입력에 따라 다릅니다.

## <a name="remarks"></a>Remarks   
`CONCAT_WS`는 다양한 개수의 문자열 인수를 가져와 첫 번째 인수를 구분 기호로 사용하여 단일 문자열로 연결합니다. 구분 기호 하나와 최소 두 개의 인수가 필요하며, 그렇지 않은 경우 오류가 발생합니다. 모든 인수는 문자열 형식으로 암시적으로 변환된 다음, 연결됩니다. 

문자열에 대한 암시적 변환은 데이터 형식 변환에 대한 기존 규칙을 따릅니다. 동작 및 데이터 형식 변환에 대한 자세한 내용은 [CONCAT(Transact-SQL)](../../t-sql/functions/concat-transact-sql.md)를 참조하십시오.

### <a name="treatment-of-null-values"></a>NULL 값 처리

`CONCAT_WS`는 `SET CONCAT_NULL_YIELDS_NULL {ON|OFF}` 설정을 무시합니다.

모든 인수가 null인 경우에는 `varchar(1)` 형식의 빈 문자열이 반환됩니다. 

연결 중에는 Null 값이 무시되며 구분 기호를 추가하지 않습니다. 이 경우 두 번째 주소 필드와 같이 대부분 빈 값이 포함된 문자열을 연결하는 일반적인 시나리오가 됩니다. 예 B를 참조하십시오.

구분 기호를 사용하여 null 값을 포함해야 하는 시나리오인 경우 `ISNULL` 함수를 사용하는 예제 C를 참조하십시오.

## <a name="examples"></a>예   

### <a name="a--concatenating-values-with-separator"></a>1.  구분 기호를 사용하여 값 연결
다음 예는 `- `로 값을 구분하여 sys.databases 테이블의 세 열을 연결합니다.   

```sql
SELECT CONCAT_WS( ' - ', database_id, recovery_model_desc, containment_desc) AS DatabaseInfo
FROM sys.databases;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

|DatabaseInfo |  
|---------|
|1 - SIMPLE - NONE |
|2 - SIMPLE - NONE |
|3 - FULL - NONE |
|4 - SIMPLE - NONE |


### <a name="b--skipping-null-values"></a>2.  NULL 값 유지
다음 예는 인수 목록의 `NULL` 값을 무시합니다.

```sql
SELECT CONCAT_WS(',','1 Microsoft Way', NULL, NULL, 'Redmond', 'WA', 98052) AS Address;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
Address
------------   
1 Microsoft Way,Redmond,WA,98052
```

### <a name="c--generating-csv-file-from-table"></a>3.  테이블에서 CSV 파일 생성
다음 예는 쉼표를 구분 기호로 사용하며 열로 구분된 값 형식의 결과에 캐리지 리턴 문자를 추가합니다.

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, recovery_model_desc, containment_desc), char(13)) AS DatabaseInfo
FROM sys.databases
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
DatabaseInfo
------------   
1,SIMPLE,NONE
2,SIMPLE,NONE
3,FULL,NONE 
4,SIMPLE,NONE 
```

CONCAT_WS는 열에서 NULL 값을 무시합니다. 일부 열에서 null을 허용하는 경우 `ISNULL` 함수로 래핑하고 다음 예와 같이 기본 값을 제공합니다.

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, ISNULL(recovery_model_desc,''), ISNULL(containment_desc,'N/A')), char(13)) AS DatabaseInfo
FROM sys.databases;
```

## <a name="see-also"></a>관련 항목:
 [CONCAT&#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [FORMATMESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME&#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE&#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE&#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG&#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE&#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF&#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE&#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  


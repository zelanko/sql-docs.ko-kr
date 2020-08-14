---
title: CONCAT_WS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/25/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- CONCAT_WS
- CONCAT_WS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_WS function
ms.assetid: f1375fd7-a2fd-48bf-922a-4f778f0deb1f
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7b952b51c6171bf22590403452e7b17899459de0
ms.sourcegitcommit: b80364e31739d7b08cc388c1f83bb01de5dd45c1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/04/2020
ms.locfileid: "87564936"
---
# <a name="concat_ws-transact-sql"></a>CONCAT_WS(Transact-SQL)
[!INCLUDE [sqlserver2017-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2017-asdb-asdbmi-asa.md)]

이 함수는 둘 이상의 문자열 값을 엔드투엔드 방식으로 연결하거나 조인한 결과 문자열을 반환합니다. 첫 번째 함수 인수에 지정된 구분 기호와 연결된 해당 문자열 값을 구분합니다. (`CONCAT_WS`는 *구분 기호를 이용한 연결*을 나타냅니다.)

##  <a name="syntax"></a>구문   
```syntaxsql
CONCAT_WS ( separator, argument1, argument2 [, argumentN]... )
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
‘구분 기호’ 모든 문자 형식의 식(`char`, `nchar`, `nvarchar` 또는 `varchar`).

‘인수1, 인수2, 인수N’ 모든 형식의 식. `CONCAT_WS` 함수에는 2개 이상, 254개 이하의 인수가 필요합니다.

## <a name="return-types"></a>반환 형식
길이와 형식이 입력에 따라 달라지는 문자열 값입니다.

## <a name="remarks"></a>설명   
`CONCAT_WS`는 가변 개수의 문자열 인수를 가져와서 단일 문자열로 연결(또는 조인)합니다. 첫 번째 함수 인수에 지정된 구분 기호와 연결된 해당 문자열 값을 구분합니다. `CONCAT_WS`에는 구분 기호 인수 및 최소 다른 두 개의 문자열 값 인수가 필요합니다. 그렇지 않으면 `CONCAT_WS`에서 오류가 발생합니다. `CONCAT_WS`는 병합하기 전에 모든 인수를 문자열 형식으로 암시적으로 변환합니다. 

문자열에 대한 암시적 변환은 데이터 형식 변환에 대한 기존 규칙을 따릅니다. 동작 및 데이터 형식 변환에 대한 자세한 내용은 [CONCAT(Transact-SQL)](../../t-sql/functions/concat-transact-sql.md)를 참조하세요.

### <a name="treatment-of-null-values"></a>NULL 값 처리

`CONCAT_WS`는 `SET CONCAT_NULL_YIELDS_NULL {ON|OFF}` 설정을 무시합니다.

`CONCAT_WS`가 모두 NULL 값인 인수를 받으면 varchar(1) 형식의 빈 문자열을 반환합니다.

`CONCAT_WS`은 연결 중 Null 값을 무시하고 Null 값 사이에 구분 기호를 추가하지 않습니다. 따라서 `CONCAT_WS`은 "빈" 값(예: 두 번째 주소 필드)이 있을 수 있는 문자열의 연결을 깨끗하게 처리할 수 있습니다. 자세한 내용은 예제 B를 참조하세요.

시나리오에 구분 기호로 구분된 null 값이 포함되는 경우 `ISNULL` 함수를 사용합니다. 자세한 내용은 예제 C를 참조하세요.

## <a name="examples"></a>예   

### <a name="a--concatenating-values-with-separator"></a>A.  구분 기호를 사용하여 값 연결
이 예제에서는 `-`로 값을 구분하여 sys.databases 테이블의 세 열을 연결합니다.   

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


### <a name="b--skipping-null-values"></a>B.  NULL 값 유지
이 예제에서는 인수 목록의 `NULL` 값을 무시합니다.

```sql
SELECT CONCAT_WS(',','1 Microsoft Way', NULL, NULL, 'Redmond', 'WA', 98052) AS Address;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
Address
------------   
1 Microsoft Way,Redmond,WA,98052
```

### <a name="c--generating-csv-file-from-table"></a>C.  테이블에서 CSV 파일 생성
이 예제에서는 `,` 쉼표를 구분 기호로 사용하고, 결과 집합의 열로 구분된 값 형식으로 `char(13)` 캐리지 반환 문자를 추가합니다.

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

CONCAT_WS는 열에서 NULL 값을 무시합니다. `ISNULL` 함수를 사용하여 Null 허용 열을 래핑하고, 기본값을 제공합니다. 자세한 내용은 이 예제를 참조하세요.

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, ISNULL(recovery_model_desc,''), ISNULL(containment_desc,'N/A')), char(13)) AS DatabaseInfo
FROM sys.databases;
```

## <a name="see-also"></a>참고 항목
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


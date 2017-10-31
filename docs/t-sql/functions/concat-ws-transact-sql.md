---
title: CONCAT_WS (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 377db445118e55f1bdeec220f1e6701e9f89706c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="concatws-transact-sql"></a>CONCAT_WS (Transact SQL)
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

첫 번째 인수에 지정 된 구분 기호와 함께 가변 개수의 인수를 연결 합니다. (`CONCAT_WS` 나타냅니다 *구분 기호로 concatenate*.)

##  <a name="syntax"></a>구문   
```sql
CONCAT_WS ( separator, argument1, argument1 [, argumentN]… ) 
```

## <a name="arguments"></a>인수   
구분 기호  
모든 문자 형식의 식 (`nvarchar`, `varchar`, `nchar`, 또는 `char`).

인수 1, 인수 2, 인수*N*  
모든 유형의 식이입니다.

## <a name="return-types"></a>반환 형식
문자열입니다. 길이 형식 입력에 따라 달라 집니다.

## <a name="remarks"></a>주의   
`CONCAT_WS`인수의 가변 수를 사용 하 고 첫 번째 인수를 사용 하 여 구분 기호로 단일 문자열로 연결 합니다. 구분 기호가 두 개의 인수; 최소 필요합니다. 그렇지 않으면 오류가 발생 합니다. 모든 인수 문자열 형식으로 암시적으로 변환 됩니다 되었고 연결 됩니다. 

문자열에 대한 암시적 변환은 데이터 형식 변환에 대한 기존 규칙을 따릅니다. 동작 및 데이터 형식 변환에 대 한 자세한 내용은 참조 [CONCAT (Transact SQL)](../../t-sql/functions/concat-transact-sql.md)합니다.

### <a name="treatment-of-null-values"></a>NULL 값의 처리

`CONCAT_WS`무시 된 `SET CONCAT_NULL_YIELDS_NULL {ON|OFF}` 설정 합니다.

모든 인수가 null, 빈 문자열 형식의 경우 `varchar(1)` 반환 됩니다. 

Null 값을 연결 하는 동안 무시 되 고 구분 기호를 추가 하지 않습니다. 종종 두 번째 주소 필드와 같은 빈 값을 포함 하는 문자열을 연결 하는 일반적인 시나리오를 지원 합니다. 예 2를 참조 하십시오.

예 3를 사용 하 여 시나리오에는 구분 기호로 포함 되도록 null 값이 필요한 경우 참조는 `ISNULL` 함수입니다.

## <a name="examples"></a>예   

### <a name="a--concatenating-values-with-separator"></a>1.  구분 기호 값을 연결한
다음 예제에서는 연결 세 테이블의 열은 sys.databases 사용 하 여 값을 구분 하는 `- `합니다.   

```sql
SELECT CONCAT_WS( ' - ', database_id, recovery_model_desc, containment_desc) AS DatabaseInfo
FROM sys.databases;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

|DatabaseInfo |  
|---------|
|1-단순-없음 |
|2-단순-없음 |
|3-전체-없음 |
|4-단순-없음 |


### <a name="b--skipping-null-values"></a>2.  NULL 값을 건너뛰는 중
다음 예제에서는 무시 `NULL` 인수 목록에는 값입니다.

```sql
SELECT CONCAT_WS(',','1 Microsoft Way', NULL, NULL, 'Redmond', 'WA', 98052) AS Address;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
Address
------------   
1 Microsoft Way,Redmond,WA,98052
```

### <a name="c--generating-csv-file-from-table"></a>3.  테이블에서 CSV 파일을 생성합니다.
다음 예제에서는 구분 기호로 쉼표를 사용 하 고 결과적으로 열 구분 된 값 형식을 캐리지 리턴 문자를 추가 합니다.

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

CONCAT_WS 열에서 NULL 값을 무시 합니다. 일부 열이 null을 허용, 줄이 사용 하 여 `ISNULL` 작동 하 고 다음 예제에서와 같은 기본 값을 제공 합니다.

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, ISNULL(recovery_model_desc,''), ISNULL(containment_desc,'N/A')), char(13)) AS DatabaseInfo
FROM sys.databases;
```

## <a name="see-also"></a>참고 항목
[문자열 함수 (Transact SQL)](../../t-sql/functions/string-functions-transact-sql.md)  
[CONCAT (Transact SQL)](../../t-sql/functions/concat-transact-sql.md)      



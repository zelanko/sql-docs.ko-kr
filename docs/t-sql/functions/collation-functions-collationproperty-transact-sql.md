---
title: COLLATIONPROPERTY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLLATIONPROPERTY_TSQL
- COLLATIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], properties
- COLLATIONPROPERTY function
ms.assetid: f5029e74-a1db-4f69-b0f5-5ee920c3311d
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 166a85e5fe33a95cd8a36f221c2a774e4a0a9fb2
ms.contentlocale: ko-kr
ms.lasthandoff: 10/24/2017

---
# <a name="collation-functions---collationproperty-transact-sql"></a>데이터 정렬 함수-COLLATIONPROPERTY (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지정된 데이터 정렬의 속성을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
COLLATIONPROPERTY( collation_name , property )  
```  
  
## <a name="arguments"></a>인수  
*데이터 정렬 이름*  
데이터 정렬의 이름입니다. *데이터 정렬 이름* 은 **nvarchar (128)**, 기본값은 없습니다.
  
*속성*  
데이터 정렬의 속성입니다. *속성* 은 **varchar (128)**, 이며 다음 값 중 하나를 사용할 수 있습니다.
  
|속성 이름|Description|  
|---|---|
|**CodePage**|데이터 정렬의 유니코드가 아닌 코드 페이지입니다. 참조 하십시오 [부록 G DBCS/유니코드 매핑 테이블](https://msdn.microsoft.com/en-us/library/cc194886.aspx) 및 [부록 H 코드 페이지](https://msdn.microsoft.com/en-us/library/cc195051.aspx) 에 이러한 값을 변환 하 고 해당 문자 매핑을 확인 합니다.|  
|**LCID**|데이터 정렬의 Windows LCID입니다. 참조 하십시오 [LCID 구조](https://msdn.microsoft.com/en-us/library/cc233968.aspx) 이러한 값을 변환 (변환 해야 합니다 `VARBINARY` 첫 번째).|  
|**ComparisonStyle**|데이터 정렬의 Windows 비교 스타일입니다. 모든 이진 데이터 정렬에 대 한 0 반환 합니다 (둘 다 `_BIN` 및 `_BIN2`) 모든 속성은 중요 한 경우 뿐만 아니라 합니다. 비트 마스크 값:<br /><br /> 대/소문자 무시: 1<br /><br /> 악센트 무시: 2<br /><br /> 일본어가 나 무시: 65536<br /><br /> 전자/반자 무시: 131072|  
|**버전**|데이터 정렬 ID의 버전 필드에서 파생된 데이터 정렬 버전입니다. 0에서 3 사이 정수 값을 반환 합니다.<br /><br /> 이름에 "140"를 사용한 데이터 정렬은 3을 반환합니다.<br /><br /> 데이터 정렬 이름에 "100"으로 2를 반환 합니다.<br /><br /> 이름에 "90"를 사용한 데이터 정렬은 1을 반환 합니다.<br /><br /> 다른 모든 데이터 정렬은 0을 반환합니다.|  
  
## <a name="return-types"></a>반환 형식
**sql_variant**
  
## <a name="examples"></a>예  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage')  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
## <a name="see-also"></a>참고 항목
[sys.fn_helpcollations&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
  
  



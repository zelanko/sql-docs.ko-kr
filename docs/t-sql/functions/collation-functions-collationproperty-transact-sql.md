---
description: 데이터 정렬 - COLLATIONPROPERTY(Transact-SQL)
title: COLLATIONPROPERTY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f2b4678d8c33ed7cc83bcefcdef13c91cf550086
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478754"
---
# <a name="collation-functions---collationproperty-transact-sql"></a>데이터 정렬 - COLLATIONPROPERTY(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 함수는 지정된 데이터 정렬의 요청된 속성을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
COLLATIONPROPERTY( collation_name , property )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*collation_name*  
데이터 정렬의 이름입니다. *collation_name* 인수는 **nvarchar(128)** 데이터 형식이며 기본값이 없습니다.
  
*property*  
데이터 정렬 속성입니다. *property* 인수는 **varchar(128)** 데이터 형식이며, 다음 값 중 하나일 수 있습니다.
  
|속성 이름|Description|  
|---|---|
|**CodePage**|데이터 정렬의 유니코드가 아닌 코드 페이지입니다. 이는 **varchar** 데이터에 사용되는 문자 집합입니다. 이러한 값을 변환하고 해당 문자 매핑을 확인하려면 [부록 G DBCS/유니코드 매핑 표](/previous-versions/cc194886(v=msdn.10)) 및 [부록 H 코드 페이지](/previous-versions/cc195051(v=msdn.10))를 참조하세요.<br /><br />기본 데이터 형식: **int**|  
|**LCID**|데이터 정렬의 Windows 로캘 ID입니다. 이는 정렬 및 비교 규칙에 사용되는 문화권입니다. 이러한 값을 변환하려면 [LCID 구조](/openspecs/windows_protocols/ms-lcid/63d3d639-7fd2-4afb-abbe-0d5b5551eef8)를 참조하세요(먼저 **varbinary** 로 변환해야 함).<br /><br />기본 데이터 형식: **int**|  
|**ComparisonStyle**|데이터 정렬의 Windows 비교 스타일입니다. 모든 이진 데이터 정렬((\_BIN) 및 (\_BIN2) 모두 해당)의 경우와 모든 속성((\_CS\_AS\_KS\_WS), (\_CS\_AS\_KS\_WS\_SC) 및 (\_CS\_AS\_KS\_WS\_VSS))이 대/소문자를 구분하는 경우 0을 반환합니다. 비트 마스크 값:<br /><br /> 대/소문자 무시: 1<br /><br /> 악센트 무시: 2<br /><br /> 일본어 가나 무시: 65536<br /><br /> 전자/반자 무시: 131072<br /><br /> 참고: 비교 동작에 영향을 주는 경우에도 \_VSS(변형 선택기 구분) 옵션은 이 값으로 표시되지 않습니다.<br /><br />기본 데이터 형식: **int**|  
|**Version**|데이터 정렬의 버전입니다. 0 ~ 3 사이의 값을 반환합니다.<br /><br /> 이름에 “140”이 있는 데이터 정렬은 3을 반환합니다.<br /><br /> 이름에 “100”이 있는 데이터 정렬은 2를 반환합니다.<br /><br /> 이름에 “90”이 있는 데이터 정렬은 1을 반환합니다.<br /><br /> 다른 모든 데이터 정렬은 0을 반환합니다.<br /><br />기본 데이터 형식: **tinyint**|  
  
## <a name="return-types"></a>반환 형식
**sql_variant**
  
## <a name="examples"></a>예  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
1252   
```  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage')  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
1252   
```  
  
## <a name="see-also"></a>참고 항목
[sys.fn_helpcollations&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
  

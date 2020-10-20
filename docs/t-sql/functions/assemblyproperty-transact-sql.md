---
description: ASSEMBLYPROPERTY(Transact-SQL)
title: ASSEMBLYPROPERTY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASSEMBLYPROPERTY_TSQL
- ASSEMBLYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- ASSEMBLYPROPERTY statement
- assemblies [CLR integration], properties
ms.assetid: cf03d1b1-724c-48bf-a8df-3fe2586b150a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 722d6c4b2130ad51c2249f083691233524d3834c
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037086"
---
# <a name="assemblyproperty-transact-sql"></a>ASSEMBLYPROPERTY(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 기능은 어셈블리의 속성에 대한 정보를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
ASSEMBLYPROPERTY('assembly_name', 'property_name')  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*assembly_name*  
어셈블리의 이름입니다.
  
*property_name*  
정보를 검색할 속성의 이름입니다. *property_name*은 다음 값 중 하나일 수 있습니다.
  
|값|Description|  
|---|---|
|**CultureInfo**|어셈블리의 로캘입니다.|  
|**PublicKey**|어셈블리의 공개 키 또는 공개 키 토큰입니다.|  
|**MvID**|어셈블리의 완전한 컴파일러 생성 버전 식별 번호입니다.|  
|**VersionMajor**|네 부분으로 된 버전의 어셈블리 식별 번호에서 주 구성 요소(첫 번째 부분)입니다.|  
|**VersionMinor**|네 부분으로 된 버전의 어셈블리 식별 번호에서 부 구성 요소(두 번째 부분)입니다.|  
|**VersionBuild**|네 부분으로 된 버전의 어셈블리 식별 번호에서 빌드 구성 요소(세 번째 부분)입니다.|  
|**VersionRevision**|네 부분으로 된 버전의 어셈블리 식별 번호에서 개정 구성 요소(네 번째 부분)입니다.|  
|**SimpleName**|어셈블리의 간략한 이름입니다.|  
|**아키텍처**|어셈블리의 프로세서 아키텍처입니다.|  
|**CLRName**|어셈블리의 단순한 이름, 버전 번호, culture, 공개 키, 아키텍처 등을 인코딩하는 정식 문자열입니다. 이 값은 CLR(공용 언어 런타임) 측에서 어셈블리를 고유하게 식별합니다.|  
  
## <a name="return-type"></a>반환 형식
**sql_variant**
  
## <a name="examples"></a>예  
이 예에서는 `HelloWorld` 어셈블리가 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 등록되어 있다고 가정합니다. 자세한 내용은 [Hello World 예제](/previous-versions/sql/sql-server-2016/ff878250(v=sql.130))를 참조하세요.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ASSEMBLYPROPERTY ('HelloWorld' , 'PublicKey');  
```  
  
## <a name="see-also"></a>참고 항목
[CREATE ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
[DROP ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)
  

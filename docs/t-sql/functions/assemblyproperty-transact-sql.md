---
title: ASSEMBLYPROPERTY (Transact SQL) | Microsoft Docs
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
- ASSEMBLYPROPERTY_TSQL
- ASSEMBLYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- ASSEMBLYPROPERTY statement
- assemblies [CLR integration], properties
ms.assetid: cf03d1b1-724c-48bf-a8df-3fe2586b150a
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9556834a173302e19358f5333b059d7b4f902519
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="assemblyproperty-transact-sql"></a>ASSEMBLYPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

어셈블리의 속성에 대한 정보를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
ASSEMBLYPROPERTY('assembly_name', 'property_name')  
```  
  
## <a name="arguments"></a>인수  
*assembly_name*  
어셈블리의 이름입니다.
  
*property_name*  
정보를 검색할 속성의 이름입니다. *property_name* 다음 값 중 하나일 수 있습니다.
  
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
다음 예에서는 `HelloWorld` 어셈블리가 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]데이터베이스에 등록되어 있다고 가정합니다. 자세한 내용은 참조 [Hello World 예제](http://msdn.microsoft.com/library/fed6c358-f5ee-4d4c-9ad6-089778383ba7)합니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ASSEMBLYPROPERTY ('HelloWorld' , 'PublicKey');  
```  
  
## <a name="see-also"></a>참고 항목
[CREATE ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
[DROP ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)
  
  


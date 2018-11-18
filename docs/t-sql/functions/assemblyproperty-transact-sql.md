---
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 468364203d169e6987322edbb99f0b2cea863fec
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51696004"
---
# <a name="assemblyproperty-transact-sql"></a>ASSEMBLYPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

이 기능은 어셈블리의 속성에 대한 정보를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
ASSEMBLYPROPERTY('assembly_name', 'property_name')  
```  
  
## <a name="arguments"></a>인수  
*assembly_name*  
어셈블리의 이름입니다.
  
*property_name*  
정보를 검색할 속성의 이름입니다. *property_name*은 다음 값 중 하나일 수 있습니다.
  
|값|설명|  
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
이 예에서는 `HelloWorld` 어셈블리가 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 등록되어 있다고 가정합니다. 자세한 내용은 [Hello World 예제](https://msdn.microsoft.com/library/fed6c358-f5ee-4d4c-9ad6-089778383ba7)를 참조하세요.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ASSEMBLYPROPERTY ('HelloWorld' , 'PublicKey');  
```  
  
## <a name="see-also"></a>관련 항목:
[CREATE ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
[DROP ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)
  
  

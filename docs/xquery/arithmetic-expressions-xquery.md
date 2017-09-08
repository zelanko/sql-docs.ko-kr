---
title: "산술 식 (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6ba5c642195f1049f7df59a0fa14ef666eec4bfe
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="arithmetic-expressions-xquery"></a>산술 식(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  모든 산술 연산자가 지원을 제외 하 고 **idiv**합니다. 다음 예에서는 산술 연산자의 기본 사용 방법을 보여 줍니다.  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 때문에 **idiv** 가 사용 하는 솔루션은 지원 되지 않습니다는 **xs:integer()** 생성자:  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 산술 연산자로부터의 결과 유형은 입력 값의 유형을 기반으로 합니다. 피연산자의 유형이 다른 경우 필요한 경우 둘 중 하나 또는 둘 모두가 유형 계층에 따라 공통된 기본 유형으로 캐스팅됩니다. 형식 계층 구조에 대 한 정보를 참조 하십시오. [XQuery의 형식 캐스트 규칙](../xquery/type-casting-rules-in-xquery.md)합니다.  
  
 두 연산의 숫자 기본 유형이 다르면 숫자 유형 승격이 발생합니다. 예를 들어 추가 **xs: decimal** 에 **xs: double** double로는 먼저 10 진수 값을 변경 합니다. 그런 다음 추가 작업을 수행하여 double 값을 만듭니다.  
  
 다른 피연산자의 숫자 기본 유형 또는 형식화 되지 않은 원자 값은 캐스팅 **xs: double** 다른 피연산자 피연산자도 형식화 되지 않은 경우.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   산술 연산자에 대 한 인수는 숫자 형식 이어야 하거나 **untypedAtomic**합니다.  
  
-   에 대 한 작업 **xs: integer** 값 형식의 값을 결과가 **xs: decimal** 대신 **xs: integer**합니다.  
  
  

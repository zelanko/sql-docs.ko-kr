---
title: 산술 식 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3d970209b71a842aa1c78b2f7dd0db980e0ce73e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47642651"
---
# <a name="arithmetic-expressions-xquery"></a>산술 식(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  모든 산술 연산자가 지원를 제외한 **idiv**합니다. 다음 예에서는 산술 연산자의 기본 사용 방법을 보여 줍니다.  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 때문에 **idiv** 는 지원 되지 않는 솔루션은 사용 하는 **xs:integer()** 생성자:  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 산술 연산자로부터의 결과 유형은 입력 값의 유형을 기반으로 합니다. 피연산자의 유형이 다른 경우 필요한 경우 둘 중 하나 또는 둘 모두가 유형 계층에 따라 공통된 기본 유형으로 캐스팅됩니다. 형식 계층 구조에 대 한 정보를 참조 하세요 [XQuery의 형식 캐스트 규칙](../xquery/type-casting-rules-in-xquery.md)합니다.  
  
 두 연산의 숫자 기본 유형이 다르면 숫자 유형 승격이 발생합니다. 예를 들어, 추가 **xs: decimal** 에 **xs: double** double는 먼저 10 진수 값을 변경 합니다. 그런 다음 추가 작업을 수행하여 double 값을 만듭니다.  
  
 형식화 되지 않은 원자 값 또는 다른 피연산자의 숫자 기본 형식으로 캐스팅 됩니다 **xs: double** 도 다른 피연산자가 형식화 된 경우.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   산술 연산자에 대 한 인수가 숫자 형식 이어야 하거나 **untypedAtomic**합니다.  
  
-   연산은 **xs: integer** 형식의 값에서 값 발생 **xs: decimal** 대신 **xs: integer**.  
  
  

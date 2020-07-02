---
title: 산술 식 (XQuery) | Microsoft Docs
description: XQuery의 산술 식과 지원 되는 산술 연산자에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
author: rothja
ms.author: jroth
ms.openlocfilehash: 548fde62cf6f07d2e31a68b7f702baa4bd9f916a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85643660"
---
# <a name="arithmetic-expressions-xquery"></a>산술 식(XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  **Idiv**를 제외 하 고 모든 산술 연산자가 지원 됩니다. 다음 예에서는 산술 연산자의 기본 사용 방법을 보여 줍니다.  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 **Idiv** 는 지원 되지 않으므로 솔루션은 **xs: integer ()** 생성자를 사용 하는 것입니다.  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 산술 연산자로부터의 결과 유형은 입력 값의 유형을 기반으로 합니다. 피연산자의 유형이 다른 경우 필요한 경우 둘 중 하나 또는 둘 모두가 유형 계층에 따라 공통된 기본 유형으로 캐스팅됩니다. 형식 계층 구조에 대 한 자세한 내용은 [XQuery의 형식 캐스팅 규칙](../xquery/type-casting-rules-in-xquery.md)을 참조 하세요.  
  
 두 연산의 숫자 기본 유형이 다르면 숫자 유형 승격이 발생합니다. 예를 들어 xs: **double** 에 **xs: decimal** 을 추가 하면 먼저 10 진수 값을 double로 변경 합니다. 그런 다음 추가 작업을 수행하여 double 값을 만듭니다.  
  
 형식화 되지 않은 원자 값은 다른 피연산자의 숫자 기본 형식으로 캐스팅 되거나 다른 피연산자도 형식화 되지 않은 경우 **xs: double** 로 캐스팅 됩니다.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   산술 연산자에 대 한 인수는 숫자 형식 또는 **untypedAtomic**이어야 합니다.  
  
-   Xs: **integer** 값에 대 한 연산은 xs: **integer**대신 **xs: decimal** 형식의 값을 반환 합니다.  
  
  

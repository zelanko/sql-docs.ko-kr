---
title: floor 함수 (XQuery) | Microsoft Docs
description: 인수 값 보다 크지 않은 소수 부분이 없는 가장 큰 숫자를 반환 하는 XQuery floor () 함수에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- floor function [XQuery]
- fn:floor function
ms.assetid: 4ace57dd-b66e-4b60-a2b9-a1b0f1a0831d
author: rothja
ms.author: jroth
ms.openlocfilehash: cf7943cbcef462dbdf73e72357f28e4f4e3eb20d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85724213"
---
# <a name="numeric-values-functions---floor"></a>숫자 값 함수 - floor
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  해당 인수의 값보다 크지 않은 소수가 포함되지 않은 가장 큰 수를 반환합니다. 인수가 빈 시퀀스이면 빈 시퀀스가 반환됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:floor ($arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 함수가 적용되는 번호입니다.  
  
## <a name="remarks"></a>설명  
 *$Arg* 형식이 세 가지 숫자 기본 유형인 **xs: float**, **xs: double**또는 **xs: decimal**중 하나 이면 반환 형식은 *$arg* 형식과 같습니다. *$Arg* 형식이 숫자 형식 중 하나에서 파생 된 형식인 경우 반환 형식은 기본 숫자 형식입니다.  
  
 Fn: floor, fn: 천장 또는 fn: round 함수에 대 한 입력이 **xdt: untypedAtomic**형식화 되지 않은 데이터 이면 암시적으로 **xs: double**로 캐스팅 됩니다. 다른 유형을 사용하면 정적 오류가 발생합니다.  
  
## <a name="examples"></a>예제  
 이 항목에서는 AdventureWorks 예제 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
 **Floor ()** xquery 함수에 대 한 [천장 함수 (XQuery)](../xquery/numeric-values-functions-ceiling.md) 에서 작업 예제를 사용할 수 있습니다. 쿼리의 **상한은 ()** 함수를 **floor ()** 함수로 바꾸어야 합니다.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **Floor ()** 함수는 모든 정수 값을 xs: decimal로 매핑합니다.  
  
## <a name="see-also"></a>참고 항목  
 [천장 함수 &#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)   
 [round 함수 &#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)   
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

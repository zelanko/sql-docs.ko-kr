---
title: "round 함수 (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- fn:round function
- round function [XQuery]
ms.assetid: 320b572f-bd5b-4055-95a6-dec5718c0041
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a579433be42dbd22db3467cbf72a9bb4de623a51
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="numeric-values-functions---round"></a>반올림할 숫자 값 함수-
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  소수 부분이 없고 인수에 가장 근접한 숫자를 반환합니다. 이와 같은 숫자가 하나 이상 있는 경우 양의 무한수에 가장 근접한 숫자가 반환됩니다. 예를 들어  
  
 2.5에서는 인수가 **round ()** 3을 반환 합니다.  
  
 인수가 2.4999, **round ()** 2를 반환 합니다.  
  
 인수가-2.5 이면 **round ()** -2를 반환 합니다.  
  
 인수가 빈 시퀀스 이면 **round ()** 빈 시퀀스를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:round ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 함수가 적용되는 번호입니다.  
  
## <a name="remarks"></a>주의  
 경우 유형의 *$arg* 세 가지 숫자 기본 형식 중 하나인 **xs: float**, **xs: double**, 또는 **xs: decimal**, 반환 형식이 동일는 *$arg* 유형입니다. 경우 유형의 *$arg* 숫자 형식 중 하나에서 파생 된 형식이 반환 형식은 기본 숫자 형식입니다.  
  
 경우에 대 한 입력은 **fn: floor**, **fn: ceiling**, 또는 **fn: round** 함수는 **xdt: untypedatomic**, 형식화 되지 않은 데이터를 암시적으로 캐스팅 됩니다에 **xs: double**합니다.  
  
 다른 유형을 사용하면 정적 오류가 발생합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
 작업 예제를 사용할 수 있습니다는 [ceiling 함수 (XQuery)](../xquery/numeric-values-functions-ceiling.md) 에 대 한는 **round ()** XQuery 함수입니다. 수행 해야 하는 대체는 **ceiling ()** 쿼리에서 함수는 **round ()** 함수입니다.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **round ()** 함수 정수 값을 xs: decimal에 매핑합니다.  
  
-   **round ()** -0.5e0와-0e0 사이의 xs: double 및 xs: float 값의 함수-0e0 대신 0 e 0으로 매핑됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [floor 함수 &#40; XQuery &#41;](../xquery/numeric-values-functions-floor.md)   
 [ceiling 함수 &#40; XQuery &#41;](../xquery/numeric-values-functions-ceiling.md)  
  
  

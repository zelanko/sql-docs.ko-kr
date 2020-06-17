---
title: round 함수 (XQuery) | Microsoft Docs
description: 지정 된 인수와 가장 가까운 소수 부분이 없는 숫자를 반환 하는 XQuery 함수 round ()에 대해 알아봅니다.
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
- fn:round function
- round function [XQuery]
ms.assetid: 320b572f-bd5b-4055-95a6-dec5718c0041
author: rothja
ms.author: jroth
ms.openlocfilehash: 53686410ff6dc36af5cc50a0210e33e9a1fb6ad1
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84881481"
---
# <a name="numeric-values-functions---round"></a>숫자 값 함수 - round
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  소수 부분이 없고 인수에 가장 근접한 숫자를 반환합니다. 이와 같은 숫자가 하나 이상 있는 경우 양의 무한수에 가장 근접한 숫자가 반환됩니다. 다음은 그 예입니다.  
  
 인수가 2.5 인 경우 **round ()** 는 3을 반환 합니다.  
  
 인수가 2.4999 인 경우 **round ()** 는 2를 반환 합니다.  
  
 인수가-2.5 인 경우 **round ()** 는-2를 반환 합니다.  
  
 인수가 빈 시퀀스인 경우 **round ()** 는 빈 시퀀스를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:round ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 함수가 적용되는 번호입니다.  
  
## <a name="remarks"></a>설명  
 *$Arg* 형식이 세 가지 숫자 기본 유형인 **xs: float**, **xs: double**또는 **xs: decimal**중 하나 이면 반환 형식은 *$arg* 형식과 같습니다. *$Arg* 형식이 숫자 형식 중 하나에서 파생 된 형식인 경우 반환 형식은 기본 숫자 형식입니다.  
  
 **Fn: floor**, **fn: 천장**또는 **fn: round** 함수에 대 한 입력이 **xdt: untypedAtomic**형식화 되지 않은 데이터 이면 암시적으로 **xs: double**로 캐스팅 됩니다.  
  
 다른 유형을 사용하면 정적 오류가 발생합니다.  
  
## <a name="examples"></a>예제  
 이 항목에서는 AdventureWorks 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
 **Round ()** xquery 함수에 대 한 [천장 함수 (XQuery)](../xquery/numeric-values-functions-ceiling.md) 에서 작업 예제를 사용할 수 있습니다. 쿼리의 **상한은 ()** 함수를 **round ()** 함수로 바꾸어야 합니다.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **Round ()** 함수는 정수 값을 xs: decimal로 매핑합니다.  
  
-   -0.5 e0 및-0e0 사이의 xs: double 및 xs: float 값의 **round ()** 함수는-0e0 대신 0e0에 매핑됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [floor 함수 &#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [천장 함수 &#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)  
  
  

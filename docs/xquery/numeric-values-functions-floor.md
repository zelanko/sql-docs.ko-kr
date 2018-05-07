---
title: floor 함수 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- floor function [XQuery]
- fn:floor function
ms.assetid: 4ace57dd-b66e-4b60-a2b9-a1b0f1a0831d
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4f0ec0cc8b4a6e958767c805a5bc7ec68678f753
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="numeric-values-functions---floor"></a>숫자 값 함수-floor
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  해당 인수의 값보다 크지 않은 소수가 포함되지 않은 가장 큰 수를 반환합니다. 인수가 빈 시퀀스이면 빈 시퀀스가 반환됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:floor ($arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 함수가 적용되는 번호입니다.  
  
## <a name="remarks"></a>주의  
 경우 유형의 *$arg* 세 가지 숫자 기본 형식 중 하나인 **xs: float**, **xs: double**, 또는 **xs: decimal**, 반환 형식이 동일는 *$arg* 유형입니다. 경우 유형의 *$arg* 숫자 형식 중 하나에서 파생 된 형식이 반환 형식은 기본 숫자 형식입니다.  
  
 Fn: floor, fn: ceiling 또는 fn: round 함수에 대 한 입력 이면 **xdt: untypedatomic**, 형식화 되지 않은 데이터를 암시적으로 캐스팅 됩니다에 **xs: double**합니다. 다른 유형을 사용하면 정적 오류가 발생합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** AdventureWorks 예제 데이터베이스에 열을 입력 합니다.  
  
 작업 예제를 사용할 수 있습니다는 [ceiling 함수 (XQuery)](../xquery/numeric-values-functions-ceiling.md) 에 대 한는 **floor ()** XQuery 함수입니다. 수행 해야 하는 대체는 **ceiling ()** 쿼리에서 함수는 **floor ()** 함수입니다.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **floor ()** 함수 모든 정수 값을 xs: decimal에 매핑합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ceiling 함수 &#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)   
 [round 함수 &#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)   
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

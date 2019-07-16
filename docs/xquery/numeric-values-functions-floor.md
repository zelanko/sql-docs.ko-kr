---
title: floor 함수 (XQuery) | Microsoft Docs
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
ms.openlocfilehash: 1c27e432dc258b4d2b9d21bfe0ab28df8ee5b510
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946533"
---
# <a name="numeric-values-functions---floor"></a>숫자 값 함수 - floor
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  해당 인수의 값보다 크지 않은 소수가 포함되지 않은 가장 큰 수를 반환합니다. 인수가 빈 시퀀스이면 빈 시퀀스가 반환됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:floor ($arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 함수가 적용되는 번호입니다.  
  
## <a name="remarks"></a>설명  
 경우 유형의 *$arg* 세 가지 숫자 기본 유형 중 하나인 **xs: float**, **xs: double**, 또는 **xs: decimal**, 반환 형식은 동일 합니다 *$arg* 형식입니다. 경우 유형의 *$arg* 숫자 유형 중 하나에서 파생 된 형식인 반환 형식은 기본 숫자 형식입니다.  
  
 Fn: floor, fn: ceiling 또는 fn: round 함수에 대 한 입력 이면 **xdt: untypedatomic**, 형식화 되지 않은 데이터를 암시적으로 캐스팅 됩니다 하 **xs: double**합니다. 다른 유형을 사용하면 정적 오류가 발생합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예를 제공 **xml** AdventureWorks 예제 데이터베이스의 열을 입력 합니다.  
  
 사용할 수 있는 작업 예제는 [ceiling 함수 (XQuery)](../xquery/numeric-values-functions-ceiling.md) 에 대 한는 **floor ()** XQuery 함수. 대체는 수행 해야 모든는 **ceiling ()** 사용 하 여 쿼리에 함수를 **floor ()** 함수.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   합니다 **floor ()** 함수 모든 정수 값을 xs: decimal로 매핑합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ceiling 함수 &#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)   
 [round 함수 &#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)   
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

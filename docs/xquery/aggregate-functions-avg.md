---
title: avg 함수 (XQuery) | Microsoft Docs
description: 지정 된 숫자 시퀀스의 평균을 반환 하는 XQuery 함수 avg ()에 대해 알아봅니다.
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:avg function
- avg function [XQuery]
ms.assetid: 0cc60267-3c56-4a88-8ad7-bb07f0255d56
author: rothja
ms.author: jroth
ms.openlocfilehash: af6e9ba832a267c2f85bbe2f44f087399384179c
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914669"
---
# <a name="aggregate-functions---avg"></a>집계 함수 - avg
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  일련의 숫자의 평균을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:avg($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 평균이 계산되는 일련의 원자 값입니다.  
  
## <a name="remarks"></a>설명  
 **Avg ()** 에 전달 되는 원자화 된 값의 모든 형식은 세 가지 기본 제공 숫자 기본 형식 또는 Xdt: untypedAtomic의 하위 형식 이어야 합니다. 이러한 유형은 혼합 유형일 수 없습니다. xdt:untypedAtomic 유형의 값은 xs:double로 취급됩니다. **Avg ()** 의 결과는 Xdt: untypedAtomic의 경우 xs: double과 같이 전달 된 유형의 기본 유형을 수신 합니다.  
  
 입력이 정적으로 비어 있으면 비어 있다는 것이 유추되어 정적 오류가 발생합니다.  
  
 **Avg ()** 함수는 계산 된 숫자의 평균을 반환 합니다. 예를 들어:  
  
 **sum(** *$arg* **) div count(** *$arg* **)**  
  
 *$Arg* 빈 시퀀스인 경우 빈 시퀀스가 반환 됩니다.  
  
 Xdt: untypedAtomic 값을 xs: double로 캐스팅할 수 없는 경우 값은 *$arg*입력 시퀀스에서 무시 됩니다.  
  
 다른 모든 경우 함수는 정적 오류를 반환합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 AdventureWorks 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
### <a name="a-using-the-avg-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-in-which-labor-hours-are-greater-than-the-average-for-all-work-center-locations"></a>A. avg() XQuery 함수를 사용하여 제조 과정에서 근로 시간이 모든 작업 센터 위치의 평균보다 큰 경우의 작업 센터 위치 찾기  
 [Min 함수 (XQuery)](../xquery/aggregate-functions-min.md) 에 제공 된 쿼리를 다시 작성 하 여 **avg ()** 함수를 사용할 수 있습니다.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **Avg ()** 함수는 모든 정수를 xs: decimal로 매핑합니다.  
  
-   Xs: duration 유형의 값에 대 한 **avg ()** 함수는 지원 되지 않습니다.  
  
-   여러 기본 유형 범위의 유형이 혼합된 시퀀스는 지원되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

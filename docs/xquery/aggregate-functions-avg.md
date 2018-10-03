---
title: avg 함수 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:avg function
- avg function [XQuery]
ms.assetid: 0cc60267-3c56-4a88-8ad7-bb07f0255d56
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b9a8ef18dca7bf61907219d4a09882c62deb2712
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47833361"
---
# <a name="aggregate-functions---avg"></a>집계 함수 - avg
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  일련의 숫자의 평균을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:avg($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 평균이 계산되는 일련의 원자 값입니다.  
  
## <a name="remarks"></a>Remarks  
 에 전달 되는 세분화 된 값의 모든 형식을 **avg ()** 세 가지 기본 제공 숫자 기준 유형 이거나 xdt: untypedatomic 중 정확히 하나의 하위 해야 합니다. 이러한 유형은 혼합 유형일 수 없습니다. xdt:untypedAtomic 유형의 값은 xs:double로 취급됩니다. 결과인 **avg ()** xdt: untypedatomic의 경우 xs: double 처럼 전달 된 유형의 기본 유형을 수신 합니다.  
  
 입력이 정적으로 비어 있으면 비어 있다는 것이 유추되어 정적 오류가 발생합니다.  
  
 합니다 **avg ()** 함수 계산 된 숫자의 평균을 반환 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
 **sum(** *$arg* **) div count(** *$arg* **)**  
  
 하는 경우 *$arg* 가 빈 시퀀스, 빈 시퀀스가 반환 됩니다.  
  
 입력된 시퀀스에서 값이 무시 됩니다 xdt: untypedatomic 값을 xs: double로 캐스팅할 수 없습니다, 하는 경우 *$arg*합니다.  
  
 다른 모든 경우 함수는 정적 오류를 반환합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예를 제공 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-using-the-avg-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-in-which-labor-hours-are-greater-than-the-average-for-all-work-center-locations"></a>1. avg() XQuery 함수를 사용하여 제조 과정에서 근로 시간이 모든 작업 센터 위치의 평균보다 큰 경우의 작업 센터 위치 찾기  
 제공한 쿼리를 다시 작성할 수 있습니다 [min 함수 (XQuery)](../xquery/aggregate-functions-min.md) 사용 하 여 **avg ()** 함수입니다.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   합니다 **avg ()** 함수 모든 정수를 xs: decimal로 매핑합니다.  
  
-   합니다 **avg ()** xs: duration 유형의 값에는 함수가 지원 되지 않습니다.  
  
-   여러 기본 유형 범위의 유형이 혼합된 시퀀스는 지원되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

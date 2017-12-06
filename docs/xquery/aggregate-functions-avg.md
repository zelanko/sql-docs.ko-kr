---
title: "avg 함수 (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: XML
helpviewer_keywords:
- fn:avg function
- avg function [XQuery]
ms.assetid: 0cc60267-3c56-4a88-8ad7-bb07f0255d56
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4bdc56fac5ad9b478a1b24ec06bc97d6ad2aece9
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="aggregate-functions---avg"></a>Avg 집계 함수-
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  일련의 숫자의 평균을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:avg($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 평균이 계산되는 일련의 원자 값입니다.  
  
## <a name="remarks"></a>주의  
 에 전달 되는 세분화 된 값의 모든 형식 **avg ()** 세 가지 기본 제공 숫자 기준 유형 이거나 xdt: untypedatomic 중 정확히 하나의 하위 있어야 합니다. 이러한 유형은 혼합 유형일 수 없습니다. xdt:untypedAtomic 유형의 값은 xs:double로 취급됩니다. 결과 **avg ()** xdt: untypedatomic의 경우 xs: double 처럼 전달 유형의 기본 유형을 수신 합니다.  
  
 입력이 정적으로 비어 있으면 비어 있다는 것이 유추되어 정적 오류가 발생합니다.  
  
 **avg ()** 함수 계산 된 숫자의 평균을 반환 합니다. 예를 들어  
  
 **sum (** *$arg* **) div count (** *$arg* **)**  
  
 경우 *$arg* 이 빈 시퀀스인 경우 빈 시퀀스가 반환 됩니다.  
  
 Xdt: untypedatomic 값을 xs: double로 캐스팅할 수 없습니다, 값은 입력된 시퀀스에서 무시 됩니다 *$arg*합니다.  
  
 다른 모든 경우 함수는 정적 오류를 반환합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-using-the-avg-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-in-which-labor-hours-are-greater-than-the-average-for-all-work-center-locations"></a>1. avg() XQuery 함수를 사용하여 제조 과정에서 근로 시간이 모든 작업 센터 위치의 평균보다 큰 경우의 작업 센터 위치 찾기  
 에 제공 된 쿼리를 다시 작성할 수 [min 함수 (XQuery)](../xquery/aggregate-functions-min.md) 사용 하 여 **avg ()** 함수입니다.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **avg ()** 함수는 모든 정수를 xs: decimal에 매핑합니다.  
  
-   **avg ()** xs: duration 유형의 값에는 함수가 지원 되지 않습니다.  
  
-   여러 기본 유형 범위의 유형이 혼합된 시퀀스는 지원되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

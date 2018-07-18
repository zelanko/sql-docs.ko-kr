---
title: max 함수 (XQuery) | Microsoft Docs
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
- max function [XQuery]
- fn:max function
ms.assetid: 5ee625c0-044a-4cda-b210-02b64e619d65
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a53b02bc682bf7b3c918a02d5a16dc326ca3a594
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37983391"
---
# <a name="aggregate-functions---max"></a>집계 함수-max
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  원자 값의 시퀀스에서 반환 *$arg*를 하나씩 값의 다른 모든 보다 큽니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:max($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 최대값을 반환할 원자 값의 시퀀스입니다.  
  
## <a name="remarks"></a>Remarks  
 에 전달 되는 세분화 된 값의 유형도 **max ()** 동일한 기본 유형의 하위 유형 이어야 합니다. 기본 허용 되는 형식은 지 원하는 형식을 합니다 **gt** 작업 합니다. 이러한 유형에는 3가지 기본 제공 숫자 기본 유형, 날짜/시간 기본 유형, xs:string, xs:boolean 및 xdt:untypedAtomic이 포함됩니다. xdt:untypedAtomic 유형의 값이 xs:double로 캐스팅됩니다. 이러한 종류의 혼합 없거나 다른 형식의 다른 값을 전달 하는 경우 정적 오류가 발생 합니다.  
  
 결과인 **max ()** xdt: untypedatomic의 경우 xs: double 처럼 전달 된 유형의 기본 유형을 수신 합니다. 입력이 정적으로 비어 있으면 비어 있다는 것이 유추되어 정적 오류가 발생합니다.  
  
 합니다 **max ()** 함수는 입력된 시퀀스의 다른 보다 큰 시퀀스의 값 중 하나를 반환 합니다. xs:string 값의 경우 기본 Unicode Codepoint Collation이 사용됩니다. 입력된 시퀀스에서 값을 xdt: untypedatomic 값을 xs: double로 캐스팅할 수 없습니다, 하는 경우 무시 됩니다 *$arg*합니다. 입력이 동적으로 계산된 빈 시퀀스이면 빈 시퀀스가 반환됩니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예를 제공 **xml** 유형 열에는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스입니다.  
  
### <a name="a-using-the-max-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-that-have-the-most-labor-hours"></a>1. max() XQuery 함수를 사용하여 제조 프로세스에서 근무 시간이 가장 많은 작업 센터 위치 찾기  
 제공 된 쿼리 [min 함수 (XQuery)](../xquery/aggregate-functions-min.md) 사용 하도록 다시 작성할 수 있습니다 합니다 **max ()** 함수입니다.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   합니다 **max (**) 함수는 모든 정수를 xs: decimal에 매핑합니다.  
  
-   합니다 **max ()** xs: duration 유형의 값에는 함수가 지원 되지 않습니다.  
  
-   여러 기본 유형 범위의 유형이 혼합된 시퀀스는 지원되지 않습니다.  
  
-   데이터 정렬을 제공하는 구문 옵션은 지원되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

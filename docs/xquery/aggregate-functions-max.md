---
title: max 함수 (XQuery) | Microsoft Docs
description: 시퀀스에서 다른 항목 보다 큰 값을 가진 한 항목을 반환 하는 XQuery max () 함수에 대해 알아봅니다.
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
- max function [XQuery]
- fn:max function
ms.assetid: 5ee625c0-044a-4cda-b210-02b64e619d65
author: rothja
ms.author: jroth
ms.openlocfilehash: caf736973d288a89bec287aff3cb1c1993e3b0dc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726781"
---
# <a name="aggregate-functions---max"></a>집계 함수 - max
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  원자 값의 시퀀스에서 반환 *$arg*, 값이 다른 항목 보다 큰 항목 하나를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:max($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 최대값을 반환할 원자 값의 시퀀스입니다.  
  
## <a name="remarks"></a>설명  
 **Max ()** 에 전달 되는 원자화 된 값의 모든 형식은 동일한 기본 형식의 하위 형식 이어야 합니다. 허용 되는 기본 형식은 **gt** 작업을 지 원하는 형식입니다. 이러한 유형에는 3가지 기본 제공 숫자 기본 유형, 날짜/시간 기본 유형, xs:string, xs:boolean 및 xdt:untypedAtomic이 포함됩니다. xdt:untypedAtomic 유형의 값이 xs:double로 캐스팅됩니다. 이러한 형식이 혼합 되어 있거나 다른 형식의 다른 값이 전달 되 면 정적 오류가 발생 합니다.  
  
 **Max ()** 의 결과는 Xdt: untypedAtomic의 경우 xs: double과 같이 전달 된 유형의 기본 유형을 수신 합니다. 입력이 정적으로 비어 있으면 비어 있다는 것이 유추되어 정적 오류가 발생합니다.  
  
 **Max ()** 함수는 시퀀스에서 입력 시퀀스의 다른 값 보다 큰 하나의 값을 반환 합니다. xs:string 값의 경우 기본 Unicode Codepoint Collation이 사용됩니다. Xdt: untypedAtomic 값을 xs: double로 캐스팅할 수 없는 경우 값은 *$arg*입력 시퀀스에서 무시 됩니다. 입력이 동적으로 계산된 빈 시퀀스이면 빈 시퀀스가 반환됩니다.  
  
## <a name="examples"></a>예제  
 이 항목에서는 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 합니다.  
  
### <a name="a-using-the-max-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-that-have-the-most-labor-hours"></a>A. max() XQuery 함수를 사용하여 제조 프로세스에서 근무 시간이 가장 많은 작업 센터 위치 찾기  
 [Min 함수 (XQuery)](../xquery/aggregate-functions-min.md) 에 제공 된 쿼리를 다시 작성 하 여 **max ()** 함수를 사용할 수 있습니다.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **Max (**) 함수는 모든 정수를 xs: decimal로 매핑합니다.  
  
-   Xs: duration 형식의 값에 대 한 **max ()** 함수는 지원 되지 않습니다.  
  
-   여러 기본 유형 범위의 유형이 혼합된 시퀀스는 지원되지 않습니다.  
  
-   데이터 정렬을 제공하는 구문 옵션은 지원되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

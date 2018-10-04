---
title: Null 허용 여부 및 3 개의 값 논리 비교 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- precision [CLR integration]
- overflow detections [CLR integration]
- null values [CLR integration]
- three-value logic comparisons [CLR integration]
- data types [CLR integration]
- SqlBoolean data type
ms.assetid: 13da4c7f-1010-4b2d-a63c-c69b6bfd96f1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4f1b4823db4ae961024ac2a786c948d8349f31be
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48160946"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Null 허용 여부 및 3개의 값 논리 비교
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 대해 잘 아는 경우 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]의 `System.Data.SqlTypes` 네임스페이스와 의미 체계 및 전체 자릿수가 유사하다는 것을 알 수 있습니다. 그러나 약간의 차이가 있으며 이 항목에서는 이러한 차이 중 가장 중요한 점에 대해 설명합니다.  
  
## <a name="null-values"></a>NULL 값  
 기본 CLR(공용 언어 런타임) 데이터 형식과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 간의 주된 차이점은 전자에서는 NULL 값을 허용하지 않는 반면 후자에서는 완전한 NULL 의미 체계를 제공한다는 것입니다.  
  
 비교는 NULL 값의 영향을 받습니다. 두 값 x와 y를 비교할 때 x 또는 y 중 하나가 NULL이면 일부 논리적 비교가 true 또는 false가 아닌 UNKNOWN으로 계산됩니다.  
  
## <a name="sqlboolean-data-type"></a>SqlBoolean 데이터 형식  
 `System.Data.SqlTypes` 네임스페이스에서는 이 3값 논리를 나타내기 위해 `SqlBoolean` 형식을 제공합니다. `SqlTypes` 간을 비교하면 `SqlBoolean` 값 형식이 반환됩니다. UNKNOWN 값은 `SqlBoolean` 형식의 null 값으로 표현됩니다. `IsTrue` 형식의 값을 확인하기 위해 `IsFalse`, `IsNull` 및 `SqlBoolean` 속성이 제공됩니다.  
  
## <a name="operations-functions-and-null-values"></a>연산, 함수 및 NULL 값  
 모든 산술 연산자 (+,-, \*, /, %), 비트 연산자 (~, &, 및 |), 대부분의 함수 인수 또는 피연산자가 있을 경우 NULL을 반환 하 고 `SqlTypes` null입니다. `IsNull` 속성은 항상 true 또는 false 값을 반환합니다.  
  
## <a name="precision"></a>전체 자릿수  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR의 decimal 데이터 형식에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 숫자 및 decimal 데이터 형식의 최대값과는 다른 최대값이 있습니다. 또한 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR decimal 데이터 형식에는 최대 전체 자릿수가 있는 것으로 간주됩니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]용 CLR의 `SqlDecimal`은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 decimal 데이터 형식과 동일한 전체 자릿수, 소수 자릿수 및 의미 체계를 제공합니다.  
  
## <a name="overflow-detection"></a>오버플로 검색  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR에서 아주 큰 두 수를 더하면 예외가 throw되지 않습니다. 대신 확인 연산자를 사용하지 않는 경우 반환된 결과가 음의 정수로 "래핑"될 수 있습니다. `System.Data.SqlTypes`에서는 모든 오버플로 및 언더플로 오류와 0으로 나누기 오류에 대해 예외가 throw됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [.NET Framework의 SQL Server 데이터 형식](sql-server-data-types-in-the-net-framework.md)  
  
  

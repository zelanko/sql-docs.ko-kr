---
title: Null 허용 여부 및 3 값 논리 비교 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- precision [CLR integration]
- overflow detections [CLR integration]
- null values [CLR integration]
- three-value logic comparisons [CLR integration]
- data types [CLR integration]
- SqlBoolean data type
ms.assetid: 13da4c7f-1010-4b2d-a63c-c69b6bfd96f1
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cf4eb07bb901fa9657f5533847b5a07334526bc2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Null 허용 여부 및 3개의 값 논리 비교
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  에 대해 잘 알고 있다면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식, 비슷한 의미 체계와 정확 하 게 찾을 수 있습니다는 **System.Data.SqlTypes** 네임 스페이스에는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]합니다. 그러나 약간의 차이가 있으며 이 항목에서는 이러한 차이 중 가장 중요한 점에 대해 설명합니다.  
  
## <a name="null-values"></a>NULL 값  
 기본 CLR(공용 언어 런타임) 데이터 형식과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 간의 주된 차이점은 전자에서는 NULL 값을 허용하지 않는 반면 후자에서는 완전한 NULL 의미 체계를 제공한다는 것입니다.  
  
 비교는 NULL 값의 영향을 받습니다. 두 값 x와 y를 비교할 때 x 또는 y 중 하나가 NULL이면 일부 논리적 비교가 true 또는 false가 아닌 UNKNOWN으로 계산됩니다.  
  
## <a name="sqlboolean-data-type"></a>SqlBoolean 데이터 형식  
 **System.Data.SqlTypes** 네임 스페이스 소개는 **SqlBoolean** 를이 3 개의 값 논리를 나타내는 형식입니다. 간을 비교 **SqlTypes** 반환는 **SqlBoolean** 값 형식입니다. 알 수 없는 값의 null 값으로 표현 되는 **SqlBoolean** 유형입니다. 속성 **IsTrue**, **IsFalse**, 및 **IsNull** 의 값을 확인 하는 제공 되는 **SqlBoolean** 유형입니다.  
  
## <a name="operations-functions-and-null-values"></a>연산, 함수 및 NULL 값  
 모든 산술 연산자 (+,-, \*, /, %), 비트 연산자 (~, &, 및 |), 대부분의 함수 경우 피연산자 중 하나가 또는 인수에 NULL을 반환 하 고 **SqlTypes** 은 NULL입니다. **IsNull** 속성은 항상 true 또는 false 값을 반환 합니다.  
  
## <a name="precision"></a>전체 자릿수  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR의 decimal 데이터 형식에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 숫자 및 decimal 데이터 형식의 최대값과는 다른 최대값이 있습니다. 또한 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR decimal 데이터 형식에는 최대 전체 자릿수가 있는 것으로 간주됩니다. 에 대 한 CLR에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]그러나 **SqlDecimal** 동일한 최대 전체 자릿수, 소수 자릿수 및 decimal 데이터 형식에서와 동일한 의미 체계를 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="overflow-detection"></a>오버플로 검색  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR에서 아주 큰 두 수를 더하면 예외가 throw되지 않습니다. 대신 확인 연산자를 사용하지 않는 경우 반환된 결과가 음의 정수로 "래핑"될 수 있습니다. **System.Data.SqlTypes**, 모든 오버플로 및 언더플로 오류와 0으로 나누기 오류에 대 한 예외가 throw 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [.NET Framework의 SQL Server 데이터 형식](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  

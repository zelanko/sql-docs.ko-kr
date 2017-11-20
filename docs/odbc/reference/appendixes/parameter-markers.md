---
title: "매개 변수 표식을 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c2c8708c18abee3609fc0b01f6ccd2e0362e5706
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="parameter-markers"></a>매개 변수 표식
Sql-92 사양에 따라 응용 프로그램은 다음 위치에 매개 변수 표식에 배치할 수 없습니다. 보다 포괄적인 목록에 대 한 SQL 92 사양을 참조 하십시오.  
  
-   에 **선택** 목록  
  
-   두 가지 모두 *식* 에 *비교 조건자*  
  
-   이항 연산자의 피연산자가 모두로  
  
-   첫 번째 및 두 번째 피연산자가 모두로 **BETWEEN** 작업  
  
-   첫 번째 및 세 번째 피연산자로 **BETWEEN** 작업  
  
-   식 및의 첫 번째 값으로는 **IN** 작업  
  
-   단항 피연산자로 + 또는-작업  
  
-   인수로 *집합 함수 참조*  
  
 매개 변수 표식에 대 한 자세한 내용은 SQL 92 사양을 참조 하십시오. 매개 변수에 대 한 자세한 내용은 참조 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)합니다.


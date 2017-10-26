---
title: "카탈로그 함수를 실행 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 489cd057a15e90794c71cfb433931cd9bc687016
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="executing-catalog-functions"></a>카탈로그 함수를 실행합니다.
카탈로그 함수 결과 집합을 만들기 때문에 모든 결과 집합 생성-SQL 문을 실행 하는 것이 같습니다. 사실, 카탈로그 함수는 종종 미리 정의 된 SQL 문을 실행 하거나 드라이버 또는 DBMS와 함께 제공 되는 미리 정의 된 프로시저를 호출 하 여 구현 됩니다. 결과 집합을 만드는 SQL 문을 적용 되는 거의 모든 항목은 카탈로그 함수에도 적용 됩니다. 반환 된 행의 수를 제한 하는 것 처럼 SQL_ATTR_MAX_ROWS 문 특성 카탈로그 함수에서 반환 된 행의 수를 제한 하는 예를 들어 한 **선택** 문.  
  
 카탈로그 함수를 실행 하는 응용 프로그램은 함수를 호출 합니다.  
  
 카탈로그 함수에 대 한 자세한 내용은 참조 [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)합니다.


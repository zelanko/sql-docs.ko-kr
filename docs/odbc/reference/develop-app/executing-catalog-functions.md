---
title: 카탈로그 기능 실행 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6469a5394e232ab9d9135fbbbd56ba7b791ccbcb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305724"
---
# <a name="executing-catalog-functions"></a>카탈로그 함수 실행
카탈로그 함수는 결과 집합을 생성하므로 결과 집합 생성 SQL 문을 실행하는 것과 같습니다. 실제로 카탈로그 함수는 미리 정의된 SQL 문을 실행하거나 드라이버 또는 DBMS와 함께 제공되는 미리 정의된 프로시저를 호출하여 구현되는 경우가 많습니다. 결과 집합을 만드는 SQL 문에 적용되는 거의 모든 것이 카탈로그 함수에도 적용됩니다. 예를 들어 SQL_ATTR_MAX_ROWS 문 특성은 **SELECT** 문에서 반환되는 행 수를 제한하는 것처럼 카탈로그 함수에서 반환되는 행 수를 제한합니다.  
  
 카탈로그 함수를 실행하기 위해 응용 프로그램은 함수만 호출합니다.  
  
 카탈로그 기능에 대한 자세한 내용은 [카탈로그 함수 를](../../../odbc/reference/develop-app/catalog-functions.md)참조하십시오.

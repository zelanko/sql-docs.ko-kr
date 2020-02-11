---
title: 카탈로그 함수 실행 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab6eba9c4a3df3e16e35d8a93dc95209a093fb80
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901273"
---
# <a name="executing-catalog-functions"></a>카탈로그 함수 실행
카탈로그 함수는 결과 집합을 만들기 때문에 결과 집합을 생성 하는 SQL 문을 실행 하는 것과 같습니다. 실제로 카탈로그 함수는 미리 정의 된 SQL 문을 실행 하거나 드라이버 또는 DBMS와 함께 제공 되는 미리 정의 된 프로시저를 호출 하 여 구현 되는 경우가 많습니다. 결과 집합을 만드는 SQL 문에 적용 되는 거의 모든 항목은 카탈로그 함수에도 적용 됩니다. 예를 들어 SQL_ATTR_MAX_ROWS statement 특성은 **SELECT** 문에서 반환 되는 행 수를 제한 하는 것 처럼 catalog 함수에서 반환 되는 행 수를 제한 합니다.  
  
 카탈로그 함수를 실행 하기 위해 응용 프로그램은 함수를 호출 하기만 합니다.  
  
 카탈로그 함수에 대 한 자세한 내용은 [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)를 참조 하세요.

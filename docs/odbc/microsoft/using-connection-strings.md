---
title: 연결 문자열 사용 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC]
- connecting to data source [ODBC], Visual FoxPro
- Visual FoxPro data source [ODBC], connecting
ms.assetid: 57634960-47e9-49bf-95c1-6e3702ac8166
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9083414503606720a40d372ed883a140953dc415
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307594"
---
# <a name="using-connection-strings"></a>연결 문자열 사용
연결 문자열을 사용하여 Visual FoxPro 데이터 원본에 연결할 수 있습니다.  
  
 예를 들어 TasTrade 데이터 원본에 연결하고 데이터 원본과 연결된 배타적 현재 설정을 재정의하려면 문자열을 사용합니다.  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 연결 문자열에 포함할 수 있는 특성 키워드 및 값 목록은 [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)를 참조하십시오.  
  
 연결 문자열 구문에 대한 자세한 설명은 *ODBC 프로그래머 의 참조에서* [SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md) 를 참조하십시오.

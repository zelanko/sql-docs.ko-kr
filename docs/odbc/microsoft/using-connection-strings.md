---
title: 연결 문자열 사용 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 496fe10fbf49f4d712127e2e4122c50fa20ba2be
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68044579"
---
# <a name="using-connection-strings"></a>연결 문자열 사용
연결 문자열을 사용 하 여 Visual FoxPro 데이터 원본에 연결할 수 있습니다.  
  
 예를 들어 TasTrade 데이터 원본에 연결 하 고 데이터 원본에 연결 된 전용의 현재 설정을 재정의 하려면 다음 문자열을 사용 합니다.  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 연결 문자열에 포함할 수 있는 특성 키워드 및 값 목록은 [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)를 참조 하세요.  
  
 연결 문자열 구문에 대 한 자세한 설명은 *ODBC 프로그래머 참조*에서 [SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md) 를 참조 하세요.

---
title: "날짜 형식 연결 설정 | Microsoft Docs"
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
- date formats [ODBC]
- ODBC driver for Oracle [ODBC], date formats
ms.assetid: ba0d5123-db52-448b-8e19-b7647ce4b361
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 36011b0a1ea6fbb753c2e091a1e74edce498a31b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setting-the-date-format-on-connection"></a>날짜 형식 연결 설정
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 새 버전의 Microsoft ODBC Driver for Oracle의 날짜 형식 Oracle 날짜 필드에 자동으로 설정 하지 않습니다. 이전에 드라이버가 연결 하는 경우 그 사용 `ALTER SESSION SET NLS_DATE_FORMAT ='YYYY-MM-DD HH:MI:SS'`합니다.  
  
 날짜 형식은 설정 하려면 ALTER 세션 집합 호출 하 고 삽입을 수행 합니다. 예를 들어  
  
```  
conn.Execute "ALTER SESSION SET NLS_DATE_FORMAT = 'YYYY-MM-DD HH:MI:SS' "  
sSql = "INSERT INTO DATETEST VALUES (24,'1988-12-01 10:23:03')"  
conn.Execute sSql  
```

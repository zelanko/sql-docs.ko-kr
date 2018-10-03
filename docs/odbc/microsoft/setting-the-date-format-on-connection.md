---
title: 날짜 형식 연결 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date formats [ODBC]
- ODBC driver for Oracle [ODBC], date formats
ms.assetid: ba0d5123-db52-448b-8e19-b7647ce4b361
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e36192279bfc5730559c795ee076db11394ab94
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654281"
---
# <a name="setting-the-date-format-on-connection"></a>연결 시 날짜 형식 설정
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 새 버전의 Microsoft ODBC Driver for Oracle에서는 Oracle 날짜 필드의 날짜 형식을 자동으로 설정 하지 않습니다. 이전에 드라이버를 연결 된 경우 해당 사용 `ALTER SESSION SET NLS_DATE_FORMAT ='YYYY-MM-DD HH:MI:SS'`합니다.  
  
 날짜 형식 설정, ALTER 세션 집합을 호출 하 고 삽입을 수행 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
conn.Execute "ALTER SESSION SET NLS_DATE_FORMAT = 'YYYY-MM-DD HH:MI:SS' "  
sSql = "INSERT INTO DATETEST VALUES (24,'1988-12-01 10:23:03')"  
conn.Execute sSql  
```

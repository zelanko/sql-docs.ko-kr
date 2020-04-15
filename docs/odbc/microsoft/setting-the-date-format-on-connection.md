---
title: 연결날짜 형식 설정 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9da75702275959b48d4965189c9ef5cd856491ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300743"
---
# <a name="setting-the-date-format-on-connection"></a>연결 시 날짜 형식 설정
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 오라클용 Microsoft ODBC 드라이버의 새 버전은 Oracle 날짜 필드의 날짜 형식을 자동으로 설정하지 않습니다. 이전에는 드라이버가 연결될 `ALTER SESSION SET NLS_DATE_FORMAT ='YYYY-MM-DD HH:MI:SS'`때 을 사용했습니다.  
  
 날짜 형식을 설정하려면 세션 변경 SET을 호출한 다음 삽입을 수행합니다. 다음은 그 예입니다.  
  
```  
conn.Execute "ALTER SESSION SET NLS_DATE_FORMAT = 'YYYY-MM-DD HH:MI:SS' "  
sSql = "INSERT INTO DATETEST VALUES (24,'1988-12-01 10:23:03')"  
conn.Execute sSql  
```

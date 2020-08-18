---
description: 연결 시 날짜 형식 설정
title: 연결에 날짜 형식 설정 | Microsoft Docs
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
ms.openlocfilehash: 3137fa2a8433b7b5174910926fd91e846fd462b3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412409"
---
# <a name="setting-the-date-format-on-connection"></a>연결 시 날짜 형식 설정
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 새 버전의 Oracle 용 Microsoft ODBC 드라이버는 Oracle 날짜 필드의 날짜 형식을 자동으로 설정 하지 않습니다. 이전에는 드라이버가 연결 되었을 때이를 사용 `ALTER SESSION SET NLS_DATE_FORMAT ='YYYY-MM-DD HH:MI:SS'` 했습니다.  
  
 날짜 형식을 설정 하려면 ALTER SESSION SET를 호출한 다음 insert를 수행 합니다. 다음은 그 예입니다.  
  
```  
conn.Execute "ALTER SESSION SET NLS_DATE_FORMAT = 'YYYY-MM-DD HH:MI:SS' "  
sSql = "INSERT INTO DATETEST VALUES (24,'1988-12-01 10:23:03')"  
conn.Execute sSql  
```

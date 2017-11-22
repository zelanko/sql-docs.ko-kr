---
title: "ODBC 드라이버의 하위 키 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 756f1f145d7e9a8ea5698366af920cce13041dd2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-drivers-subkey"></a>ODBC 드라이버의 하위 키
ODBC 드라이버 하위 키 아래의 값 설치 된 드라이버를 나열합니다. 이러한 값의 서식은 다음 표에 표시 됩니다.  
  
|이름|데이터 형식|data|  
|----------|---------------|----------|  
|*드라이버 설명*|REG_SZ|**설치**|  
  
 *드라이버 설명* 드라이버 개발자 이름이 정의 됩니다. 일반적으로 드라이버와 관련 된 DBMS의 이름입니다.  
  
 예를 들어, 서식 있는 텍스트 파일 및 SQL Server에 대 한 드라이버가 설치 되어 있다고 가정 합니다. ODBC 드라이버 하위 키 값 수 있습니다.  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```

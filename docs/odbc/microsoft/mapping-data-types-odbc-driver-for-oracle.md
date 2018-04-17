---
title: 데이터 형식 (ODBC Driver for Oracle) 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mapping data types [ODBC]
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: a5d9ce12-19da-4943-8493-e3d56fa08348
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a87220ab330cc7dab4337aa6592ee9f08443d431
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>데이터 형식 매핑 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 Oracle 서버 데이터 형식의 집합을 지원합니다. ODBC Driver for Oracle의 적절 한 ODBC SQL 데이터 형식으로 이러한 데이터 형식을 매핑합니다. 다음 표에서 Oracle 7.3 서버 데이터 형식 및 해당 ODBC SQL 데이터 형식입니다.  
  
 ODBC Driver for Oracle Oracle 7.3 및 일부 열고 Oracle8 데이터 형식을 지원합니다. 지원 되는 열고 Oracle8 데이터 형식에 대 한 자세한 내용은 참조 [지원 되는 데이터 유형](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)합니다.  
  
|Oracle 서버 데이터 형식|ODBC SQL 데이터 형식|  
|-----------------------------|------------------------|  
|CHAR|SQL_CHAR|  
|DATE|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_DECIMAL|  
|LONG|SQL_LONGVARCHAR|  
|LONG RAW|SQL_LONGVARBINARY|  
|NUMBER|SQL_DECIMAL|  
|RAW|SQL_VARBINARY|  
|VARCHAR2|SQL_VARCHAR|  
  
> [!NOTE]  
>  VARCHAR 열에 허용 되는 크기에 대 한 자세한 내용은 참조 [VARCHAR 열 크기](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) 이 가이드의 합니다.

---
title: 데이터 형식 (Oracle 용 ODBC 드라이버) 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping data types [ODBC]
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: a5d9ce12-19da-4943-8493-e3d56fa08348
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ecdd7d7d4b597c4cae218e18b40b0f78e27a6bd5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47775811"
---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>매핑 데이터 형식(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle 서버에는 데이터 형식의 집합을 지원합니다. Oracle 용 ODBC 드라이버는 적절 한 ODBC SQL 데이터 형식으로 이러한 데이터 형식을 매핑합니다. 다음 표에 Oracle 7.3 Server 데이터 형식 및 해당 ODBC SQL 데이터 형식이 있습니다.  
  
 Oracle 용 ODBC 드라이버는 Oracle 7.3 및 열고 Oracle8 데이터 형식도 지원합니다. 지원 되는 열고 Oracle8 데이터 형식에 대 한 자세한 내용은 참조 하세요. [Supported Data Types](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)합니다.  
  
|Oracle Server 데이터 형식|ODBC SQL 데이터 형식|  
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
>  VARCHAR 열 크기를 허용 하는 방법에 대 한 자세한 내용은 참조 [VARCHAR 열 크기](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) 이 가이드에서.

---
title: 데이터 형식 매핑 (Oracle 용 ODBC 드라이버) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 432c21b70efcdd63ef36bfe3d26f8488ddb11d1d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302674"
---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>매핑 데이터 형식(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle 서버는 데이터 형식 집합을 지원 합니다. Oracle 용 ODBC 드라이버는 이러한 데이터 형식을 적절 한 ODBC SQL 데이터 형식에 매핑합니다. 다음 표에서는 Oracle 7.3 서버 데이터 형식 및 해당 ODBC SQL 데이터 형식을 보여 줍니다.  
  
 Oracle 용 ODBC 드라이버는 Oracle 7.3 및 일부 Oracle8 데이터 형식을 지원 합니다. 지원 되는 Oracle8 데이터 형식에 대 한 자세한 내용은 [지원 되는 데이터 형식](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)을 참조 하세요.  
  
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
>  VARCHAR 열에 허용 되는 크기에 대 한 자세한 내용은이 가이드의 [Varchar 열 크기](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) 를 참조 하십시오.

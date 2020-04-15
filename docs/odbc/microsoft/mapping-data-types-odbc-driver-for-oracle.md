---
title: 매핑 데이터 유형(오라클용 ODBC 드라이버) | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302674"
---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>매핑 데이터 형식(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 Oracle Server는 데이터 형식 집합을 지원합니다. 오라클의 ODBC 드라이버는 이러한 데이터 형식을 적절한 ODBC SQL 데이터 형식에 매핑합니다. 다음 표에는 Oracle 7.3 Server 데이터 형식과 해당 ODBC SQL 데이터 형식이 나열되어 있습니다.  
  
 오라클용 ODBC 드라이버는 오라클 7.3 및 일부 Oracle8 데이터 유형을 지원합니다. 지원되는 Oracle8 데이터 유형에 대한 자세한 내용은 [지원되는 데이터 유형을](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)참조하십시오.  
  
|오라클 서버 데이터 유형|ODBC SQL 데이터 유형|  
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
>  VARCHAR 열의 허용 크기에 대한 자세한 내용은 이 가이드의 [VARCHAR 열 크기를](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) 참조하십시오.

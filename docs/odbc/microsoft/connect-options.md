---
title: 연결 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection options [ODBC]
- ODBC driver for Oracle [ODBC], connection options
- custom connection options [ODBC]
ms.assetid: abfdc133-cb33-435f-a467-fbe15444f687
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06695bf1770c9e362decac5702dcd924d47c23bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63301769"
---
# <a name="connect-options"></a>연결 옵션
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 이러한 옵션에는 응용 프로그램 내에서 데이터베이스 연결을 사용자 지정할을 수 있습니다.  
  
|연결 옵션|참고|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|SQL_AUTOCOMMIT_OFF를 선택 하면 응용 프로그램이 명시적으로 커밋하거나 사용 하 여 트랜잭션을 롤백합니다 [SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)합니다.|  
|SQL_ODBC_CURSORS|이 연결 특성은 드라이버 관리자에서 구현 됩니다.|  
|SQL_OPT_TRACE|이 연결 특성은 드라이버 관리자에서 구현 됩니다.|  
|SQL_OPT_TRACEFILE|이 연결 특성은 드라이버 관리자에서 구현 됩니다.|  
|SQL_TRANSLATE_DLL|오류를 반환합니다. "드라이버를 수행할 수 없습니다."|  
|SQL_TRANSLATE_OPTION|번역.dll 전달 되는 32 비트 값입니다.|  
|SQL_TXN_ISOLATION|드라이버 SQL_TXN_READ_COMMITTED만 허용합니다.<br /><br /> 다음 vParams 지원 되지 않습니다.<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|이 ODBC 3.0 연결 특성을 사용 하면 Oracle 용 ODBC 드라이버를 사용 하 여 Microsoft 구성 요소 서비스 (또는 MTS, Windows NT를 사용 하는 경우)에 의해 조정 된 분산 트랜잭션에서 수 있습니다. 인터페이스 포인터를 제공 *pITransaction* 으로 트랜잭션에 합니다 *갖고* 인수입니다.|  
|SQL_ATTR_CONNECTION_DEAD|이 읽기 전용 ODBC 3.5 연결 특성을 사용 하면 Oracle 서버에 연결 실패 했는지 여부를 확인할 수 있습니다. Get만 해당 합니다. 설정할 수 없습니다.|

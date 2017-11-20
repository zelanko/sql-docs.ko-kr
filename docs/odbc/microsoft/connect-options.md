---
title: "옵션 연결 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection options [ODBC]
- ODBC driver for Oracle [ODBC], connection options
- custom connection options [ODBC]
ms.assetid: abfdc133-cb33-435f-a467-fbe15444f687
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9bb45857d47ef145c5693f6718696cbf75ccd666
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="connect-options"></a>연결 옵션
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 이러한 옵션에는 사용자 지정 응용 프로그램 내에서 데이터베이스 연결을 허용 합니다.  
  
|연결 옵션|참고|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|SQL_AUTOCOMMIT_OFF를 선택 하면 응용 프로그램이 명시적으로 커밋하거나 사용 하 여 트랜잭션을 롤백할 [SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)합니다.|  
|SQL_ODBC_CURSORS|이 연결 특성에는 드라이버 관리자에서 구현 됩니다.|  
|SQL_OPT_TRACE|이 연결 특성에는 드라이버 관리자에서 구현 됩니다.|  
|SQL_OPT_TRACEFILE|이 연결 특성에는 드라이버 관리자에서 구현 됩니다.|  
|SQL_TRANSLATE_DLL|오류 반환: "드라이버를 수행할 수 없습니다."|  
|SQL_TRANSLATE_OPTION|번역.dll에 전달 되는 32 비트 값입니다.|  
|SQL_TXN_ISOLATION|드라이버에서 SQL_TXN_READ_COMMITTED만 허용 합니다.<br /><br /> 다음 vParams 지원 되지 않습니다.<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|이 ODBC 3.0 연결 특성을 사용 하면 oracle ODBC 드라이버를 사용 하 여 Microsoft 구성 요소 서비스 (또는 Windows NT를 사용 하는 경우에 MTS)에 의해 조정 된 분산 트랜잭션에 수 있습니다. 인터페이스 포인터를 제공 *pITransaction* 으로 트랜잭션에 *vParam* 인수입니다.|  
|SQL_ATTR_CONNECTION_DEAD|이 읽기 전용 ODBC 3.5 연결 특성을 사용 하면 Oracle 서버에 연결에 문제가 있는지 여부를 확인 수 있습니다. Get만 사용 합니다. 설정할 수 없습니다.|


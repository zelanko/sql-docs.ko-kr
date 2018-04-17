---
title: SQLSetConnectOption (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
- SQLSetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5a35449e-4694-4ee5-9fa1-45d5a8fe7823
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2ee1a1b75b4baca42f58ef91070e8a374e2da964
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 부분  
  
 수준 1 ODBC API 적용:  
  
 연결의 측면을 제어 하는 옵션을 설정 합니다. 이 함수는 부분적으로 지원: 드라이버 지원에 대 한 모든 값은 *fOption* 인수 하지만 중 일부를 지원 하지 않습니다 *vParam* 에 대 한 값은 *fOption* 인수 SQL_TXN_ISOLATION 합니다.  
  
 다음 표에서 설명의 Visual FoxPro ODBC 드라이버 구현에 대 한 동작으로 인수만 **SQLSetConnectOption**합니다.  
  
|*fOption*|주의|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|SQL_AUTOCOMMIT_OFF를 선택 하면 응용 프로그램이 명시적으로 커밋하거나 사용 하 여 트랜잭션을 롤백할 [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); 자동으로 Visual FoxPro ODBC 드라이버는 transactable 문이 완료 되 면을 커밋하지 않습니다. 문이 transactable 경우 드라이버에서 트랜잭션을 시작지 않습니다.|  
|SQL_CURRENT_QUALIFIER|정규화 된 수 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md) 이름 또는 0 개 이상 포함 하는 디렉터리에 대 한 정규화 된 경로 [테이블 있음](../../odbc/microsoft/visual-foxpro-terminology.md)합니다.|  
|SQL_LOGINTIMEOUT|"드라이버를 사용할 수 없습니다." 오류를 반환합니다.|  
|SQL_CURSORS|"드라이버를 사용할 수 없습니다." 오류를 반환합니다.|  
|SQL_PACKET_SIZE|"드라이버를 사용할 수 없습니다." 오류를 반환합니다.|  
|SQL_TXN_ISOLATION|드라이버에서 SQL_TXN_READ_COMMITTED만 허용 합니다.<br /><br /> 다음 *vParam*s는 지원 되지 않습니다.<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 자세한 내용은 참조 [SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md) 에 *ODBC Programmer's Reference*합니다.

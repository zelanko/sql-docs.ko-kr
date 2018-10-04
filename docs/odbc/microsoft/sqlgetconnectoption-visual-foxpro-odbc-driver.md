---
title: SQLGetConnectOption (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5703eb39-f3b2-4f3a-8676-a5625ae29a41
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62f1033abeaa32499602534f7f43b17fefe55ce9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767261"
---
# <a name="sqlgetconnectoption-visual-foxpro-odbc-driver"></a>SQLGetConnectOption(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보를 포함합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: Partial  
  
 수준 1 ODBC API 규칙:  
  
 연결 옵션의 현재 설정을 반환 합니다. 이 함수는 부분적으로 지원: 드라이버에 대 한 모든 값을 지원 합니다 *fOption* 인수 하지만 일부 지원 하지 않습니다 *갖고* 에 대 한 값을 *fOption* 인수 SQL_TXN_ISOLATION 합니다.  
  
 다음 표에서 Visual FoxPro ODBC 드라이버 구현에 특정 동작을 사용 하 여 해당 인수만 **SQLGetConnectOption**합니다.  
  
|*fOption*|Remarks|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|SQL_AUTOCOMMIT_OFF를 선택 하면 응용 프로그램이 명시적으로 커밋하거나 사용 하 여 트랜잭션을 롤백합니다 [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); Visual FoxPro ODBC 드라이버 transactable 문이 완료 될 때를 자동으로 커밋하지 않습니다. 문이 transactable 경우 드라이버에서 트랜잭션을 시작지 않습니다.|  
|SQL_CURRENT_QUALIFIER|정규화 된 데이터베이스 (.dbc 파일) 이름 또는 정규화 된 0 개 이상의 테이블 (.dbf 파일)를 포함 하는 디렉터리 경로 수 있습니다.|  
|SQL_LOGINTIMEOUT|"드라이버 사용할 수 없습니다." 오류를 반환합니다.|  
|SQL_CURSORS|"드라이버 사용할 수 없습니다." 오류를 반환합니다.|  
|SQL_PACKET_SIZE|"드라이버 사용할 수 없습니다." 오류를 반환합니다.|  
|SQL_TXN_ISOLATION|드라이버 SQL_TXN_READ_COMMITTED만 허용합니다.<br /><br /> 다음 *갖고*s는 지원 되지 않습니다.<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE로|  
  
 자세한 내용은 [SQLGetConnectOption](../../odbc/reference/syntax/sqlgetconnectoption-function.md) 에 *ODBC 프로그래머 참조*합니다.

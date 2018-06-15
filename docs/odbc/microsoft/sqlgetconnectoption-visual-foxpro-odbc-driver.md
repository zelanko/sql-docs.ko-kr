---
title: SQLGetConnectOption (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5703eb39-f3b2-4f3a-8676-a5625ae29a41
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23654dc89260423ce51fcde1fd60e554a3095209
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32903558"
---
# <a name="sqlgetconnectoption-visual-foxpro-odbc-driver"></a>SQLGetConnectOption (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 부분  
  
 수준 1 ODBC API 적용:  
  
 연결 옵션의 현재 설정을 반환합니다. 이 함수는 부분적으로 지원: 드라이버 지원에 대 한 모든 값은 *fOption* 인수 하지만 중 일부를 지원 하지 않습니다 *vParam* 에 대 한 값은 *fOption* 인수 SQL_TXN_ISOLATION 합니다.  
  
 다음 표에서 설명의 Visual FoxPro ODBC 드라이버 구현에 대 한 동작으로 인수만 **SQLGetConnectOption**합니다.  
  
|*fOption*|주의|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|SQL_AUTOCOMMIT_OFF를 선택 하면 응용 프로그램이 명시적으로 커밋하거나 사용 하 여 트랜잭션을 롤백할 [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); 자동으로 Visual FoxPro ODBC 드라이버는 transactable 문이 완료 되 면을 커밋하지 않습니다. 문이 transactable 경우 드라이버에서 트랜잭션을 시작지 않습니다.|  
|SQL_CURRENT_QUALIFIER|정규화 된 데이터베이스 (.dbc 파일) 이름 또는 정규화 된 0 개 이상의 테이블 (.dbf 파일)를 포함 하는 디렉터리 경로 수 있습니다.|  
|SQL_LOGINTIMEOUT|"드라이버 사용할 수 없습니다." 오류를 반환합니다.|  
|SQL_CURSORS|"드라이버 사용할 수 없습니다." 오류를 반환합니다.|  
|SQL_PACKET_SIZE|"드라이버 사용할 수 없습니다." 오류를 반환합니다.|  
|SQL_TXN_ISOLATION|드라이버에서 SQL_TXN_READ_COMMITTED만 허용 합니다.<br /><br /> 다음 *vParam*s는 지원 되지 않습니다.<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 자세한 내용은 참조 [SQLGetConnectOption](../../odbc/reference/syntax/sqlgetconnectoption-function.md) 에 *ODBC Programmer's Reference*합니다.

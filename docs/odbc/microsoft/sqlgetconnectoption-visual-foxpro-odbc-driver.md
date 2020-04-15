---
title: SQLGetConnect옵션 (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2dd801988343ded46305665ab2a99aa4e7d76cba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298633"
---
# <a name="sqlgetconnectoption-visual-foxpro-odbc-driver"></a>SQLGetConnectOption(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 부분  
  
 ODBC API 적합성: 레벨 1  
  
 연결 옵션의 현재 설정을 반환합니다. 이 함수는 부분적으로 지원됩니다: 드라이버는 *fOption* 인수에 대한 모든 값을 지원하지만 *SQL_TXN_ISOLATION fOption* 인수에 대한 *일부 vParam* 값을 지원하지 않습니다.  
  
 다음 표에서는 **SQLGetConnectOption의**Visual FoxPro ODBC 드라이버 구현과 관련된 동작이 있는 인수만 설명합니다.  
  
|*f옵션*|설명|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|SQL_AUTOCOMMIT_OFF 선택하면 응용 프로그램이 [SQLTransact를](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md)통해 트랜잭션을 명시적으로 커밋하거나 롤백해야 합니다. Visual FoxPro ODBC 드라이버는 완료시 거래 가능한 문을 자동으로 커밋하지 않습니다. 명령문이 트랜잭션가능한 경우 드라이버가 트랜잭션을 시작합니다.|  
|SQL_CURRENT_QUALIFIER|정규화된 데이터베이스(.dbc file) 이름이거나 테이블이 0개 이상(.dbf 파일)을 포함하는 디렉터리로 의한 완전 정규화된 경로일 수 있습니다.|  
|SQL_LOGINTIMEOUT|"드라이버를 수행할 수 없음" 오류를 반환합니다.|  
|SQL_CURSORS|"드라이버를 수행할 수 없음" 오류를 반환합니다.|  
|SQL_PACKET_SIZE|"드라이버를 수행할 수 없음" 오류를 반환합니다.|  
|SQL_TXN_ISOLATION|드라이버는 SQL_TXN_READ_COMMITTED 수 있습니다.<br /><br /> 다음 *vParam*s는 지원되지 않습니다.<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLGetConnectOption을](../../odbc/reference/syntax/sqlgetconnectoption-function.md) 참조하십시오.

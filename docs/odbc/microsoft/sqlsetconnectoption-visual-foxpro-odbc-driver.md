---
title: SQLSetConnect옵션 (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5a35449e-4694-4ee5-9fa1-45d5a8fe7823
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2af208663f1e91250faad0ca9538b76bcec43b06
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301504"
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 부분  
  
 ODBC API 적합성: 레벨 1  
  
 연결 의 측면을 제어하는 옵션을 설정합니다. 이 함수는 부분적으로 지원됩니다: 드라이버는 *fOption* 인수에 대한 모든 값을 지원하지만 *SQL_TXN_ISOLATION fOption* 인수에 대한 *일부 vParam* 값을 지원하지 않습니다.  
  
 다음 표에서는 **SQLSetConnectOption의**Visual FoxPro ODBC 드라이버 구현과 관련된 동작이 있는 인수만 설명합니다.  
  
|*f옵션*|설명|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|SQL_AUTOCOMMIT_OFF 선택하면 응용 프로그램이 [SQLTransact를](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md)통해 트랜잭션을 명시적으로 커밋하거나 롤백해야 합니다. Visual FoxPro ODBC 드라이버는 완료시 거래 가능한 문을 자동으로 커밋하지 않습니다. 명령문이 트랜잭션가능한 경우 드라이버가 트랜잭션을 시작합니다.|  
|SQL_CURRENT_QUALIFIER|정규 [테이블이](../../odbc/microsoft/visual-foxpro-terminology.md) 0개 [이상](../../odbc/microsoft/visual-foxpro-terminology.md)인 디렉터리에 대한 정규 화된 데이터베이스 이름 또는 정규화된 경로일 수 있습니다.|  
|SQL_LOGINTIMEOUT|"드라이버가 불가능" 오류를 반환합니다.|  
|SQL_CURSORS|"드라이버가 불가능" 오류를 반환합니다.|  
|SQL_PACKET_SIZE|"드라이버가 불가능" 오류를 반환합니다.|  
|SQL_TXN_ISOLATION|드라이버는 SQL_TXN_READ_COMMITTED 수 있습니다.<br /><br /> 다음 *vParam*s는 지원되지 않습니다.<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md) 을 참조하십시오.

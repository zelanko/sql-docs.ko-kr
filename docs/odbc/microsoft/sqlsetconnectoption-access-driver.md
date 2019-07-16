---
title: SQLSetConnectOption (Access 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], Access Driver
ms.assetid: 58399bc4-d0b1-4eaa-a474-c92b2d5855ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bea124a78e2a180180c59de3577fe1db7637e110
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897792"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 액세스 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
|fOption|설명|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption SQL_MODE_READ_ONLY 또는 SQL_MODE_READ_WRITE로 설정할 수 있습니다. 그러나 드라이버 SQL_ACCESS_MODE SQL_MODE_READ_ONLY로 설정 된 경우 업데이트를 방지 하지 않습니다.|  
|SQL_AUTOCOMMIT|Microsoft Access 드라이버를 사용 하는 경우 Microsoft Access 드라이버를 트랜잭션 [1]를 지원 하므로 SQL_AUTOCOMMIT 옵션을 sql_autocommit_on으로 또는 SQL_AUTOCOMMIT_OFF를 설정할 수 있습니다.|  
|SQL_CURRENT_QUALIFIER|지원됩니다.|  
|SQL_LOGIN_TIMEOUT|지원되지 않습니다.|  
|SQL_OPT_TRACE|지원됩니다.|  
|SQL_OPT_TRACEFILE|지원됩니다.|  
|SQL_PACKET_SIZE|지원되지 않습니다.|  
|SQL_QUIET_MODE|지원되지 않습니다.|  
|SQL_TRANSLATE_DLL|지원되지 않습니다.|  
|SQL_TRANSLATION_OPTION|지원되지 않습니다.|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION SQL_TXN_READ_COMMITTED은 항상입니다.|  
  
 [1] 원자성 트랜잭션은 Microsoft Access 드라이버에서 지원 되지 않습니다. Microsoft Access 드라이버를 사용 하 여 트랜잭션 커밋, 유한 지연 트랜잭션이 커밋될 때 시간 값을 기록 하는 시간 사이의 있습니다 디스크에 있습니다. 이 지연은 Microsoft Jet 엔진에 내재 된 지연에 의해 결정 됩니다. 페이지 시간 제한이 됩니다 최소 값 보다 작은 값 아래 PageTimeout 옵션을 설정 하는 경우에 합니다. 결과적으로,가 커밋된 데이터 보장 되지 않습니다 안정적 이므로 지연 시간 동안 변경 될 수 있습니다.

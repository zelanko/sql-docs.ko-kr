---
title: SQLSetConnectOption (텍스트 파일 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Text File Driver
- text file driver [ODBC], SQLSetConnectOption
ms.assetid: b631a20c-2f60-4102-a61d-93b8780a4620
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 32c4a0219b049ee66a38d6c7c10295245dd48ebc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905480"
---
# <a name="sqlsetconnectoption-text-file-driver"></a>SQLSetConnectOption(텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
|fOption|주석|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption은 SQL_MODE_READ_ONLY 또는 SQL_MODE_READ_WRITE로 설정할 수 있습니다. 그러나 SQL_ACCESS_MODE SQL_MODE_READ_ONLY으로 설정 된 경우 드라이버는 업데이트를 방지 하지 않습니다.|  
|SQL_AUTOCOMMIT|텍스트 드라이버는 트랜잭션을 지원 하지 않으므로 ON (기본 상태)으로 설정 된 SQL_AUTOCOMMIT만 지원 합니다.|  
|SQL_CURRENT_QUALIFIER|지원됩니다.|  
|SQL_LOGIN_TIMEOUT|지원되지 않습니다.|  
|SQL_OPT_TRACE|지원됩니다.|  
|SQL_OPT_TRACEFILE|지원됩니다.|  
|SQL_PACKET_SIZE|지원되지 않습니다.|  
|SQL_QUIET_MODE|지원되지 않습니다.|  
|SQL_TRANSLATE_DLL|지원되지 않습니다.|  
|SQL_TRANSLATION_OPTION|지원되지 않습니다.|  
|SQL_TXN_ISOLATION|지원되지 않습니다.|

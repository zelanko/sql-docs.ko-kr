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
manager: craigg
ms.openlocfilehash: ed5c3230a12e79c79624d69b4714a828a865f1dd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47645911"
---
# <a name="sqlsetconnectoption-text-file-driver"></a>SQLSetConnectOption(텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
|fOption|설명|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption SQL_MODE_READ_ONLY 또는 SQL_MODE_READ_WRITE로 설정할 수 있습니다. 그러나 드라이버 SQL_ACCESS_MODE SQL_MODE_READ_ONLY로 설정 된 경우 업데이트를 방지 하지 않습니다.|  
|SQL_AUTOCOMMIT|텍스트 드라이버는 트랜잭션을 지원 하지 않으므로 SQL_AUTOCOMMIT (기본 상태)로 설정 되 고 지원 합니다.|  
|SQL_CURRENT_QUALIFIER|지원됩니다.|  
|SQL_LOGIN_TIMEOUT|지원되지 않습니다.|  
|SQL_OPT_TRACE|지원됩니다.|  
|SQL_OPT_TRACEFILE|지원됩니다.|  
|SQL_PACKET_SIZE|지원되지 않습니다.|  
|SQL_QUIET_MODE|지원되지 않습니다.|  
|SQL_TRANSLATE_DLL|지원되지 않습니다.|  
|SQL_TRANSLATION_OPTION|지원되지 않습니다.|  
|SQL_TXN_ISOLATION|지원되지 않습니다.|

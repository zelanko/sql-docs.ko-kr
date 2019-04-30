---
title: SQLSetConnectOption (dBASE 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], dBASE Driver
ms.assetid: b1924c33-6820-4566-b716-6897807edd0f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0b3c421ad00a1627ddfb7e6f4fb63ee5d30981a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305843"
---
# <a name="sqlsetconnectoption-dbase-driver"></a>SQLSetConnectOption(dBASE 드라이버)
> [!NOTE]  
>  이 항목에서는 dBASE 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
|fOption|설명|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption SQL_MODE_READ_ONLY 또는 SQL_MODE_READ_WRITE로 설정할 수 있습니다. 그러나 드라이버 SQL_ACCESS_MODE SQL_MODE_READ_ONLY로 설정 된 경우 업데이트를 방지 하지 않습니다.|  
|SQL_AUTOCOMMIT|DBASE 드라이버는 트랜잭션을 지원 하지 않습니다 (기본 상태)로 설정 되 고 SQL_AUTOCOMMIT 지원 합니다.|  
|SQL_CURRENT_QUALIFIER|지원됩니다.|  
|SQL_LOGIN_TIMEOUT|지원되지 않습니다.|  
|SQL_OPT_TRACE|지원됩니다.|  
|SQL_OPT_TRACEFILE|지원됩니다.|  
|SQL_PACKET_SIZE|지원되지 않습니다.|  
|SQL_QUIET_MODE|지원되지 않습니다.|  
|SQL_TRANSLATE_DLL|지원되지 않습니다.|  
|SQL_TRANSLATION_OPTION|지원되지 않습니다.|  
|SQL_TXN_ISOLATION|지원되지 않습니다.|

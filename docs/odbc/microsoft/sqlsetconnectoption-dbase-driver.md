---
title: "SQLSetConnectOption (dBASE 드라이버) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DBase driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], dBASE Driver
ms.assetid: b1924c33-6820-4566-b716-6897807edd0f
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 923a8b48c93de3456a1f3cbc002ca73753c8535e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectoption-dbase-driver"></a>SQLSetConnectOption (dBASE 드라이버)
> [!NOTE]  
>  이 항목에서는 dBASE 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
|fOption|설명|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption SQL_MODE_READ_ONLY 또는 SQL_MODE_READ_WRITE로 설정할 수 있습니다. 그러나 드라이버 SQL_ACCESS_MODE SQL_MODE_READ_ONLY로 설정 되어 있으면 업데이트가 방해 되지는 않습니다.|  
|SQL_AUTOCOMMIT|DBASE 드라이버는 트랜잭션을 지원 하지 않으므로 SQL_AUTOCOMMIT (기본 상태)로 설정 되 고 지원 합니다.|  
|SQL_CURRENT_QUALIFIER|지원됩니다.|  
|SQL_LOGIN_TIMEOUT|지원되지 않습니다.|  
|SQL_OPT_TRACE|지원됩니다.|  
|SQL_OPT_TRACEFILE|지원됩니다.|  
|SQL_PACKET_SIZE|지원되지 않습니다.|  
|SQL_QUIET_MODE|지원되지 않습니다.|  
|SQL_TRANSLATE_DLL|지원되지 않습니다.|  
|SQL_TRANSLATION_OPTION|지원되지 않습니다.|  
|SQL_TXN_ISOLATION|지원되지 않습니다.|

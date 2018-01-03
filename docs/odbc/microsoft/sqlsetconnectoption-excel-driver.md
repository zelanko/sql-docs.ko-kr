---
title: "SQLSetConnectOption (Excel 드라이버) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Excel Driver
- Excel driver [ODBC], SQLSetConnectOption
ms.assetid: 528d21d1-4516-4497-9da4-7b87d77e622a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3db148faf3a4a1585a8de981e9d28e769bc9e8c1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetconnectoption-excel-driver"></a>SQLSetConnectOption (Excel 드라이버)
> [!NOTE]  
>  이 항목에서는 Excel 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
|fOption|설명|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption SQL_MODE_READ_ONLY 또는 SQL_MODE_READ_WRITE로 설정할 수 있습니다. 그러나 드라이버 SQL_ACCESS_MODE SQL_MODE_READ_ONLY로 설정 되어 있으면 업데이트가 방해 되지는 않습니다.|  
|SQL_AUTOCOMMIT|Microsoft Excel 드라이버는 트랜잭션을 지원 하지 않기 때문에 (기본 상태)로 설정 되 고 SQL_AUTOCOMMIT 지원 합니다.|  
|SQL_CURRENT_QUALIFIER|지원됩니다.|  
|SQL_LOGIN_TIMEOUT|지원되지 않습니다.|  
|SQL_OPT_TRACE|지원됩니다.|  
|SQL_OPT_TRACEFILE|지원됩니다.|  
|SQL_PACKET_SIZE|지원되지 않습니다.|  
|SQL_QUIET_MODE|지원되지 않습니다.|  
|SQL_TRANSLATE_DLL|지원되지 않습니다.|  
|SQL_TRANSLATION_OPTION|지원되지 않습니다.|  
|SQL_TXN_ISOLATION|지원되지 않습니다.|

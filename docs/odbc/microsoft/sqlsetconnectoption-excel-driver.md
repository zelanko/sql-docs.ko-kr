---
title: SQLSetConnectOption (Excel 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Excel Driver
- Excel driver [ODBC], SQLSetConnectOption
ms.assetid: 528d21d1-4516-4497-9da4-7b87d77e622a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7b9ddd764823b4ed89d9aae7055cf966f9f840a3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301514"
---
# <a name="sqlsetconnectoption-excel-driver"></a>SQLSetConnectOption(Excel 드라이버)
> [!NOTE]  
>  이 항목에서는 Excel 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
|fOption|주석|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption은 SQL_MODE_READ_ONLY 또는 SQL_MODE_READ_WRITE로 설정할 수 있습니다. 그러나 SQL_ACCESS_MODE SQL_MODE_READ_ONLY으로 설정 된 경우 드라이버는 업데이트를 방지 하지 않습니다.|  
|SQL_AUTOCOMMIT|Microsoft Excel 드라이버는 트랜잭션을 지원 하지 않으므로 ON (기본 상태)으로 설정 된 SQL_AUTOCOMMIT만 지원 합니다.|  
|SQL_CURRENT_QUALIFIER|지원됩니다.|  
|SQL_LOGIN_TIMEOUT|지원 안 됨|  
|SQL_OPT_TRACE|지원됩니다.|  
|SQL_OPT_TRACEFILE|지원됩니다.|  
|SQL_PACKET_SIZE|지원 안 됨|  
|SQL_QUIET_MODE|지원 안 됨|  
|SQL_TRANSLATE_DLL|지원 안 됨|  
|SQL_TRANSLATION_OPTION|지원 안 됨|  
|SQL_TXN_ISOLATION|지원 안 됨|

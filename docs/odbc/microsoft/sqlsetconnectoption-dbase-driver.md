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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32bfb4755d308706372c0d863f8246631c122f21
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301524"
---
# <a name="sqlsetconnectoption-dbase-driver"></a>SQLSetConnectOption(dBASE 드라이버)
> [!NOTE]  
>  이 항목에서는 dBASE 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
|fOption|주석|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption은 SQL_MODE_READ_ONLY 또는 SQL_MODE_READ_WRITE로 설정할 수 있습니다. 그러나 SQL_ACCESS_MODE SQL_MODE_READ_ONLY으로 설정 된 경우 드라이버는 업데이트를 방지 하지 않습니다.|  
|SQL_AUTOCOMMIT|DBASE 드라이버는 트랜잭션을 지원 하지 않으므로 ON (기본 상태)으로 설정 된 SQL_AUTOCOMMIT만 지원 합니다.|  
|SQL_CURRENT_QUALIFIER|지원됩니다.|  
|SQL_LOGIN_TIMEOUT|지원 안 됨|  
|SQL_OPT_TRACE|지원됩니다.|  
|SQL_OPT_TRACEFILE|지원됩니다.|  
|SQL_PACKET_SIZE|지원 안 됨|  
|SQL_QUIET_MODE|지원 안 됨|  
|SQL_TRANSLATE_DLL|지원 안 됨|  
|SQL_TRANSLATION_OPTION|지원 안 됨|  
|SQL_TXN_ISOLATION|지원 안 됨|

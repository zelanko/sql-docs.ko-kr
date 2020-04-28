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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e5f15575d34031d9886219af5677b4fc5f1d5aa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301536"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 드라이버 관련 정보에 대 한 액세스를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
|fOption|주석|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption은 SQL_MODE_READ_ONLY 또는 SQL_MODE_READ_WRITE로 설정할 수 있습니다. 그러나 SQL_ACCESS_MODE SQL_MODE_READ_ONLY으로 설정 된 경우 드라이버는 업데이트를 방지 하지 않습니다.|  
|SQL_AUTOCOMMIT|Microsoft access driver를 사용 하는 경우 microsoft access driver가 [1] 트랜잭션을 지원 하기 때문에 SQL_AUTOCOMMIT 옵션을 SQL_AUTOCOMMIT_ON 또는 SQL_AUTOCOMMIT_OFF으로 설정할 수 있습니다.|  
|SQL_CURRENT_QUALIFIER|지원됩니다.|  
|SQL_LOGIN_TIMEOUT|지원 안 됨|  
|SQL_OPT_TRACE|지원됩니다.|  
|SQL_OPT_TRACEFILE|지원됩니다.|  
|SQL_PACKET_SIZE|지원 안 됨|  
|SQL_QUIET_MODE|지원 안 됨|  
|SQL_TRANSLATE_DLL|지원 안 됨|  
|SQL_TRANSLATION_OPTION|지원 안 됨|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION 항상 SQL_TXN_READ_COMMITTED입니다.|  
  
 [1] Microsoft Access 드라이버에서 원자성 트랜잭션을 지원 하지 않습니다. Microsoft Access 드라이버를 사용 하 여 트랜잭션을 커밋하는 경우 트랜잭션이 커밋되는 시간과 값이 디스크에 기록 되는 시간 사이에 유한 지연이 있습니다. 이러한 지연은 Microsoft Jet 엔진에서 내재 된 지연에 의해 결정 됩니다. PageTimeout 옵션이 해당 값 아래에 설정 된 경우에도 페이지 시간 제한은 최소값 보다 작지 않습니다. 결과적으로 지연 중에 변경 될 수 있으므로 커밋된 데이터는 안정적이 지 않을 수 있습니다.

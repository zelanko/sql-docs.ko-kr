---
title: SQLSetConnectOption (Access 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], Access Driver
ms.assetid: 58399bc4-d0b1-4eaa-a474-c92b2d5855ea
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 952bfe683dabbcedeb771c0e7f1787f7a0e6f7bb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption (Access 드라이버)
> [!NOTE]  
>  이 항목에서는 액세스 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
|fOption|설명|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption SQL_MODE_READ_ONLY 또는 SQL_MODE_READ_WRITE로 설정할 수 있습니다. 그러나 드라이버 SQL_ACCESS_MODE SQL_MODE_READ_ONLY로 설정 되어 있으면 업데이트가 방해 되지는 않습니다.|  
|SQL_AUTOCOMMIT|Microsoft Access 드라이버를 사용 하면 Microsoft Access 드라이버에는 [1] 트랜잭션을 지원 하기 때문에 SQL_AUTOCOMMIT 옵션을 SQL_AUTOCOMMIT_ON 또는 SQL_AUTOCOMMIT_OFF를 설정할 수 있습니다.|  
|SQL_CURRENT_QUALIFIER|지원됩니다.|  
|SQL_LOGIN_TIMEOUT|지원되지 않습니다.|  
|SQL_OPT_TRACE|지원됩니다.|  
|SQL_OPT_TRACEFILE|지원됩니다.|  
|SQL_PACKET_SIZE|지원되지 않습니다.|  
|SQL_QUIET_MODE|지원되지 않습니다.|  
|SQL_TRANSLATE_DLL|지원되지 않습니다.|  
|SQL_TRANSLATION_OPTION|지원되지 않습니다.|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION SQL_TXN_READ_COMMITTED 항상입니다.|  
  
 [1] 원자성 트랜잭션은 Microsoft Access 드라이버에서 지원 되지 않습니다. 트랜잭션이 커밋될 때 시간 값을 기록 하는 시간 사이 유한 지연 존재 Microsoft Access 드라이버를 사용 하 여 트랜잭션 커밋 때 디스크에 있습니다. 이 지연 Microsoft Jet 엔진에서 사용 하 여 본질적으로 존재 하는 지연으로 결정 됩니다. 페이지 시간 초과가 됩니다 최소 값 보다 작은 값 보다 PageTimeout 옵션을 설정 하는 경우에 합니다. 결과적으로, 없을 데이터 커밋되는 보장 되지 않으므로 안정 된 지연 시간 동안 변경 될 수 있습니다.

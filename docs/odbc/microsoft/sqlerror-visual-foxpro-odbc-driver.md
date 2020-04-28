---
title: SQLError (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLError function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8315ec16-1c22-447a-a577-39bd94f61070
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0d1247217905187cfb2dbaca6d7b7b562d0175bd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298683"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함 되어 있습니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 지원: 전체  
  
 ODBC API 규칙: 코어 수준  
  
 마지막 오류에 대 한 오류 또는 상태 정보를 반환 합니다. 이 드라이버는 **SQLError** 를 호출 하는 방법에 따라 *hstmt*, *hdbc*및 *henv* 인수에 대해 반환 될 수 있는 오류 또는 스택 또는 목록을 유지 관리 합니다. 각 문 다음에 오류 큐가 플러시됩니다.  
  
 다음 표에서는 드라이버에서 사용 하는 **SQLError** 인수와 반환 값에 대해 설명 합니다.  
  
|SQLError 인수|반환 값 설명|  
|-----------------------|------------------------------|  
|*szSQLState*|오류가 나타내는 SQLSTATE의 값입니다.|  
|*pfNativeError*|0이 아닌 값은 [Visual FOXPRO ODBC 드라이버 원시 오류 메시지](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)를 나타냅니다. 값이 0 이면 드라이버에서 오류를 감지 하 여 해당 [ODBC 오류 코드](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)에 매핑 했음을 나타냅니다.|  
|*szErrorMsg*|네이티브 오류 또는 ODBC 오류의 텍스트입니다.|  
|*pcbErrorMsg*|메시지 텍스트의 길이에 식별자의 길이를 더한 값입니다.|  
  
 드라이버 오류 메시지에 대 한 자세한 내용은 [오류 메시지 개요](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md)를 참조 하세요. 이 함수에 대 한 자세한 내용은 *ODBC 프로그래머 참조*의 [SQLError](../../odbc/reference/syntax/sqlerror-function.md) 를 참조 하십시오.

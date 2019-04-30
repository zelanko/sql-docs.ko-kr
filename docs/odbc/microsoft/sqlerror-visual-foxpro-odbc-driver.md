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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3014c5c2af1a0ef8e5f485c790089e4807834446
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313275"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보를 포함합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 코어 수준  
  
 마지막 오류에 대 한 오류 또는 상태 정보를 반환합니다. 드라이버 스택 또는 오류에 대 한 반환 될 수 있는 목록을 유지 관리 합니다 *hstmt*, *hdbc*, 및 *henv* 방법에 따라 인수에 대 한 호출 **SQLError**  이루어집니다. 오류 큐는 각 문 뒤에 플러시됩니다.  
  
 다음 표에서 설명 합니다 **SQLError** 인수 및 반환 값은 드라이버에서 사용 합니다.  
  
|SQLError 인수|반환 값 설명|  
|-----------------------|------------------------------|  
|*szSQLState*|SQLSTATE 오류를 나타내는 값입니다.|  
|*pfNativeError*|0이 아닌 값을 [Visual FoxPro ODBC 드라이버 원시 오류 메시지](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)합니다. 0 값 오류 드라이버에서 검색 되어 적절 한에 매핑된 [ODBC 오류 코드](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)합니다.|  
|*szErrorMsg*|원시 오류 또는 ODBC 오류에 대 한 텍스트입니다.|  
|*pcbErrorMsg*|메시지 텍스트의 길이 더한 식별자의 길이입니다.|  
  
 드라이버 오류 메시지에 대 한 자세한 내용은 참조 하세요. [오류 메시지 개요](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md)합니다. 이 함수에 대 한 자세한 내용은 참조 하세요. [SQLError](../../odbc/reference/syntax/sqlerror-function.md) 에 *ODBC 프로그래머 참조*합니다.

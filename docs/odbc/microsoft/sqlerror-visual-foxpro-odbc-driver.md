---
title: SQLError (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298683"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 전체  
  
 ODBC API 적합성: 코어 레벨  
  
 마지막 오류에 대한 오류 또는 상태 정보를 반환합니다. 드라이버는 **SQLError** 에 대한 호출이 이루어지는 방법에 따라 *hstmt,* *hdbc*및 *henv* 인수에 대해 반환할 수 있는 스택 또는 오류 목록을 유지 관리합니다. 각 문 후에 오류 큐가 플러시됩니다.  
  
 다음 표는 **SQLError** 인수및 드라이버에서 사용하는 반환 값을 설명합니다.  
  
|SQLError 인수|반환 값 설명|  
|-----------------------|------------------------------|  
|*szSQLState*|오류로 표시되는 SQLSTATE값입니다.|  
|*pf네이티브 오류*|영하지 않은 값은 [Visual FoxPro ODBC 드라이버 네이티브 오류 메시지를](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)나타냅니다. 값이 0이면 드라이버에서 오류가 감지되어 적절한 [ODBC 오류 코드에](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)매핑되었음을 나타냅니다.|  
|*szErrorMsg*|기본 오류 또는 ODBC 오류에 대한 텍스트입니다.|  
|*pcbErrorMsg*|메시지 텍스트의 길이와 식별자의 길이입니다.|  
  
 드라이버 오류 메시지에 대한 자세한 내용은 [오류 메시지 개요를](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md)참조하십시오. 이 함수에 대한 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLError를](../../odbc/reference/syntax/sqlerror-function.md) 참조하십시오.

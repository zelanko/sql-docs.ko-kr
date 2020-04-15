---
title: SQLSetConnectAttr (커서 라이브러리) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC], Cursor Library
ms.assetid: 6f70bbd0-a057-49ef-8b05-4c80b58fc6e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a87c85d727fb9eb2fc27613b9eecd3fe0ec51b58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300543"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLSetConnectAttr** 함수의 사용에 대해 설명합니다. **SQLSetConnectAttr에**대한 일반 정보는 [SQLSetConnectAttr 함수를](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)참조하십시오.  
  
 응용 프로그램은 **SQLSetConnectAttr을** SQL_ATTR_ODBC_CURSORS 특성을 사용하여 커서 라이브러리가 항상 사용되는지, 드라이버가 스크롤 가능한 커서를 지원하지 않는지 또는 사용되지 않는지 지정합니다. 커서 라이브러리는 **SQLGetInfo에서**SQL_STATIC_CURSOR_ATTRIBUTES1 정보 형식에 대한 SQL_CA1_RELATIVE 반환하는 경우 드라이버가 스크롤 가능한 커서를 지원한다고 가정합니다.  
  
 응용 프로그램은 **SQLSetConnectAttr을** 호출하여 연결을 할당하기 위해 *핸들 SQL_HANDLE_DBC 핸들유형이* 있는 **SQLAllocHandle을** 호출한 후 데이터 원본에 연결하기 전에 커서 라이브러리 사용을 지정해야 합니다. 연결이 여전히 활성 상태인 동안 응용 프로그램에서 **SQLSetConnectAttr을** SQL_ATTR_ODBC_CURSORS 특성으로 호출하면 커서 라이브러리에서 오류를 반환합니다.  
  
 연결과 연결된 모든 문에 대해 커서 라이브러리에서 지원하는 문 특성을 설정하려면 응용 프로그램이 데이터 원본에 연결하고 커서를 열기 전에 해당 문 특성에 대해 **SQLSetConnectAttr을** 호출해야 합니다. 응용 프로그램이 **SQLSetConnectAttr을** 문 특성으로 호출하고 연결과 연결된 명령문에서 커서가 열려 있으면 커서가 닫혀 다시 열릴 때까지 문 특성이 해당 명령문에 적용되지 않습니다.

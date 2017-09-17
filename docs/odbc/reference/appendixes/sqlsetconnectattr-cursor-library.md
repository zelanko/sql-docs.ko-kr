---
title: "SQLSetConnectAttr (커서 라이브러리) | Microsoft Docs"
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
- SQLSetConnectAttr function [ODBC], Cursor Library
ms.assetid: 6f70bbd0-a057-49ef-8b05-4c80b58fc6e6
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bf6a14b8215f981e5e0e9c0ca6e9b2e1a2269f65
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLSetConnectAttr** 커서 라이브러리의 함수가 있습니다. 에 대 한 일반적인 내용은 **SQLSetConnectAttr**, 참조 [SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)합니다.  
  
 응용 프로그램이 호출 **SQLSetConnectAttr** 커서 라이브러리 항상 사용, 드라이버는 스크롤 가능 커서를 지원 하지 않는 경우 사용 또는 사용 되지 않았습니다. 지정 SQL_ATTR_ODBC_CURSORS 특성을 사용 합니다. 커서 라이브러리에서 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 유형에 대해 SQL_CA1_RELATIVE 반환 하는 경우는 드라이버가 스크롤 가능 커서를 지원 하는지 가정 **SQLGetInfo**합니다.  
  
 호출 하는 응용 프로그램 **SQLSetConnectAttr** 호출한 후 커서 라이브러리 사용을 지정 하려면 **SQLAllocHandle** 와 *HandleType* 할당할 sql_handle_dbc 라는의 연결 및 데이터 원본에 연결 하기 전에. 응용 프로그램을 호출 하는 경우 **SQLSetConnectAttr** SQL_ATTR_ODBC_CURSORS 특성으로 연결이 여전히 활성 상태 동안 커서 라이브러리는 오류를 반환 합니다.  
  
 연결과 관련 된 모든 문에 대해 커서 라이브러리에서 지 원하는 문 특성을 설정 하려면 응용 프로그램 호출 해야 **SQLSetConnectAttr** 전에 및 데이터 원본에 연결한 후 해당 문 특성 커서를 엽니다. 응용 프로그램을 호출 하는 경우 **SQLSetConnectAttr** 문을 사용 하 여 특성 및 커서는 열린 연결과 관련 된 문, 문 특성 커서를 닫을 때까지 해당 문에 적용 되지 것입니다 및 다시 열립니다.

---
title: SQLSetConnectAttr (커서 라이브러리) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d4023c513ffda04a3cf499110185d3746ca40d9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713461"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLSetConnectAttr** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLSetConnectAttr**를 참조 하십시오 [SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)합니다.  
  
 응용 프로그램 호출 **SQLSetConnectAttr** 커서 라이브러리를 항상 사용, 드라이버 스크롤 가능 커서를 지원 하지 않는 경우 사용 또는 사용 되지 않습니다 지정 SQL_ATTR_ODBC_CURSORS 특성을 사용 합니다. 커서 라이브러리 SQL_CA1_RELATIVE SQL_STATIC_CURSOR_ATTRIBUTES1 정보 형식에 대 한 반환 하는 경우 드라이버 스크롤 가능 커서를 지원 하는지 가정 **SQLGetInfo**합니다.  
  
 응용 프로그램을 호출 해야 합니다 **SQLSetConnectAttr** 호출한 후 커서 라이브러리 사용을 적용 하지 않으려면 **SQLAllocHandle** 사용 하 여는 *HandleType* 할당할 SQL_HANDLE_DBC의 연결 및 데이터 원본에 연결 하기 전에 합니다. 응용 프로그램을 호출 하는 경우 **SQLSetConnectAttr** SQL_ATTR_ODBC_CURSORS 특성을 사용 하 여 연결이 아직 활성 상태인 경우 커서 라이브러리 오류를 반환 합니다.  
  
 연결과 관련 된 모든 문에 대해 커서 라이브러리에 의해 지원 되는 문 특성을 설정 하려면 응용 프로그램 호출 해야 합니다 **SQLSetConnectAttr** 하기 전에 데이터 원본에 연결한 후 해당 문 특성 커서를 엽니다. 응용 프로그램을 호출 하는 경우 **SQLSetConnectAttr** 문을 사용 하 여 특성 및 커서에서 열려 있는 연결과 관련 된 문을, 문 특성 커서를 닫을 때까지 해당 문에 적용 되지 것입니다 및 다시 시작 합니다.

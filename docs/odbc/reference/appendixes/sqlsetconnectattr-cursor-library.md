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
ms.openlocfilehash: 73d1369a2bce0327ac3367d33f0894bdcfab8205
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125578"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLSetConnectAttr** 함수를 사용 하는 방법을 설명 합니다. **SQLSetConnectAttr**에 대 한 일반 정보는 [SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)를 참조 하세요.  
  
 응용 프로그램은 SQL_ATTR_ODBC_CURSORS 특성을 사용 하 여 **SQLSetConnectAttr** 를 호출 하 여 커서 라이브러리가 항상 사용 되는지 여부를 지정 합니다 .이 경우 드라이버에서 스크롤 가능 커서를 지원 하지 않거나 사용 되지 않는 경우에 사용 됩니다. 커서 라이브러리는 **SQLGetInfo**의 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 형식에 대 한 SQL_CA1_RELATIVE를 반환 하는 경우 드라이버가 스크롤 가능 커서를 지원 한다고 가정 합니다.  
  
 응용 프로그램은 **SQLSetConnectAttr** *를 호출* 하 SQL_HANDLE_DBC 여 **SQLAllocHandle** 를 호출한 후 연결을 할당 하 고 데이터 원본에 연결 하기 전에 커서 라이브러리 사용을 지정 해야 합니다. 연결이 아직 활성 상태일 때 응용 프로그램이 SQL_ATTR_ODBC_CURSORS 특성을 사용 하 여 **SQLSetConnectAttr** 를 호출 하면 커서 라이브러리에서 오류를 반환 합니다.  
  
 커서 라이브러리에서 연결과 관련 된 모든 문에 대해 지원 되는 문 특성을 설정 하려면 응용 프로그램이 데이터 소스에 연결한 후 커서를 열기 전에 해당 문 특성에 대해 **SQLSetConnectAttr** 를 호출 해야 합니다. 응용 프로그램에서 문 특성을 사용 하 여 **SQLSetConnectAttr** 를 호출 하 고 연결과 관련 된 문에서 커서가 열려 있는 경우 커서가 닫혔다가 다시 열릴 때까지 문 특성이 해당 문에 적용 되지 않습니다.

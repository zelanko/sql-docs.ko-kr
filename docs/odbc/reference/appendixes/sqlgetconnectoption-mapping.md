---
title: SQLGetConnectOption 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d2905bd6793d032e485183c8f553cef2cdefda3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302004"
---
# <a name="sqlgetconnectoption-mapping"></a>SQLGetConnectOption 매핑
응용 *프로그램이 ODBC 3.x* 드라이버를 통해 **SQLGetConnectOption** 를 호출 하는 경우에 대 한 호출이  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 는 다음과 같이 매핑됩니다.  
  
-   *Foption* 이 문자열을 반환 하는 ODBC 정의 연결 옵션을 나타내는 경우 드라이버 관리자는를 호출 합니다.  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   *Foption* 이 32 비트 정수 값을 반환 하는 ODBC 정의 연결 옵션을 나타내는 경우 드라이버 관리자는를 호출 합니다.  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   *Foption* 이 드라이버 정의 문 옵션을 나타내는 경우 드라이버 관리자는를 호출 합니다.  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 앞의 세 가지 경우에서 *ConnectionHandle* 인수는 *hdbc*의 값으로 설정 되 고, *특성* 인수는 *foption*의 값으로 설정 되며, 값 *eptr* 인수는 *pvParam*와 동일한 값으로 설정 됩니다.  
  
 ODBC 정의 문자열 연결 옵션의 경우 드라이버 관리자는 **SQLGetConnectAttr** 호출에서 *bufferlength* 인수를 미리 정의 된 최대 길이 (SQL_MAX_OPTION_STRING_LENGTH)로 설정 합니다. 문자열이 아닌 연결 옵션의 경우 *Bufferlength* 는 0으로 설정 됩니다.  
  
 ODBC 3.x 드라이버의 경우 드라이버 관리자는 더 이상 *옵션이* SQL_CONN_OPT_MIN와 SQL_CONN_OPT_MAX 사이에 있는지 또는 SQL_CONNECT_OPT_DRVR_START 보다 큰지 확인 하지 *않습니다.* 드라이버는 옵션 값의 유효성을 검사 해야 합니다.

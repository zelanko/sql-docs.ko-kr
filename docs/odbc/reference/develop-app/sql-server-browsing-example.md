---
title: SQL Server 검색 예제 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBrowseConnect function [ODBC], example
- connecting to data source [ODBC], SqlBrowseConnect
- connecting to driver [ODBC], SQLBrowseConnect
ms.assetid: 6e0d5fd1-ec93-4348-a77a-08f5ba738bc6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7b15aa8e3d573660a312fceb5b9100a41f0384d2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301984"
---
# <a name="sql-server-browsing-example"></a>SQL Server 찾아보기 예제
다음 예에서는 **SQLBrowseConnect** 를 사용 하 여 SQL Server 드라이버에서 사용할 수 있는 연결을 검색 하는 방법을 보여 줍니다. 먼저 응용 프로그램에서 연결 핸들을 요청 합니다.  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 그런 다음 응용 프로그램은 **SQLBrowseConnect** 를 호출 하 고 **sqldrivers**에서 반환 된 드라이버 설명을 사용 하 여 SQL Server 드라이버를 지정 합니다.  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 이는 **SQLBrowseConnect**에 대 한 첫 번째 호출 이므로 드라이버 관리자는 SQL Server 드라이버를 로드 하 고 응용 프로그램에서 받은 것과 동일한 인수를 사용 하 여 드라이버의 **SQLBrowseConnect** 함수를 호출 합니다.  
  
> [!NOTE]  
>  Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는 경우 연결 문자열에 사용자 `Trusted_Connection=yes` ID 및 암호 정보를 지정 하는 대신를 지정 해야 합니다.  
  
 드라이버는 **SQLBrowseConnect** 에 대 한 첫 번째 호출을 확인 하 고 두 번째 수준의 연결 특성 (서버, 사용자 이름, 암호, 응용 프로그램 이름 및 워크스테이션 ID)을 반환 합니다. 서버 특성의 경우 유효한 서버 이름 목록을 반환 합니다. **SQLBrowseConnect** 의 반환 코드는 SQL_NEED_DATA 되었습니다. 찾아보기 결과 문자열은 다음과 같습니다.  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 찾아보기 결과 문자열의 각 키워드 뒤에는 콜론과 등호 앞에 있는 하나 이상의 단어가 나옵니다. 이러한 단어는 응용 프로그램에서 대화 상자를 작성 하는 데 사용할 수 있는 사용자에 게 친숙 한 이름입니다. **앱** 및 **wsid** 키워드는 별표를 접두사로 사용 합니다. 즉, 선택 사항입니다. **서버**, **UID**및 **PWD** 키워드에 별표가 접두사로 붙지 않습니다. 다음 찾아보기 요청 문자열에서 값을 제공 해야 합니다. **SERVER** 키워드의 값은 **SQLBrowseConnect** 에서 반환 하는 서버 또는 사용자가 제공한 이름 중 하나일 수 있습니다.  
  
 응용 프로그램은 **SQLBrowseConnect** 를 다시 호출 하 고, 녹색 서버를 지정 하 고, **앱** 및 **wsid** 키워드를 생략 하 고 각 키워드 뒤에 사용자에 게 친숙 한 이름을 지정 합니다.  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 드라이버가 녹색 서버에 연결 하려고 합니다. 누락 된 키워드-값 쌍과 같이 심각 하지 않은 오류가 발생 하는 경우 **SQLBrowseConnect** 는 SQL_NEED_DATA을 반환 하 고 오류 이전과 동일한 상태로 유지 됩니다. 응용 프로그램에서 **SQLGetDiagField** 또는 **SQLGetDiagRec** 를 호출 하 여 오류를 확인할 수 있습니다. 연결에 성공 하면 드라이버는 SQL_NEED_DATA을 반환 하 고 찾아보기 결과 문자열을 반환 합니다.  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 이 문자열의 특성은 선택 사항 이므로 응용 프로그램에서 생략할 수 있습니다. 그러나 응용 프로그램은 **SQLBrowseConnect** 를 다시 호출 해야 합니다. 응용 프로그램에서 데이터베이스 이름 및 언어를 생략 하도록 선택 하면 빈 찾아보기 요청 문자열을 지정 합니다. 이 예제에서 응용 프로그램은 pubs 데이터베이스를 선택 하 고 **SQLBrowseConnect** 를 마지막으로 호출 합니다. 이때 **LANGUAGE** 키워드와 별표는 **데이터베이스** 키워드 앞에 있습니다.  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 **데이터베이스** 특성은 드라이버에 필요한 최종 연결 특성이 기 때문에 검색 프로세스가 완료 되 고 응용 프로그램이 데이터 원본에 연결 되며 **SQLBrowseConnect** 가 SQL_SUCCESS를 반환 합니다. 또한 **SQLBrowseConnect** 는 전체 연결 문자열을 찾아보기 결과 문자열로 반환 합니다.  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 드라이버에서 반환 되는 최종 연결 문자열에는 각 키워드 뒤에 사용자에 게 친숙 한 이름이 포함 되지 않으며, 응용 프로그램에서 지정 하지 않은 선택적 키워드만 포함 되지 않습니다. 응용 프로그램은 **SQLDriverConnect** 와 함께이 문자열을 사용 하 여 현재 연결 핸들 (연결 끊기 후)에서 데이터 원본에 다시 연결 하거나 다른 연결 핸들의 데이터 원본에 연결할 수 있습니다. 다음은 그 예입니다.  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```

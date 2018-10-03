---
title: 예를 검색 하는 SQL Server | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8dc57d738c1d5726d2208b930c5d4fadcd93b39
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47786701"
---
# <a name="sql-server-browsing-example"></a>SQL Server 찾아보기 예제
다음 예제에서는 어떻게 **SQLBrowseConnect** SQL Server에 대 한 드라이버를 사용 하 여 사용할 수 있는 연결을 찾아보기에 사용 될 수 있습니다. 첫째, 응용 프로그램 연결 핸들을 요청합니다.  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 다음으로 응용 프로그램 호출 **SQLBrowseConnect** 반환한 드라이버 설명을 사용 하 여 SQL Server 드라이버를 지정 하 고 **SQLDrivers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 첫 번째 호출은 이기 때문에 **SQLBrowseConnect**, SQL Server 드라이버를 로드 하 고 드라이버를 호출 하는 드라이버 관리자 **SQLBrowseConnect** 에서 수신한 동일한 인수를 사용 하 여 함수를 응용 프로그램입니다.  
  
> [!NOTE]  
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, `Trusted_Connection=yes` 연결 문자열에 사용자 ID와 암호 정보 대신 합니다.  
  
 드라이버 확인이 첫 번째 호출은 **SQLBrowseConnect** 연결 특성의 두 번째 수준을 반환 하 고: 서버, 사용자 이름, 암호, 응용 프로그램 이름 및 워크스테이션 id입니다. 서버 특성에 대해 유효한 서버 이름 목록을 반환합니다. 반환 코드 **SQLBrowseConnect** sql_need_data가 됩니다. 찾아보기 결과 문자열은 다음과 같습니다.  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 각 키워드 찾아보기 결과 문자열의 콜론 및 등호 앞에 있는 하나 이상의 단어 뒤에. 이러한 단어는 응용 프로그램 대화 상자를 만드는 데 사용할 수 있는 친숙 한 이름입니다. **앱** 하 고 **WSID** 키워드 선택 사항인 즉 별표가 붙습니다. 합니다 **SERVER**를 **UID**, 및 **PWD** 키워드 별표가 붙습니다 하지 않으면 다음 찾아보기 요청 문자열의 값에 제공 되어야 합니다. 에 대 한 값을 **SERVER** 키워드에서 반환 된 서버 중 하나일 수 있습니다 **SQLBrowseConnect** 또는 사용자가 제공한 이름입니다.  
  
 응용 프로그램 호출 **SQLBrowseConnect** 다시 녹색 서버를 지정 하 고 생략 하는 **앱** 및 **WSID** 키워드 및 각 키워드 다음 친숙 한 이름:  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 드라이버는 녹색 서버에 연결 하려고 합니다. 누락 된 키워드-값 쌍을 같은 치명적이 지 않은 오류가 발생 하는 경우 **SQLBrowseConnect** SQL_NEED_DATA를 반환 하 고 오류 하기 이전과 동일한 상태로 유지 됩니다. 응용 프로그램에서 호출할 수 있습니다 **SQLGetDiagField** 하거나 **SQLGetDiagRec** 오류를 확인 합니다. 연결이 성공 하면 드라이버 SQL_NEED_DATA를 반환 합니다 하 고 찾아보기 결과 문자열을 반환 합니다.  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 이 문자열의 특성은 선택 사항 이므로 응용 프로그램을 생략할 수 있습니다. 그러나 응용 프로그램 호출 해야 합니다 **SQLBrowseConnect** 다시 합니다. 응용 프로그램을 데이터베이스 이름 및 언어 생략 하기로 빈 찾아보기 요청 문자열을 지정 합니다. Pubs 데이터베이스 및 호출에이 예제에서 응용 프로그램을 선택 **SQLBrowseConnect** 를 마지막으로 생략 합니다 **언어** 키워드와 전에 별표를 **데이터베이스**키워드:  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 때문에 합니다 **데이터베이스** 특성은 드라이버에 필요한 최종 연결 특성, 검색 프로세스가 완료 된 응용 프로그램의 데이터 원본에 연결 하 고 **SQLBrowseConnect** 관계 없이 SQL_SUCCESS를 반환합니다. **SQLBrowseConnect** 도 찾아보기 결과 문자열로 전체 연결 문자열을 반환 합니다.  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 각 키워드에 다음 알기 쉬운 이름을 드라이버에서 반환 하는 최종 연결 문자열에 포함 되지 않습니다도 포함 하 고 응용 프로그램에서 지정 되지 않은 선택적 키워드입니다. 응용 프로그램으로이 문자열을 사용할 수 있습니다 **SQLDriverConnect** (연결 끊기) 한 후 현재 연결 핸들에 대해 데이터 원본에 다시 연결 하거나 다른 연결 핸들의 데이터 원본에 연결 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```

---
title: "예제를 탐색 하는 SQL Server | Microsoft Docs"
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
- SQLBrowseConnect function [ODBC], example
- connecting to data source [ODBC], SqlBrowseConnect
- connecting to driver [ODBC], SQLBrowseConnect
ms.assetid: 6e0d5fd1-ec93-4348-a77a-08f5ba738bc6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6f344ce0a3830bbd79d6674cfd4d5961b973939e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sql-server-browsing-example"></a>SQL Server 검색 예
다음 예제에서는 어떻게 **SQLBrowseConnect** SQL Server에 대 한 드라이버를 사용할 수 있는 연결을 검색 하는 데 사용 될 수 있습니다. 첫째, 응용 프로그램 연결 핸들을 요청합니다.  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 다음으로 응용 프로그램 호출 **SQLBrowseConnect** 반환한 드라이버 설명을 사용 하 여 SQL Server 드라이버를 지정 하 고 **SQLDrivers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 이 항목은 첫 번째 호출 **SQLBrowseConnect**, 드라이버 관리자는 SQL Server 드라이버를 로드 하 고 호출 하는 드라이버의 **SQLBrowseConnect** 에서 받은 동일한 인수를 갖는 함수는 응용 프로그램입니다.  
  
> [!NOTE]  
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, `Trusted_Connection=yes` 연결 문자열에 사용자 ID와 암호 정보 대신 합니다.  
  
 드라이버는 첫 번째 호출 하다 고 결정 **SQLBrowseConnect** 연결 특성의 두 번째 수준을 반환 하 고: 서버, 사용자 이름, 암호, 응용 프로그램 이름 및 워크스테이션 id입니다. 서버 특성에 대 한 유효한 서버 이름 목록을 반환합니다. 반환 코드 **SQLBrowseConnect** SQL_NEED_DATA 됩니다. 다음은 찾아보기 결과 문자열이입니다.  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 각 키워드는 찾아보기 결과 문자열에 콜론과 등호 앞에 있는 하나 이상의 단어 나옵니다. 이러한 단어는 응용 프로그램 대화 상자를 만드는 데 사용할 수 있는 이름이 됩니다. **앱** 및 **WSID** 키워드는 선택 사항 이므로 별표 접두사로 합니다. **서버**, **UID**, 및 **PWD** 키워드 별표 접두사가 붙지 않습니다; 다음 찾아보기 요청 문자열의 값을 제공 되어야 합니다. 에 대 한 값은 **서버** 키워드에서 반환 된 서버 중 하나일 수 있습니다 **SQLBrowseConnect** 또는 사용자가 제공한 이름입니다.  
  
 응용 프로그램 호출 **SQLBrowseConnect** 다시 녹색 서버를 지정 하 고는 생략 된 **앱** 및 **WSID** 키워드와 각 키워드 다음 알아보기 쉬운 이름을:  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 드라이버는 녹색 서버에 연결 하려고 시도 합니다. 한 누락 된 키워드-값 쌍과 같은 치명적이 지 않은 오류가 발생 하는 경우 **SQLBrowseConnect** SQL_NEED_DATA를 반환 하 고 오류 하기 이전과 동일한 상태로 유지 됩니다. 응용 프로그램에서 호출할 수 **SQLGetDiagField** 또는 **SQLGetDiagRec** 오류를 확인 합니다. 연결이 성공 하는 경우 드라이버 sql_need_data가 반환 하 고 찾아보기 결과 문자열을 반환 합니다.  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 이 문자열의 특성은 선택적 이기 때문에 응용 프로그램 생략할 수 있습니다. 하지만 응용 프로그램을 호출 해야 **SQLBrowseConnect** 다시 합니다. 응용 프로그램에서 데이터베이스 이름 및 언어를 선택 하면 빈 찾아보기 요청 문자열을 지정 합니다. Pubs 데이터베이스 및 호출에이 예제 응용 프로그램을 선택 **SQLBrowseConnect** 를 마지막으로 생략 하는 것은 **언어** 키워드와 전에 별표는 **데이터베이스**키워드:  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 때문에 **데이터베이스** 특성은 드라이버에 필요한 최종 연결 특성, 검색 프로세스가 완료 되 면 응용 프로그램 데이터 원본에 연결 하 고 **SQLBrowseConnect** 관계 없이 SQL_SUCCESS를 반환합니다. **SQLBrowseConnect** 도 찾아보기 결과 문자열에 따라 전체 연결 문자열을 반환 합니다.  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 각 키워드 다음 알아보기 쉬운 이름을 드라이버에 의해 반환 되는 최종 연결 문자열에 포함 되지 않습니다도 포함 하 고 선택적 키워드는 응용 프로그램에서 지정 하지 않습니다. 응용 프로그램으로이 문자열 צ ְ ײ **SQLDriverConnect** (연결 끊기) 한 후 현재 연결 핸들에 데이터 원본에 다시 연결 하거나, 다른 연결 핸들의 데이터 원본에 연결 합니다. 예를 들어  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```

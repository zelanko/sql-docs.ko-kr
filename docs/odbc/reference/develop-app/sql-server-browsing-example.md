---
title: SQL 서버 브라우징 예제 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301984"
---
# <a name="sql-server-browsing-example"></a>SQL Server 찾아보기 예제
다음 예제에서는 **SQLServerConnect를** 사용하여 SQL Server용 드라이버에서 사용할 수 있는 연결을 검색하는 방법을 보여 주며 있습니다. 먼저 응용 프로그램은 연결 핸들을 요청합니다.  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 다음으로 응용 프로그램은 **SQLBrowseConnect를** 호출하고 **SQLDriver에서**반환된 드라이버 설명을 사용하여 SQL Server 드라이버를 지정합니다.  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 **SQLBrowseConnect에**대한 첫 번째 호출이기 때문에 드라이버 관리자는 SQL Server 드라이버를 로드하고 응용 프로그램에서 받은 것과 동일한 인수로 드라이버의 **SQLBrowseConnect** 함수를 호출합니다.  
  
> [!NOTE]  
>  Windows 인증을 지원하는 데이터 원본 공급자에 연결하는 경우 `Trusted_Connection=yes` 연결 문자열에서 사용자 ID 및 암호 정보 대신 지정해야 합니다.  
  
 드라이버는 이것이 **SQLBrowseConnect에** 대한 첫 번째 호출이라고 결정하고 서버, 사용자 이름, 암호, 응용 프로그램 이름 및 워크스테이션 ID와 같은 두 번째 수준의 연결 특성을 반환합니다. 서버 특성의 경우 유효한 서버 이름 목록을 반환합니다. **SQLBrowseConnect의** 반환 코드는 SQL_NEED_DATA. 찾아보기 결과 문자열은 다음과 같습니다.  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 찾아보기 결과 문자열의 각 키워드 뒤에는 콜론과 같은 기호 앞에 하나 이상의 단어가 있습니다. 이러한 단어는 응용 프로그램에서 대화 상자를 작성하는 데 사용할 수 있는 사용자 친화적인 이름입니다. **APP** 및 **WSID** 키워드는 별표에 의해 접두사에 붙어 있으며 이는 선택 사항입니다. **서버,** **UID**및 **PWD** 키워드는 별표에 의해 접두사되지 않습니다. 값은 다음 찾아보기 요청 문자열에서 제공되어야 합니다. **SERVER** 키워드의 값은 **SQLBrowseConnect에서** 반환하는 서버 중 하나이거나 사용자가 제공한 이름일 수 있습니다.  
  
 응용 프로그램은 녹색 서버를 지정하고 각 키워드 다음에 **APP** 및 **WSID** 키워드와 사용자 친화적인 이름을 생략하여 **SQLBrowseConnect를** 다시 호출합니다.  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 드라이버가 녹색 서버에 연결하려고 시도합니다. 누락된 키워드 값 쌍과 같은 치명적이지 않은 오류가 있는 경우 **SQLBrowseConnect는** SQL_NEED_DATA 반환하고 오류 이전과 동일한 상태로 유지됩니다. 응용 프로그램은 오류를 결정하기 위해 **SQLGetDiagField** 또는 **SQLGetDiagRec을** 호출 할 수 있습니다. 연결이 성공하면 드라이버는 SQL_NEED_DATA 반환하고 찾아보기 결과 문자열을 반환합니다.  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 이 문자열의 특성은 선택 사항이므로 응용 프로그램에서 이 특성을 생략할 수 있습니다. 그러나 응용 프로그램은 **SQLBrowseConnect를** 다시 호출해야 합니다. 응용 프로그램이 데이터베이스 이름과 언어를 생략하도록 선택하면 빈 찾아보기 요청 문자열이 지정됩니다. 이 예제에서 응용 프로그램은 pubs 데이터베이스를 선택하고 **SQLBrowseConnect를** 마지막으로 호출하여 **데이터베이스** 키워드 앞에 **언어** 키워드와 별표를 생략합니다.  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 **데이터베이스** 특성은 드라이버에 필요한 최종 연결 특성이므로 검색 프로세스가 완료되고 응용 프로그램이 데이터 원본에 연결되고 **SQLBrowseConnect가** SQL_SUCCESS 반환합니다. **SQLBrowseConnect는** 전체 연결 문자열을 찾아보기 결과 문자열로 반환합니다.  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 드라이버에서 반환되는 최종 연결 문자열에는 각 키워드 다음의 사용자 친화적인 이름이 포함되지 않으며 응용 프로그램에서 지정하지 않은 선택적 키워드도 포함되어 있지 않습니다. 응용 프로그램은 **SQLDriverConnect와** 함께 이 문자열을 사용하여 현재 연결 핸들의 데이터 원본에 다시 연결하거나(연결을 끊은 후) 다른 연결 핸들의 데이터 원본에 연결할 수 있습니다. 다음은 그 예입니다.  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```

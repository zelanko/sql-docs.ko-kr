---
title: SQL브라우오커와 연결 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLBrowseConnect
- SQLBrowseConnect function [ODBC], connecting
- connecting to data source [ODBC], SQLBrowseConnect
ms.assetid: 6c2e9f76-b766-48df-b109-246bb05ae45d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4d738d394bb3c507f6aa08f736016b51ac4fefb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294663"
---
# <a name="connecting-with-sqlbrowseconnect"></a>SQLBrowseConnect로 연결
**SQLDriverConnect와**같은 **SQLBrowseConnect는**연결 문자열을 사용합니다. 그러나 **SQLBrowseConnect를**사용 하 여 응용 프로그램은 런타임에 전체 연결 문자열을 생성할 수 있습니다. 이를 통해 애플리케이션에서는 다음 두 가지 작업이 가능해집니다.  
  
-   이 정보를 묻는 메시지를 표시하기 위해 자체 대화 상자를 작성하여 "모양과 느낌"에 대한 제어권을 유지합니다.  
  
-   특정 드라이버에서 사용할 수 있는 데이터 원본을 몇 개의 단계에 따라 시스템에서 찾습니다. 예를 들어 사용자는 먼저 네트워크에서 서버를 찾아서 선택한 다음 이 서버에서 드라이버가 액세스할 수 있는 데이터베이스를 찾습니다.  
  
 응용 프로그램은 **SQLBrowseConnect를** 호출하고 드라이버 또는 데이터 원본을 지정하는 *찾아보기 요청 연결 문자열이라고* 하는 연결 문자열을 전달합니다. 드라이버는 키워드, 가능한 값(키워드가 개별 값 집합을 허용하는 경우) 및 사용자 친화적인 이름을 포함하는 *찾아보기 결과 연결 문자열이라고* 하는 연결 문자열을 반환합니다. 응용 프로그램은 사용자 친화적인 이름으로 대화 상자를 빌드하고 사용자에게 값을 묻는 메시지를 표시합니다. 그런 다음 이러한 값에서 새 찾아보기 요청 연결 문자열을 빌드하고 **SQLBrowseConnect**에 대한 다른 호출을 사용하여 드라이버에 반환합니다.  
  
 연결 문자열이 앞뒤로 전달되므로 드라이버는 응용 프로그램이 이전 문자열을 반환할 때 새 연결 문자열을 반환하여 여러 수준의 탐색을 제공할 수 있습니다. 예를 들어 응용 프로그램에서 **SQLBrowseConnect를**처음 호출할 때 드라이버는 키워드를 반환하여 사용자에게 서버 이름을 묻는 메시지를 표시할 수 있습니다. 응용 프로그램이 서버 이름을 반환하면 드라이버가 키워드를 반환하여 사용자에게 데이터베이스를 묻는 메시지를 표시할 수 있습니다. 응용 프로그램이 데이터베이스 이름을 반환한 후 검색 프로세스가 완료됩니다.  
  
 **SQLBrowseConnect새** 찾아보기 결과 연결 문자열을 반환할 때마다 SQL_NEED_DATA 반환 코드로 반환합니다. 이렇게 하면 응용 프로그램에 연결 프로세스가 완료되지 않음을 알려줍니다. **SQLBrowseConnect가** SQL_SUCCESS 반환할 때까지 연결은 데이터 필요 상태이며 연결 특성을 설정하는 등의 다른 용도로 사용할 수 없습니다. 응용 프로그램은 **SQLDisconnect**를 호출하여 연결 검색 프로세스를 종료할 수 있습니다.  
  
 이 섹션에는 다음 항목이 포함되어 있습니다.  
  
-   [SQL Server 찾아보기 예제](../../../odbc/reference/develop-app/sql-server-browsing-example.md)

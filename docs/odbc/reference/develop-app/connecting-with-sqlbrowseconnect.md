---
title: SQLBrowseConnect로 연결 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec1cd42e6704bc5168b1eb20841100fc279a66ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042769"
---
# <a name="connecting-with-sqlbrowseconnect"></a>SQLBrowseConnect로 연결
**SQLBrowseConnect**과 같이 **SQLDriverConnect**, 연결 문자열을 사용 합니다. 그러나 **SQLBrowseConnect**, 응용 프로그램 런타임 시 전체 연결 문자열을 생성할 수 있습니다. 이를 통해 응용 프로그램에서는 다음 두 가지 작업이 가능해집니다.  
  
-   해당 "모양과 느낌"에 대 한 제어를 유지 하므로,이 정보를 묻는 고유의 대화 상자 빌드  
  
-   특정 드라이버에서 사용할 수 있는 데이터 원본을 몇 개의 단계에 따라 시스템에서 찾습니다. 예를 들어 사용자는 먼저 네트워크에서 서버를 찾아서 선택한 다음 이 서버에서 드라이버가 액세스할 수 있는 데이터베이스를 찾습니다.  
  
 응용 프로그램 호출 **SQLBrowseConnect** 라는 연결 문자열을 전달 합니다 *요청 연결 문자열을 찾습니다* 드라이버 또는 데이터 소스를 지정 하는 합니다. 드라이버 라는 연결 문자열을 반환 합니다 *결과 문자열을 찾습니다* 키워드 (키워드 값의 불연속 집합 허용) 하는 경우 가능한 값을 포함 하는 및 친숙 한 이름. 응용 프로그램이 알기 쉬운 이름 사용 하 여 대화 상자 빌드되고 값에 대 한 사용자 라는 메시지가 표시 됩니다. 그런 다음 이러한 값에서 새 찾아보기 요청 연결 문자열 작성 하 고이를 호출 하 여 드라이버에 반환 **SQLBrowseConnect**합니다.  
  
 연결 문자열을 앞뒤로 전달 하기 때문에 응용 프로그램이 이전 버전을 반환 하는 경우 새 연결 문자열을 반환 하 여 검색 하는 여러 수준의 드라이버에 제공할 수 있습니다. 예를 들어, 처음 응용 프로그램 호출 **SQLBrowseConnect**, 드라이버는 서버 이름에 대 한 사용자에 게 프롬프트 키워드를 반환할 수 있습니다. 응용 프로그램 서버 이름을 반환 하는 경우 드라이버는 데이터베이스에 대 한 사용자에 게 프롬프트 키워드를 반환할 수 있습니다. 검색 프로세스는 응용 프로그램 데이터베이스 이름 반환 된 후 완료 것입니다.  
  
 매번 **SQLBrowseConnect** 새 찾아보기 결과 연결 문자열을 반환 SQL_NEED_DATA의 반환 코드로 반환 합니다. 이렇게 하면 연결 프로세스가 완료 되는 응용 프로그램. 될 때까지 **SQLBrowseConnect** 연결 관계 없이 SQL_SUCCESS 반환 해야 하는 데이터 상태 이며 다른 목적으로 같은 사용할 수 없습니다 연결 특성을 설정 합니다. 응용 프로그램 호출 하 여 프로세스를 검색 하는 연결을 종료할 수 있습니다 **SQLDisconnect**합니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [SQL Server 찾아보기 예제](../../../odbc/reference/develop-app/sql-server-browsing-example.md)

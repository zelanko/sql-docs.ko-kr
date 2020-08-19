---
description: SQLBrowseConnect로 연결
title: SQLBrowseConnect를 사용 하 여 연결 | Microsoft Docs
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
ms.openlocfilehash: d7ad54276f54155c68fbdbe984642dda4300a7c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424825"
---
# <a name="connecting-with-sqlbrowseconnect"></a>SQLBrowseConnect로 연결
**SQLDriverConnect**와 같은 **SQLBrowseConnect**는 연결 문자열을 사용 합니다. 그러나 **SQLBrowseConnect**을 사용 하면 응용 프로그램에서 런타임에 전체 연결 문자열을 생성할 수 있습니다. 이를 통해 애플리케이션에서는 다음 두 가지 작업이 가능해집니다.  
  
-   이 정보를 묻는 메시지를 표시 하는 대화 상자를 작성 하 여 "모양과 느낌"에 대 한 제어를 유지 합니다.  
  
-   특정 드라이버에서 사용할 수 있는 데이터 원본을 몇 개의 단계에 따라 시스템에서 찾습니다. 예를 들어 사용자는 먼저 네트워크에서 서버를 찾아서 선택한 다음 이 서버에서 드라이버가 액세스할 수 있는 데이터베이스를 찾습니다.  
  
 응용 프로그램은 **SQLBrowseConnect** 를 호출 하 고 *검색 요청 연결 문자열* 이라고 하는 연결 문자열을 전달 하 여 드라이버 또는 데이터 원본을 지정 합니다. 드라이버는 *찾아보기 결과 연결 문자열* 이라고 하는 연결 문자열을 반환 합니다. 여기에는 키워드, 가능한 값 (키워드에서 불연속 값 집합을 허용 하는 경우) 및 사용자에 게 친숙 한 이름이 포함 됩니다. 응용 프로그램은 사용자에 게 친숙 한 이름을 사용 하 여 대화 상자를 빌드하고 사용자에 게 값을 입력 하 라는 메시지를 표시 합니다. 그런 다음 이러한 값에서 새 찾아보기 요청 연결 문자열을 작성 하 고 **SQLBrowseConnect**에 대 한 다른 호출을 통해이를 드라이버로 반환 합니다.  
  
 연결 문자열이 앞뒤로 전달 되기 때문에 드라이버는 응용 프로그램에서 기존 연결 문자열을 반환할 때 새 연결 문자열을 반환 하 여 여러 수준의 검색을 제공할 수 있습니다. 예를 들어 응용 프로그램이 처음으로 **SQLBrowseConnect**를 호출 하면 드라이버에서 키워드를 반환 하 여 사용자에 게 서버 이름을 입력 하 라는 메시지를 표시할 수 있습니다. 응용 프로그램에서 서버 이름을 반환 하는 경우 드라이버는 사용자에 게 데이터베이스를 묻는 키워드를 반환할 수 있습니다. 응용 프로그램에서 데이터베이스 이름을 반환한 후에는 검색 프로세스가 완료 됩니다.  
  
 **SQLBrowseConnect** 는 새 찾아보기 결과 연결 문자열을 반환할 때마다 SQL_NEED_DATA 반환 코드로 반환 합니다. 이렇게 하면 연결 프로세스가 완료 되지 않은 것을 응용 프로그램에 알립니다. **SQLBrowseConnect** 가 SQL_SUCCESS를 반환할 때 까지는 연결이 필요한 데이터 상태 이며 연결 특성을 설정 하는 등의 다른 용도로 사용할 수 없습니다. 응용 프로그램은 **Sqldisconnect**를 호출 하 여 연결 검색 프로세스를 종료할 수 있습니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [SQL Server 찾아보기 예제](../../../odbc/reference/develop-app/sql-server-browsing-example.md)

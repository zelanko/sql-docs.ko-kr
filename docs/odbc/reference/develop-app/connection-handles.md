---
title: 연결 핸들 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: 12222653-f04d-46d6-bdee-61348f5d550f
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dc70c1ade4dcf55d6c66f4e6e44279dcc384fc25
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="connection-handles"></a>연결 핸들
A *연결* 드라이버 및 데이터 원본으로 구성 됩니다. 연결 핸들 각 연결을 식별합니다. 연결 핸들에는 드라이버를 사용할 뿐 아니라 해당 드라이버와 함께 사용 하는 데이터 원본을 정의 합니다. ODBC (드라이버 관리자 또는 드라이버)를 구현 하는 코드의 세그먼트 내 연결 핸들 다음과 같은 연결 정보를 포함 하는 구조를 식별 합니다.  
  
-   연결의 상태  
  
-   현재 연결 수준을 진단  
  
-   문 및 연결에 현재 할당 된 설명자 핸들  
  
-   각 연결 특성의 현재 설정  
  
 ODBC는 드라이버가 지 원하는 경우 여러 개의 동시 연결을 방해 되지는 않습니다. 따라서 특정 한 ODBC 환경에서 다양 한 드라이버와 같은 드라이버를 데이터 원본 및 데이터 원본 또는 데이터 원본 및 동일한 드라이버에 여러 연결에도 다양 한 여러 연결 핸들 가리킬 수 있습니다. 일부 드라이버 지 원하는; 활성 연결 수를 제한 합니다. 옵션에 SQL_MAX_DRIVER_CONNECTIONS **SQLGetInfo** 특정 드라이버에서 지 원하는 활성 연결 수를 지정 합니다.  
  
 연결 핸들을 데이터 원본에 연결할 때 주로 사용 됩니다 (**SQLConnect**, **SQLDriverConnect**, 또는 **SQLBrowseConnect**) 연결을 끊고 데이터에서 원본 (**SQLDisconnect**), 드라이버 및 데이터 원본에 대 한 정보 가져오기 (**SQLGetInfo**), 진단 검색 (**SQLGetDiagField** 및 **SQLGetDiagRec**), 트랜잭션 수행 하 고 (**SQLEndTran**). 설정 하 고 연결 특성을 가져오는 경우도 사용 됩니다 (**SQLSetConnectAttr** 및 **SQLGetConnectAttr**) 및 SQL 문의 네이티브 형식 가져올 때 (**SQLNativeSql** ).  
  
 사용 하 여 연결 핸들 할당은 **SQLAllocHandle** 로 해제 및 **SQLFreeHandle**합니다.

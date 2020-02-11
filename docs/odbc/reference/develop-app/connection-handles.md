---
title: 연결 핸들 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: 12222653-f04d-46d6-bdee-61348f5d550f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab8b94835fb9a6103436026a669c86f2401d57b0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036434"
---
# <a name="connection-handles"></a>연결 핸들
*연결은* 드라이버와 데이터 원본으로 구성 됩니다. 연결 핸들은 각 연결을 식별 합니다. 연결 핸들은 사용할 드라이버 뿐만 아니라 해당 드라이버에서 사용할 데이터 원본을 정의 합니다. ODBC (드라이버 관리자 또는 드라이버)를 구현 하는 코드 세그먼트 내에서 연결 핸들은 다음과 같이 연결 정보를 포함 하는 구조를 식별 합니다.  
  
-   연결 상태  
  
-   현재 연결 수준 진단  
  
-   연결에 현재 할당 된 문과 설명자의 핸들  
  
-   각 연결 특성의 현재 설정  
  
 드라이버가 지 원하는 경우 ODBC는 여러 동시 연결을 방지 하지 않습니다. 따라서 특정 ODBC 환경에서 여러 연결 핸들은 다양 한 드라이버 및 데이터 원본, 동일한 드라이버와 다양 한 데이터 원본 또는 동일한 드라이버와 데이터 원본에 대 한 여러 연결을 가리킬 수 있습니다. 일부 드라이버는 지원 되는 활성 연결 수를 제한 합니다. **SQLGetInfo** 의 SQL_MAX_DRIVER_CONNECTIONS 옵션은 특정 드라이버가 지 원하는 활성 연결 수를 지정 합니다.  
  
 연결 핸들은 데이터 원본 (**SQLConnect**, **SQLDriverConnect**또는 **SQLBrowseConnect**)에 연결 하 고, 데이터 원본에서 연결을 끊고 (**sqldisconnect**), 드라이버 및 데이터 원본 (**SQLGetInfo**)에 대 한 정보를 가져오고, 진단을 검색 (**SQLGetDiagField** 및 **SQLGetDiagRec**) 하 고, 트랜잭션 (**sqlendtran**)을 수행할 때 주로 사용 됩니다. 연결 특성 (**SQLSetConnectAttr** 및 **SQLGetConnectAttr**)을 설정 하 고 가져올 때와 SQL 문의 네이티브 형식 (**SQLNativeSql**)을 가져올 때도 사용 됩니다.  
  
 연결 핸들은 **SQLAllocHandle** 를 사용 하 여 할당 되며 **sqlfreehandle**을 사용 하 여 해제 됩니다.

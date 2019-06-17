---
title: 진단 레코드 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- handles [ODBC], diagnostic records
- header records [ODBC]
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 92c73f9b-3ed7-410d-9cec-2771004aae60
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 928e9ffa4701568aac8c519a23e7e371596a36eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63242340"
---
# <a name="diagnostic-records"></a>진단 레코드
각 환경에 연결, 연결, 문 및 설명자 핸들은 *진단 레코드*합니다. 이러한 레코드는 특정 핸들을 사용 하는 마지막 함수 호출에 대 한 진단 정보를 포함 합니다. 레코드는 해당 핸들을 사용 하 여 다른 함수를 호출할 경우에 대체 됩니다. 한 번에 저장할 수 있는 진단 레코드의 수 제한은 없습니다.  
  
 진단 레코드의 두 종류가 있습니다:는 *헤더 레코드* 및 0 개 이상의 *상태 레코드*합니다. 헤더 레코드는 레코드 0; 상태 레코드는 레코드 1 이상입니다. 진단 레코드는 헤더 레코드 및 상태 레코드에 대 한 다른 별도 필드를 숫자로 구성 됩니다. 또한 ODBC 구성 요소 자체 진단 레코드 필드를 정의할 수 있습니다.  
  
 진단 레코드 구조도 생각할 수 있습니다, 있지만 실제로 구조; 수 있도록 요구 사항은 없습니다. 드라이버 진단 정보를 저장 하는 방법을 드라이버 관련 됩니다.  
  
 진단 레코드의 필드를 통해 검색 됩니다 **SQLGetDiagField**합니다. 사용 하 여 단일 호출에서 SQLSTATE, 원시 오류 번호 및 상태 레코드의 진단 메시지 필드를 검색할 수 있습니다 **SQLGetDiagRec**합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [헤더 레코드](../../../odbc/reference/develop-app/header-record.md)  
  
-   [상태 레코드](../../../odbc/reference/develop-app/status-records.md)

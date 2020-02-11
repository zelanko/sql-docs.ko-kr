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
ms.openlocfilehash: 90133b4a18876c52b9b6b6bffbe4c8c02c953e07
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039885"
---
# <a name="diagnostic-records"></a>진단 레코드
각 환경, 연결, 문 및 설명자 핸들은 *진단 레코드*입니다. 이러한 레코드는 특정 핸들을 사용 하는 라는 마지막 함수에 대 한 진단 정보를 포함 합니다. 해당 핸들을 사용 하 여 다른 함수를 호출 하는 경우에만 레코드가 바뀝니다. 한 번에 저장할 수 있는 진단 레코드 수에는 제한이 없습니다.  
  
 진단 레코드에는 *헤더 레코드* 와 0 개 이상의 *상태 레코드*라는 두 가지 유형이 있습니다. 헤더 레코드는 레코드 0입니다. 상태 레코드는 1 이상 레코드입니다. 진단 레코드는 헤더 레코드 및 상태 레코드에 대해 서로 다른 여러 개별 필드로 구성 됩니다. 또한 ODBC 구성 요소는 자체 진단 레코드 필드를 정의할 수 있습니다.  
  
 진단 레코드를 구조체로 간주할 수 있지만 실제로 구조를 가질 필요는 없습니다. 드라이버에서 진단 정보를 저장 하는 방법은 드라이버와 관련 됩니다.  
  
 진단 레코드의 필드는 **SQLGetDiagField**를 사용 하 여 검색 됩니다. 상태 레코드의 SQLSTATE, 원시 오류 번호 및 진단 메시지 필드는 **SQLGetDiagRec**를 사용 하 여 단일 호출에서 검색할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [헤더 레코드](../../../odbc/reference/develop-app/header-record.md)  
  
-   [상태 레코드](../../../odbc/reference/develop-app/status-records.md)

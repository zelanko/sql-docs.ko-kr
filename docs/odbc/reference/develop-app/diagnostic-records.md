---
title: 진단 기록 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b564f2837bc76e04011170e191d00c08d10c119d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305184"
---
# <a name="diagnostic-records"></a>진단 레코드
각 환경, 연결, 명령문 및 설명자 핸들과 연결된 *진단 레코드입니다.* 이러한 레코드에는 특정 핸들을 사용한 마지막 함수에 대한 진단 정보가 포함됩니다. 레코드는 해당 핸들을 사용하여 다른 함수를 호출할 때만 대체됩니다. 한 번에 저장할 수 있는 진단 레코드 의 수에는 제한이 없습니다.  
  
 진단 레코드에는 *헤더 레코드와* 0 개 이상의 상태 레코드의 두 가지 *유형이 있습니다.* 헤더 레코드는 레코드 0입니다. 상태 레코드는 레코드 1 이상입니다. 진단 레코드는 헤더 레코드 및 상태 레코드에 대해 서로 다른 여러 개의 개별 필드로 구성됩니다. 또한 ODBC 구성 요소는 자체 진단 레코드 필드를 정의할 수 있습니다.  
  
 진단 기록은 구조로 생각할 수 있지만 실제로 구조가 될 필요는 없습니다. 드라이버가 진단 정보를 저장하는 방법은 드라이버에 따라 다릅니다.  
  
 진단 레코드의 필드는 **SQLGetDiagField**. **SQLGetDiagRec**를 사용 하 고 단일 호출에서 상태 레코드의 SQLSTATE, 기본 오류 번호 및 진단 메시지 필드를 검색할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [헤더 레코드](../../../odbc/reference/develop-app/header-record.md)  
  
-   [상태 레코드](../../../odbc/reference/develop-app/status-records.md)

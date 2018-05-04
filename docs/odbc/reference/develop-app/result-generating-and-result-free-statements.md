---
title: 결과 생성 및 결과 필요 없는 문을 | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- result-generating statements [ODBC]
- batches [ODBC], result-generating statements
- batches [ODBC], result-free statements
- SQL statements [ODBC], batches
- result-free statements [ODBC]
ms.assetid: 2f3475d1-3999-4dd8-aba2-a6e1299c95f8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1cc68c7ca0528d2a8af2af5d33d92fb8bf92c64f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="result-generating-and-result-free-statements"></a>결과 생성 하 고 결과 필요 없는 문
SQL 문은 다음과 같은 5 개의 범주로 느슨하게 나눌 수 있습니다.  
  
-   **결과 집합 생성 문을** 다음은 결과 집합을 생성 하는 SQL 문입니다. 예를 들어 한 **선택** 문.  
  
-   **행 개수를 생성 하는 문을** 이들은 영향을 받는 행의 개수를 생성 하는 SQL 문입니다. 예를 들어 한 **업데이트** 또는 **삭제** 문.  
  
-   **데이터 정의 언어 (DDL) 문을** 이들은 데이터베이스의 구조를 수정 하는 SQL 문입니다. 예를 들어 **CREATE TABLE** 또는 **DROP INDEX**합니다.  
  
-   **컨텍스트 변경 문을** 이들은 데이터베이스의 컨텍스트를 변경 하는 SQL 문입니다. 예를 들어는 **사용** 및 **설정** SQL Server에서 문.  
  
-   **관리 문을** 이들은 데이터베이스에서 관리 용도로 사용 되는 SQL 문의 합니다. 예를 들어 **GRANT** 및 **해지**합니다.  
  
 처음 두 가지 범주에 있는 SQL 문을 이라고 통칭 *문 결과 생성*합니다. 후자는 세 가지 범주에 있는 SQL 문을 이라고 통칭 *문 결과 필요 없는*합니다. ODBC 문 결과 생성을 포함 하는 일괄 처리의 의미 체계를 정의 합니다. 이러한 의미 체계 매우 다양 하며 따라서 데이터 원본에 따른 특정 합니다. 예를 들어 개체를 삭제 하는 중 다음으로 참조 하거나 다시 동일한 일괄 처리의 동일한 개체를 만드는 SQL Server 드라이버가 지원 하지 않습니다. 따라서 용어 *일괄 처리* 결과 생성의 일괄 처리만이 설명서 참조에서 사용 되는 문입니다.

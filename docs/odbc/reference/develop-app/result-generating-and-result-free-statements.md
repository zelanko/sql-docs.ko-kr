---
title: 결과 생성 및 결과 없는 문 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result-generating statements [ODBC]
- batches [ODBC], result-generating statements
- batches [ODBC], result-free statements
- SQL statements [ODBC], batches
- result-free statements [ODBC]
ms.assetid: 2f3475d1-3999-4dd8-aba2-a6e1299c95f8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f357576e9e7510ae581b41a50976a34981f35109
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52517350"
---
# <a name="result-generating-and-result-free-statements"></a>결과 생성 및 결과 없는 명령문
SQL 문 다음 다섯 가지 범주로 나눌 수 느슨하게:  
  
-   **결과 집합 생성 문** 다음은 결과 집합을 생성 하는 SQL 문입니다. 예를 들어, 한 **선택** 문입니다.  
  
-   **행 수가 생성 문** 이들은 영향을 받는 행의 개수를 생성 하는 SQL 문입니다. 예를 들어를 **업데이트** 하거나 **삭제** 문입니다.  
  
-   **DDL (데이터 정의 언어) 문이** 이 데이터베이스의 구조를 수정 하는 SQL 문입니다. 예를 들어 **CREATE TABLE** 하거나 **DROP INDEX**합니다.  
  
-   **컨텍스트 변경 문을** 이 데이터베이스의 컨텍스트를 변경 하는 SQL 문입니다. 예를 들어를 **사용 하 여** 하 고 **설정** SQL Server에서 문.  
  
-   **관리 문이** 이 SQL 문을 데이터베이스에서 관리 목적으로 사용 합니다. 예를 들어 **권한 부여** 하 고 **REVOKE**합니다.  
  
 처음 두 가지 범주에 있는 SQL 문을 라고 통칭 *결과 생성할 문을*합니다. 후자는 세 가지 범주에 있는 SQL 문을 라고 통칭 *결과 없는 문*합니다. ODBC 결과 생성 하는 문을 포함 하는 일괄 처리의 의미 체계를 정의 합니다. 이러한 의미 체계 매우 다양 하므로 데이터 소스 관련 있습니다. 예를 들어 개체를 삭제 한 다음 참조 또는 다시 동일한 일괄 처리에 있는 동일한 개체를 만드는 SQL Server 드라이버가 지원 하지 않습니다. 따라서 용어 *일괄 처리* 결과 생성 하는 일괄 처리에만이 설명서 참조에서 사용 되는 문입니다.

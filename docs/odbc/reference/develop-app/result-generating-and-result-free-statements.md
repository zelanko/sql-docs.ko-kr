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
ms.openlocfilehash: 55b2ff4d428f02b59883b675fde95531366f0b4d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020606"
---
# <a name="result-generating-and-result-free-statements"></a>결과 생성 및 결과 없는 명령문
SQL 문은 다음과 같은 5 가지 범주로 느슨하게 나눌 수 있습니다.  
  
-   **결과 집합 생성 문** 결과 집합을 생성 하는 SQL 문입니다. 예를 들어 **select** 문입니다.  
  
-   **행 개수-생성 문** 영향을 받는 행의 수를 생성 하는 SQL 문입니다. 예를 들어 **UPDATE** 또는 **DELETE** 문이 있습니다.  
  
-   **DDL (데이터 정의 언어) 문** 데이터베이스의 구조를 수정 하는 SQL 문입니다. 예를 들어 **CREATE TABLE** 또는 **DROP INDEX**입니다.  
  
-   **컨텍스트 변경 문** 데이터베이스의 컨텍스트를 변경 하는 SQL 문입니다. 예를 들어 SQL Server의 **USE** 및 **SET** 문이 있습니다.  
  
-   **관리 문** 데이터베이스에서 관리 목적으로 사용 되는 SQL 문입니다. 예: **GRANT** 및 **REVOKE**.  
  
 처음 두 범주의 SQL 문을 *결과 생성 문*이라고 통칭 합니다. 후자의 세 가지 범주에 있는 SQL 문은 전체적으로 *결과 없는 문*이라고 합니다. ODBC는 결과 생성 문만 포함 하는 일괄 처리의 의미 체계를 정의 합니다. 이러한 의미 체계는 광범위 하 게 다르며 따라서 데이터 원본에 따라 다릅니다. 예를 들어 SQL Server 드라이버는 개체를 삭제 한 다음 동일한 일괄 처리에서 동일한 개체를 참조 하거나 다시 만드는 것을 지원 하지 않습니다. 따라서이 설명서에 사용 된 *일괄 처리* 는 결과 생성 문의 일괄 처리만 참조 합니다.

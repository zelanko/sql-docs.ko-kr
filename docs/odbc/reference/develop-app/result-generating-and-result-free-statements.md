---
title: 결과 생성 및 결과 없는 문장 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fc94aabd7982fba5879519573980db03b1857ef6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300093"
---
# <a name="result-generating-and-result-free-statements"></a>결과 생성 및 결과 없는 명령문
SQL 문은 다음 다섯 가지 범주로 느슨하게 나눌 수 있습니다.  
  
-   **결과 집합 생성 문** 결과 집합을 생성하는 SQL 문입니다. 예를 들어 **SELECT** 문을 클릭합니다.  
  
-   **행 카운트 생성 명령문** 영향을 받는 행의 수를 생성하는 SQL 문입니다. 예를 들어 **업데이트** 또는 DELETE 문을 **작성합니다.**  
  
-   **데이터 정의 언어(DDL) 명령문** 데이터베이스의 구조를 수정하는 SQL 문입니다. 예를 들어 테이블 또는 **놓기 인덱스를** **만듭니다.**  
  
-   **컨텍스트 변경 문** 데이터베이스의 컨텍스트를 변경하는 SQL 문입니다. 예를 들어 SQL Server의 **USE** 및 SET 문을 예로 **들** 수 있습니다.  
  
-   **관리 명세서** 데이터베이스의 관리 목적으로 사용되는 SQL 문입니다. 예를 **들어, 권한 부여** 및 **해지.**  
  
 처음 두 범주의 SQL 문은 *결과 생성 문으로 통칭합니다.* 후자의 세 가지 범주의 SQL 문은 결과 *없는 문으로*통칭됩니다. ODBC는 결과 생성 문만 포함하는 일괄 처리의 의미 체계를 정의합니다. 이러한 의미 체계는 매우 다양하므로 데이터 원본에 따라 다릅니다. 예를 들어 SQL Server 드라이버는 개체 삭제를 지원하지 않으며 동일한 일괄 처리에서 동일한 개체를 참조하거나 다시 만드는 것을 지원하지 않습니다. 따라서 이 설명서에 사용된 *일괄 처리라는* 용어는 결과 생성 문의 일괄 처리만 을 나타냅니다.

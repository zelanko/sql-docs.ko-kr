---
title: 카탈로그 함수에서 반환 된 데이터 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d27d395913ce64d263798205521a3d1136460105
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="data-returned-by-catalog-functions"></a>카탈로그 함수에서 반환 된 데이터
각 카탈로그 함수는 데이터를 결과 집합으로 반환 합니다. 이 결과 집합은 다른 결과 집합에서 다르지 않습니다. 일반적으로 생성 되는 미리 정의 된 의해 매개 변수화 **선택** 드라이버에 하드 코드 또는 데이터 원본에 프로시저에서 저장 된 문입니다. 결과 집합에서 데이터를 검색 하는 방법에 대 한 정보를 참조 하십시오. [는 결과 집합 생성 된?](../../../odbc/reference/develop-app/was-a-result-set-created.md)합니다.  
  
 결과 집합에 각 카탈로그 함수는 해당 함수에 대 한 참조 항목에 설명 되어 있습니다. 나열된 된 열 뿐만 아니라 결과 집합의 마지막 미리 정의 된 열 뒤 드라이버 관련 열을 포함할 수 있습니다. 이러한 열 (있는 경우) 드라이버 설명서에 설명 되어 있습니다.  
  
 응용 프로그램 결과 집합의 끝을 기준으로 드라이버 관련 열을 바인딩해야 합니다. 즉,은 마지막 열 수가 드라이버 관련 열 번호를 계산 해야-사용 하 여 검색 **SQLNumResultCols** — 필요한 열 이후에 발생 하는 열 수를 뺀 합니다. 이 인해 결과에 새 열을 추가할 때 응용 프로그램을 변경 하지는 버전의 ODBC 또는 드라이버 나중에 설정 합니다. 이 계획을 사용 하려면 드라이버 열 번호는 결과 집합의 끝을 기준으로 변경 되지 않는 이전 드라이버 관련 열 앞에 새 드라이버별 열 추가 해야 합니다.  
  
 결과 집합에 반환 되는 식별자는 특수 문자를 포함 하는 경우에 인용 되지 않습니다. 예를 들어 식별자 역따옴표 문자 (드라이버 관련 되며를 통해 반환 된 **SQLGetInfo**) 큰따옴표 (") 이며 Accounts Payable 테이블 Customer Name 이라는 열이 포함 됩니다. 반환 된 행에 **SQLColumns** TABLE_NAME 열의 값이이 열에 대 한 Accounts Payable, 없습니다 "Accounts Payable"는 이며 COLUMN_NAME 열 값 고객 이름, "Customer Name" 하지 않습니다. Accounts Payable 테이블에 고객의 이름이 검색 하려면 응용 프로그램에는 이러한 이름을 인용은:  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 자세한 내용은 참조 [따옴표 붙은 식별자](../../../odbc/reference/develop-app/quoted-identifiers.md)합니다.  
  
 카탈로그 함수 연결할 사용자 이름 및 암호를 기반 하 고 반환 되는 사용자가 권한 있는 데이터만 있는 SQL 유사 권한 부여 모델을 기반으로 합니다. 이 모델에 맞지 않는는 개별 파일의 암호 보호는 드라이버 정의입니다.  
  
 카탈로그 함수에서 반환 된 결과 집합 업데이트 거의 될 수 있으며 이러한 결과 집합의 데이터를 변경 하 여 데이터베이스의 구조를 변경 하려면 응용 프로그램에 필요 하지 않습니다.

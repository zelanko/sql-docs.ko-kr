---
title: 카탈로그 함수에서 반환 된 데이터 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d68c1a5a1b45ce5a3923ae1b4b346ae786ea9a4a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47857261"
---
# <a name="data-returned-by-catalog-functions"></a>카탈로그 함수에 의해 반환된 데이터
각 카탈로그 함수는 데이터를 결과 집합으로 반환 합니다. 이 결과 집합은 다른 결과 집합에 다르지 않습니다. 일반적으로 생성 되는 여는 미리 정의 된 매개 변수가 **선택** 드라이버에 하드 코딩 또는 프로시저는 데이터 원본에 저장 된 문입니다. 결과 집합에서 데이터를 검색 하는 방법에 대 한 정보를 참조 하세요 [는 결과 집합 생성 된?](../../../odbc/reference/develop-app/was-a-result-set-created.md)합니다.  
  
 결과 집합에 각 카탈로그 함수는 해당 함수에 대 한 참조 항목에 설명 되어 있습니다. 나열된 된 열 외에도 결과 집합의 마지막 미리 정의 된 열 뒤 드라이버 관련 열을 포함할 수 있습니다. 이러한 열 (해당 되는 경우) 드라이버 설명서에 설명 되어 있습니다.  
  
 응용 프로그램에는 결과 집합의 끝을 기준으로 드라이버 관련 열 바인딩해야 합니다. 즉,은 마지막 열 수가 드라이버별 열 개수를 계산 해야-사용 하 여 검색 **SQLNumResultCols** -덜 필요한 열 뒤에 발생 하는 열의 수입니다. ODBC의 버전 또는 드라이버를 새 열을 결과에 추가할 때 응용 프로그램을 변경 하지 않아도이 저장 나중에 설정 합니다. 이 계획을 사용 하려면 드라이버는 결과 집합의 끝을 기준으로 열 번호를 변경 하지 마십시오 이전 드라이버별 열 앞에 새 드라이버별 열 추가 해야 합니다.  
  
 결과 집합에 반환 되는 식별자는 하지 인용 부호로 특수 문자를 포함 하는 경우에 합니다. 예를 들어 식별자 인용 문자 (드라이버별 및 통해 반환 된 **SQLGetInfo**) 큰따옴표 (") 이며 Accounts Payable 테이블 고객 이름 이라는 열이 포함 됩니다. 반환한 행의 **SQLColumns** TABLE_NAME 열의 값이이 열에 대 한 Accounts Payable, 없습니다 "Accounts Payable"는 이며 COLUMN_NAME 열 값 고객 이름, "Customer Name" 하지 않습니다. Accounts Payable 테이블에서 고객의 이름이 검색 하려면 응용 프로그램에는 이러한 이름은 인용는:  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 자세한 내용은 [따옴표 붙은 식별자](../../../odbc/reference/develop-app/quoted-identifiers.md)합니다.  
  
 카탈로그 함수는 연결할 사용자 이름 및 암호 기반 및 사용자에는 권한 있는 데이터만 반환 되는 SQL과 유사한 권한 부여 모델을 기반으로 합니다. 이 모델에 적합 하지 않습니다는 개별 파일의 암호 보호 드라이버 정의 됩니다.  
  
 카탈로그 함수에서 반환한 결과 집합을 업데이트할 수 있는 거의 발생 하지 않는다는 되며 이러한 결과 집합의 데이터를 변경 하 여 데이터베이스의 구조를 변경 하려면 응용 프로그램을 기대할 수 없습니다.

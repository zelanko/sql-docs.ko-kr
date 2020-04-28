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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0d9b63de04f79fd95c1b06d8e84d85c6f4fea02
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305234"
---
# <a name="data-returned-by-catalog-functions"></a>카탈로그 함수에 의해 반환된 데이터
각 카탈로그 함수는 데이터를 결과 집합으로 반환 합니다. 이 결과 집합은 다른 결과 집합과 다르지 않습니다. 일반적으로 드라이버에서 하드 코딩 되거나 데이터 원본의 프로시저에 저장 된 미리 정의 된 매개 변수가 있는 **SELECT** 문에서 생성 됩니다. 결과 집합에서 데이터를 검색 하는 방법에 대 한 자세한 내용은 [생성 된 결과 집합을](../../../odbc/reference/develop-app/was-a-result-set-created.md)참조 하세요.  
  
 각 카탈로그 함수의 결과 집합은 해당 함수에 대 한 참조 항목에서 설명 합니다. 나열 된 열 외에도 결과 집합에는 마지막으로 미리 정의 된 열 다음에 드라이버별 열이 포함 될 수 있습니다. 이러한 열 (있는 경우)은 드라이버 설명서에 설명 되어 있습니다.  
  
 응용 프로그램은 결과 집합의 끝을 기준으로 드라이버 특정 열을 바인딩해야 합니다. 즉, 필수 열 다음에 발생 하는 열 수를 사용 하지 않는 경우 **Sqlnumresultcols** 를 사용 하 여 마지막으로 검색 한 열의 수를 계산 합니다. 이렇게 하면 이후 버전의 ODBC 또는 드라이버에서 결과 집합에 새 열이 추가 될 때 응용 프로그램을 변경 해야 합니다. 이 체계가 작동 하려면 드라이버에서 이전 드라이버별 열 앞에 새 드라이버별 열을 추가 하 여 결과 집합의 끝을 기준으로 열 번호가 변경 되지 않도록 해야 합니다.  
  
 특수 문자를 포함 하는 경우에도 결과 집합에 반환 되는 식별자는 따옴표로 묶여 있지 않습니다. 예를 들어 식별자 따옴표 문자 (드라이버별 및 **SQLGetInfo**를 통해 반환 됨)가 큰따옴표 (")이 고 외상 매입금 테이블에 Customer Name 이라는 열이 포함 되어 있다고 가정 합니다. 이 열에 대 한 **Sqlcolumns** 에서 반환 된 행에서 TABLE_NAME 열 값은 "외상 매입금"이 아닌 외상 매입금 이며 COLUMN_NAME 열의 값은 "customer name"이 아닌 고객 이름입니다. 외상 매입금 테이블에서 고객의 이름을 검색 하기 위해 응용 프로그램은 다음 이름을 인용 합니다.  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 자세한 내용은 [따옴표 붙은 식별자](../../../odbc/reference/develop-app/quoted-identifiers.md)를 참조 하세요.  
  
 카탈로그 함수는 사용자 이름 및 암호를 기반으로 연결이 설정 되 고 사용자에 게 권한이 있는 데이터만 반환 되는 SQL과 유사한 권한 부여 모델을 기반으로 합니다. 이 모델에 맞지 않는 개별 파일의 암호 보호는 드라이버에 정의 되어 있습니다.  
  
 카탈로그 함수에서 반환 되는 결과 집합은 거의 업데이트할 수 없으며, 응용 프로그램은 이러한 결과 집합에서 데이터를 변경 하 여 데이터베이스의 구조를 변경할 수 없습니다.

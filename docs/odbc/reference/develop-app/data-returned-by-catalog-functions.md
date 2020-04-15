---
title: 카탈로그 함수에서 반환되는 데이터 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305234"
---
# <a name="data-returned-by-catalog-functions"></a>카탈로그 함수에 의해 반환된 데이터
각 카탈로그 함수는 결과 집합으로 데이터를 반환합니다. 이 결과 집합은 다른 결과 집합과 다르지 않습니다. 일반적으로 드라이버에서 하드 코딩하거나 데이터 원본의 프로시저에 저장된 미리 정의된 매개 변수화된 **SELECT** 문에 의해 생성됩니다. 결과 집합에서 데이터를 검색하는 방법에 대한 자세한 내용은 [결과 집합이 만들어졌습니까?](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
 각 카탈로그 함수에 대한 결과 집합은 해당 함수의 참조 항목에 설명되어 있습니다. 나열된 열 외에도 결과 집합에는 미리 정의된 마지막 열 다음의 드라이버 별 열이 포함될 수 있습니다. 이러한 열(있는 경우)은 드라이버 설명서에 설명되어 있습니다.  
  
 응용 프로그램은 결과 집합의 끝을 기준으로 드라이버 관련 열을 바인딩해야 합니다. 즉, **SQLNumResultCols로** 검색된 마지막 열의 수로 드라이버 관련 열의 수를 계산해야 합니다. 이렇게 하면 ODBC 또는 드라이버의 이후 버전에서 설정된 결과에 새 열이 추가될 때 응용 프로그램을 변경할 필요가 없습니다. 이 스키마가 작동하려면 드라이버가 결과 집합의 끝을 기준으로 열 번호가 변경되지 않도록 이전 드라이버 별 열 앞에 새 드라이버 관련 열을 추가해야 합니다.  
  
 결과 집합에 반환되는 식별자는 특수 문자를 포함하는 경우에도 따옴표로 지정되지 않습니다. 예를 들어 식별자 따옴표 문자(드라이버별 및 **SQLGetInfo를**통해 반환됨)가 이중 따옴표(")이고 계정 지급 테이블에 고객 이름이라는 열이 포함되어 있다고 가정합니다. 이 열에 대해 **SQLColumns에서** 반환된 행에서 TABLE_NAME 열의 값은 "미지급금"이 아닌 미지급 계정이며 COLUMN_NAME 열의 값은 "고객 이름"이 아니라 고객 이름입니다. 미지급금 지급 자 테이블의 고객 이름을 검색하려면 응용 프로그램에서 다음 이름을 인용합니다.  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 자세한 내용은 [인용 식별자를](../../../odbc/reference/develop-app/quoted-identifiers.md)참조하십시오.  
  
 카탈로그 함수는 사용자 이름과 암호를 기반으로 연결이 이루어지고 사용자에게 권한이 있는 데이터만 반환되는 SQL과 같은 권한 부여 모델을 기반으로 합니다. 이 모델에 맞지 않는 개별 파일의 암호 보호는 드라이버 정의입니다.  
  
 카탈로그 함수에서 반환되는 결과 집합은 거의 업데이터 화할 수 없으며 응용 프로그램은 이러한 결과 집합의 데이터를 변경하여 데이터베이스 구조를 변경할 수 있어야 합니다.

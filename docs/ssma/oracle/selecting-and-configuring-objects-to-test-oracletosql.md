---
title: 테스트할 개체 선택 및 구성 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Selection of Objects to Test,Parameter Comparison Settings
ms.assetid: 29fb6542-5c1f-4b14-a822-87700beb7623
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: e0a8e7650534d50c5e5d7c3b02f2857764d9c2ca
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68264638"
---
# <a name="selecting-and-configuring-objects-to-test-oracletosql"></a>테스트할 개체 선택 및 구성(OracleToSQL)
이 단계에서는 테스트할 개체를 선택 하 고 프로시저의 반환 값 뿐만 아니라 프로시저의 출력 매개 변수 및 함수를 비교 하기 위한 설정을 구성 합니다.  
  
## <a name="selection-of-objects-to-test"></a>테스트할 개체 선택  
창 왼쪽에 있는 Oracle 개체 트리에서 테스트 프로세스 중에 호출 하려는 개체를 확인 합니다. [마이그레이션된 데이터베이스 개체 테스트 &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md) 항목에서 테스트 가능한 개체의 전체 목록을 참조 하세요.  
  
SSMA 테스터는 테스트를 위해 선택한 개체를 지원 하지 않는 경우 개체 트리 아래에 **선택한 일부 개체에 오류가** 있습니다 라는 링크가 표시 됩니다. 이 링크를 클릭 하 여 이러한 개체를 테스트할 수 없는 이유를 확인 하 고 잘못 된 개체 선택을 지울 수 있습니다.  
  
오른쪽에서 여러 페이지를 볼 수 있습니다. **SQL** 페이지에서 현재 개체의 정의를 표시 합니다. **매개 변수** 페이지에는 개체가 저장 프로시저 또는 함수인 경우 매개 변수가 나열 됩니다. **속성** 페이지는 개체의 추가 특성을 표시 합니다. 아래의 **매개 변수 비교** 및 **호출 값** 페이지에 대 한 설명을 참조 하세요.  
  
## <a name="parameter-comparison-settings"></a>매개 변수 비교 설정  
**매개 변수 비교** 페이지에서 출력 매개 변수 및 반환 값에 대 한 비교 규칙을 설정 합니다. 다음과 같이 설정할 수 있습니다.  
  
### <a name="use-during-test-comparisons"></a>테스트 비교 중 사용  
테스트 결과 비교에서 선택한 매개 변수를 사용 하도록 설정 합니다.  
  
-   **True**를 선택 하면 Ssma는 Oracle에서 프로시저를 실행 한 후 SQL Server의 해당 값을 사용 하 여이 매개 변수의 출력 값을 비교 합니다.
  
-   **False**를 선택 하면 매개 변수가 결과 확인에서 제외 됩니다.  
  
### <a name="use-custom-scale"></a>사용자 지정 배율 사용  
숫자 데이터 형식의 매개 변수는 비교를 위해 사용자 지정 배율을 설정할 수 있습니다.  
  
-   **True**를 선택 하는 경우 비교 하기 전에 **비교 배율** 값에 따라 숫자 값이 반올림 됩니다.  
  
-   **False**를 선택 하면 숫자 비교가 정확 하 게 됩니다.  
  
### <a name="comparing-scale"></a>배율 비교  
**사용자 지정 배율 사용** 옵션을 **True**로 설정한 경우에만 사용할 수 있습니다. 숫자 비교의 전체 자릿수입니다.  
  
### <a name="date-time-comparing"></a>비교 날짜 시간  
날짜/시간 값을 비교 하는 방법을 정의 합니다.  
  
-   **전체 날짜 비교**를 선택 하면 두 플랫폼의 값에 대 한 전체 비교가 수행 됩니다.  
  
-   **날짜만 비교**를 선택 하는 경우 시간 부분은 무시 됩니다.  
  
-   **시간만 비교**를 선택 하는 경우 날짜 부분은 무시 됩니다.  
  
-   **밀리초 무시**를 선택 하면 결과가 최대 초까지 비교 됩니다.  
  
-   **날짜 및 밀리초 무시**를 선택 하면 결과는 시간 부분에 의해서만 비교 되 고 초의 소수 부분은 무시 됩니다.  
  
### <a name="ignore-strings-case"></a>문자열 대/소문자 무시  
비교의 대/소문자 구분 여부를 제어 합니다.  
  
-   **True**를 선택 하면 비교 시 대/소문자를 구분 하지 않습니다.  
  
-   **False**를 선택 하면 비교 시 대/소문자를 구분 합니다.  
  
### <a name="ignore-trailing-spaces"></a>후행 공백 무시  
비교 중 후행 공백이 처리 되는 방식을 제어 합니다.  
  
-   **True**를 선택 하면 비교 하는 문자열이 비교 되기 전에 오른쪽으로 잘립니다.  
  
-   **False**를 선택 하면 비교 되는 문자열은 후행 공백을 유지 합니다.  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>프로시저 및 함수에 대 한 입력 값 지정 (호출 값)  
**호출 값** 페이지에서 입력 매개 변수 값을 지정할 수 있습니다. **호출 추가** 단추는 빈 매개 변수 값을 사용 하 여 새 호출을 추가 합니다. **호출 제거** 단추를 클릭 하면 현재 호출이 제거 됩니다.  
  
## <a name="next-step"></a>다음 단계  
[영향을 받는 개체 선택 및 구성 &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
## <a name="see-also"></a>참고 항목  
[OracleToSQL&#41;&#40;마이그레이션된 데이터베이스 개체 테스트](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

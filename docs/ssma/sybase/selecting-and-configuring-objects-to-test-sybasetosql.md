---
description: 테스트할 개체 선택 및 구성(SybaseToSQL)
title: 테스트할 개체 선택 및 구성 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Parameter Comparision Setting
- Tester Component,Selecting Objects
ms.assetid: 89c23aad-bfee-4917-bc16-175288390ac0
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: c6bcddffdbb524e10a0686e6e9a82f4abcd30db8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492146"
---
# <a name="selecting-and-configuring-objects-to-test-sybasetosql"></a>테스트할 개체 선택 및 구성(SybaseToSQL)
이 단계에서는 테스트할 개체를 선택 하 고 프로시저의 반환 값 뿐만 아니라 프로시저의 출력 매개 변수 및 함수를 비교 하기 위한 설정을 구성 합니다.  
  
## <a name="selection-of-objects-to-test"></a>테스트할 개체 선택  
창 왼쪽에 있는 Sybase 개체 트리에서 테스트 프로세스 중에 호출 하려는 개체를 확인 합니다. [마이그레이션된 데이터베이스 개체 테스트 &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md) 항목에서 테스트 가능한 개체의 전체 목록을 참조 하세요.  
  
SSMA 테스터는 테스트를 위해 선택한 개체를 지원 하지 않는 경우 개체 트리 아래에 **선택한 일부 개체에 오류가** 있습니다 라는 링크가 표시 됩니다. 이 링크를 클릭 하 여 이러한 개체를 테스트할 수 없는 이유를 확인 하 고 잘못 된 개체 선택을 지울 수 있습니다.  
  
오른쪽에서 여러 페이지를 볼 수 있습니다. **SQL** 페이지에서 현재 개체의 정의를 표시 합니다. **Sql 사전 sql** 및 **사후 sql** 페이지에서 테스트 개체 호출이 시작 되기 전후에 실행 되는 스크립트를 지정할 수 있습니다. 이는 개체가 임시 테이블이 나 커서와 같은 추가 개체를 필요로 하는 경우에 유용할 수 있습니다. **매개 변수** 페이지에는 개체가 저장 프로시저 또는 함수인 경우 매개 변수가 나열 됩니다. **속성** 페이지는 개체의 추가 특성을 표시 합니다. 아래의 **매개 변수 Comparsions** 및 **호출 값** 페이지에 대 한 설명을 참조 하세요.  
  
## <a name="parameter-comparison-settings"></a>매개 변수 비교 설정  
**매개 변수 비교** 페이지에서 출력 매개 변수 및 반환 값에 대 한 비교 규칙을 설정 합니다. 다음과 같이 설정할 수 있습니다.  
  
### <a name="use-during-comparisons"></a>비교 하는 동안 사용  
테스트 결과 비교에서 선택한 매개 변수를 사용 하도록 설정 합니다.  
  
-   **True**를 선택 하는 경우 ssma는에 해당 하는 값을 사용 하 여 Sybase에서 프로시저를 실행 한 후이 매개 변수의 출력 값을 비교 합니다.[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   **False**를 선택 하면 매개 변수가 결과 확인에서 제외 됩니다.  
  
### <a name="use-custom-scale"></a>사용자 지정 배율 사용  
근사 길이와 고정 길이 숫자 데이터 형식의 매개 변수의 경우 비교에 대 한 사용자 지정 배율을 설정할 수 있습니다.  
  
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
[영향을 받는 개체 선택 및 구성 &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
  
## <a name="see-also"></a>참고 항목  
[마이그레이션된 데이터베이스 개체 테스트 &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  

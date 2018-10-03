---
title: (SybaseToSQL) 테스트할 개체 선택 및 구성 | Microsoft Docs
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2b8d842e9febc94d35f2a8c53c6106159f44423a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47741831"
---
# <a name="selecting-and-configuring-objects-to-test-sybasetosql"></a>테스트할 개체 선택 및 구성(SybaseToSQL)
이 단계에서 테스트 하 고 프로시저 및 functions 출력 매개 변수 뿐만 아니라 함수의 반환 값을 비교 하기 위한 설정을 구성 하는 개체를 선택 합니다.  
  
## <a name="selection-of-objects-to-test"></a>테스트할 개체 선택  
창의 왼쪽에 있는 Sybase 개체 트리에서 테스트 과정에서 호출 하려는 개체를 선택 합니다. 테스트 가능한 개체의 전체 목록을 보려면 합니다 [마이그레이션된 데이터베이스 개체 테스트 &#40;SybaseToSQL&#41; ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md) 항목입니다.  
  
레이블이 지정 된 링크가 표시는 SSMA 테스터가 테스트를 위해 선택한 개체 중 하나가 지원 하지 않는 경우 **선택한 일부 개체에 오류가 포함 되어** 개체 트리 아래에 있는 합니다. 이러한 개체를 테스트할 수 없는 이유에 이유를 표시 하 고 잘못 된 개체의 선택을 취소 하려면이 링크를 클릭 합니다.  
  
오른쪽에 있는 여러 페이지를 볼 수 있습니다 합니다 **SQL** 페이지는 현재 개체의 정의 보여 줍니다. 에 **이전 SQL** 하 고 **게시물 SQL** 페이지 테스트 개체 시작 호출 이전 및 이후 실행 되는 스크립트를 지정할 수 있습니다. 이 이러한 임시 테이블이 나 커서 개체에 추가 개체를 필요한 경우에 유용할 수 있습니다. 합니다 **매개 변수** 페이지 저장된 프로시저 또는 함수 개체가 있으면 매개 변수를 나열 합니다. 합니다 **속성** 페이지 개체의 추가 특징을 보여 줍니다. 에 대 한 설명을 참조 하세요 **매개 변수 Comparsions** 하 고 **호출 값** 아래 페이지입니다.  
  
## <a name="parameter-comparison-settings"></a>매개 변수 비교 설정  
출력 매개 변수에 대 한 비교 규칙을 설정 및 반환 값에는 **매개 변수 비교** 페이지입니다. 다음 설정을 할 수 있습니다.  
  
### <a name="use-during-comparisons"></a>비교 하는 동안 사용 하 여  
테스트 결과 비교에서 선택한 매개 변수를 사용 하 여 사용 하도록 설정 합니다.  
  
-   선택 하면 **True**, SSMA에 해당 하는 값을 사용 하 여 Sybase에서 프로시저를 실행 한 후이 매개 변수의 출력 값을 비교 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   선택 하면**False**, 매개 변수 확인 결과에서 제외 됩니다.  
  
### <a name="use-custom-scale"></a>사용자 지정 크기 조정 사용  
대략적인 및 고정 길이 숫자 데이터 형식의 매개 변수를 비교에 대 한 사용자 지정 확장을 설정할 수 있습니다.  
  
-   선택 하면 **True**, 숫자 값에 따라 반올림 됩니다 합니다 **비교 확장** 비교 하기 전에 값입니다.  
  
-   선택 하면**False**, 숫자 비교를 정확 하 게 됩니다.  
  
### <a name="comparing-scale"></a>배율 비교  
경우에만 사용할 수는 **사용 하 여 사용자 지정 크기 조정** 옵션을 설정 **True**합니다. 숫자 비교에 대 한 전체 자릿수입니다.  
  
### <a name="date-time-comparing"></a>날짜 시간 비교  
정의 방법: 날짜/시간 값을 비교 합니다.  
  
-   선택 하는 경우 **전체 날짜 비교**, 두 플랫폼 모두에서 값의 전체 비교 수행 됩니다.  
  
-   선택 하는 경우 **날짜만 비교**, 시간 부분 무시 됩니다.  
  
-   선택 하는 경우 **시간만 비교**, 날짜 파트는 무시 됩니다.  
  
-   선택 하는 경우 **무시 밀리초**, 초까지 결과 비교 합니다.  
  
-   선택 하는 경우 **무시 날짜 및 시간 (밀리초)**, 결과 초의 소수 부분 시간 부분으로만 비교 및 무시 됩니다.  
  
### <a name="ignore-strings-case"></a>문자열의 대/소문자 무시  
비교의 대/소문자 구분을 제어합니다.  
  
-   선택 하면 **True**, 비교는 대/소문자 구분 됩니다.  
  
-   선택 하면 **False**, 비교는 대/소문자 구분 됩니다.  
  
### <a name="ignore-trailing-spaces"></a>후행 공백 무시  
어떻게 후행 공백을 제어 비교 하는 동안 처리 됩니다.  
  
-   선택 하면 **True**, 비교 문자열 됩니다 오른쪽 잘립니다 비교 하기 전에 합니다.  
  
-   선택 하면 **False**, 비교 문자열에 후행 공백이 유지 됩니다.  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>프로시저 및 함수 (호출 값)에 대 한 입력된 값을 지정 합니다.  
입력된 매개 변수 값을 지정할 수 있습니다 합니다 **호출 값** 페이지입니다. 합니다 **호출 추가** 단추 빈 매개 변수 값을 사용 하 여 새 호출을 추가 합니다. 합니다 **호출 제거** 단추는 현재 호출을 제거 합니다.  
  
## <a name="next-step"></a>다음 단계  
[영향을 받는 개체 선택 및 구성 &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
  
## <a name="see-also"></a>관련 항목  
[마이그레이션된 데이터베이스 개체 테스트 &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  

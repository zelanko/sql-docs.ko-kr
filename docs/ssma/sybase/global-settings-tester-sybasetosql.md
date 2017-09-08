---
title: "전역 설정 (테스터) (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 6f0b9cea-5a24-4e42-8bbf-c4516b00da23
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 21178ca7326678504244658192d7395bab79a9ac
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="global-settings-tester-sybasetosql"></a>전역 설정 (테스터) (SybaseToSQL)
테스터 페이지를 사용 하 여 **전역 설정** SSMA 테스터에 대 한 설정을 지정 하려면 대화 상자.  
  
테스터 설정에 액세스 하려면는 **도구** 메뉴 선택 **전역 설정**, 클릭 하 고 **테스터** 왼쪽 창의 맨 아래에 있습니다.  
  
## <a name="options"></a>옵션  
**테스트 가능한 개체 분석**  
이 설정은 테스트 가능한 개체의 분석을 수행할 것인지를 지정 합니다. 선택 **예** SSMA 테스터를 분석 하 고 자동으로 종속 개체를 확인 하려는 경우. 기본 옵션 집합이 **예**합니다.  
  
다음 옵션은이 설정에 대해 사용할 수 있습니다.  
  
1.  예  
  
2.  아니요  
  
**보조 테이블 절약 모드**  
이 설정은 테스트 사례 실행 하는 동안 만든 내부 보조 테이블을 저장 하는 방법을 지정 합니다. 이 특정 설정에 대해 다음 옵션을 설정할 수 있습니다.  
  
1.  항상 삭제  
  
2.  항상 저장  
  
3.  테이블 비교에 실패 한 경우 저장  
  
4.  테이블 비교에 실패 한 경우 사용자에 게 확인  
  
기본 옵션 집합이: **항상 삭제**합니다.  
  
**데이터 롤백을 수행합니다**  
이 설정은 각 테스트 사례를 실행 한 후에 롤백 작업을 수행할 것인지 여부를 지정 합니다. 기본 옵션 집합이 **아니요**합니다.  
  
다음 옵션은이 설정에 대해 사용할 수 있습니다.  
  
1.  예  
  
2.  아니요  
  
**첫 번째 실패 후 테스트 실행을 중지**  
이 설정은 실행 하는 동안 오류가 발생 한 경우를 현재 실행 중인 테스트 사례를 중지할지 여부를 지정 합니다. 기본 옵션 집합이 **예**합니다.  
  
다음 옵션은이 설정에 대해 사용할 수 있습니다.  
  
1.  예  
  
2.  아니요  
  
## <a name="see-also"></a>참고 항목  
[테스트 사례 준비 &#40; 마치는 중 SybaseToSQL &#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)  
  


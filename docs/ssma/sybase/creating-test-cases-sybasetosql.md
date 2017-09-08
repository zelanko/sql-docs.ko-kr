---
title: "테스트 사례 만들기 (SybaseToSQL) | Microsoft Docs"
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
helpviewer_keywords:
- Tester component,Test Case Wizard
ms.assetid: b52dfd93-95af-4299-bc8f-83f2a7a6a518
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 48a8788780c7bf277bbbc1bc1703ad559a22f8e7
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="creating-test-cases-sybasetosql"></a>테스트 사례 (SybaseToSQL) 만들기
테스트 사례 마법사를 사용 하 여 테스트를 만들려고 합니다. 이 마법사를 사용 하면 테스트 매개 변수를 지정 하 고 테스트 하 고 확인할 개체를 선택 하 여 테스트 사례를 만들 수 있습니다.  
  
## <a name="starting-the-test-case-wizard"></a>테스트 사례 마법사 시작  
테스트 사례 마법사를 시작 하려면 **새 테스트 사례 중...** **테스터** 메뉴.  
  
시작 되 면 마법사 데이터베이스 ssmatester2005db 또는 Sybase 원본 서버에서 (프로젝트 유형에 따라) ssmatester2008db 찾습니다. 보조 개체를 저장 하는 데 사용 되는 테스터 확장 스키마는 테스트 사례 마법사 ssmatester2005db 또는 ssmatester2008db를 찾을 수 없는 경우 테스터 확장 데이터베이스를 만들려고 제안 된 대화 상자 창이 표시 됩니다. (이 경우 일반적으로 발생 함 SSMA 테스터의 첫 번째 실행 중입니다.)  
  
대화 상자 창 발생 하는 경우 클릭 **예** Sybase 테스터 데이터베이스 원본 서버를 만들 수 있습니다. 다음 새 대화 상자 창은 테스터 데이터베이스를 새 위치를 하나 이상의 장치를 추가 해야 표시 됩니다. 클릭 **추가** 장치를 추가 합니다. 에 **테스터 데이터베이스에 대 한 공간 할당** 대화 장치를 선택 하 고 테스터 데이터베이스에서 사용 되는 크기를 지정 합니다. 또한 데이터베이스 로그에 대 한 별도 장치를 설정할 수 있습니다. 참고 Sybase 데이터베이스를 만들 권한이 있어야 합니다.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>마법사를 사용 하 여 테스트 사례 만들기 개요  
테스트 사례를 만드는 과정 5 단계로 구성 됩니다.  
  
1.  [테스트 사례 &#40; 초기화 SybaseToSQL &#41; ](../../ssma/sybase/initializing-test-cases-sybasetosql.md).  
  
2.  [선택 하 고 테스트 &#40; 개체를 구성 합니다. SybaseToSQL &#41; ](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md).  
  
3.  [선택 하 고 영향을 받는 개체 &#40; 구성 합니다. SybaseToSQL &#41; ](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md).  
  
4.  [호출 순서 &#40; 사용자 지정 SybaseToSQL &#41; ](../../ssma/sybase/customizing-calls-order-sybasetosql.md).  
  
5.  [테스트 사례 준비 &#40; 마치는 중 SybaseToSQL &#41; ](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md).  
  
## <a name="see-also"></a>관련 항목:  
[데이터베이스 개체 &#40; 마이그레이션 테스트 SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  


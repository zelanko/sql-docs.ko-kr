---
title: "테스트 사례 만들기 (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Test Case Wizard
ms.assetid: 22f38901-ec35-4707-a911-784e6ad8dafb
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: cd27397f5f925989412ad7a7f510778e18fb9207
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="creating-test-cases-oracletosql"></a>테스트 사례 (OracleToSQL) 만들기
테스트 사례 마법사를 사용 하 여 테스트를 만들려고 합니다. 이 마법사를 사용 하면 테스트 매개 변수를 지정 하 고 테스트 하 고 확인할 개체를 선택 하 여 테스트 사례를 만들 수 있습니다.  
  
## <a name="starting-the-test-case-wizard"></a>테스트 사례 마법사 시작  
테스트 사례 마법사를 시작 하려면 **새 테스트 사례 중...** **테스터** 메뉴.  
  
시작 되 면 마법사는 원본 Oracle 서버의 SSMATESTER_ORACLE 스키마에 대 한 보입니다. 보조 개체를 저장 하는 데 사용 되는 테스터 확장 스키마는 테스트 사례 마법사 SSMATESTER_ORACLE를 찾을 수 없는 경우에 스키마를 만들려면 다음을 제안 하는 대화 상자 창이 표시 됩니다. (이 경우 일반적으로 발생 함 SSMA 테스터의 첫 번째 실행 중입니다.)  
  
대화 상자 창 발생 하는 경우 클릭 **예** 원본 서버에서 SSMATESTER_ORACLE 스키마를 만들 수 있습니다. Oracle 권한 만든 새 사용자를 만드는 것을 해야가이 사용자의 스키마에는 개체입니다.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>마법사를 사용 하 여 테스트 사례 만들기 개요  
테스트 사례를 만드는 과정 5 단계로 구성 됩니다.  
  
1.  [초기화 하는 동안 테스트 사례 &#40; OracleToSQL &#41;](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [선택 하 고 구성 개체를 테스트 &#40; OracleToSQL &#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [선택 하 고 구성 영향을 받는 개체 &#40; OracleToSQL &#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [사용자 지정 호출 순서 &#40; OracleToSQL &#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [완료 테스트 사례 준비 &#40; OracleToSQL &#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>관련 항목:  
[데이터베이스 개체 &#40; OracleToSQL &#41; 마이그레이션 테스트](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

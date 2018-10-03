---
title: 테스트 사례 만들기 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Test Case Wizard
ms.assetid: 22f38901-ec35-4707-a911-784e6ad8dafb
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 07b52a71d3f12455bacdd2e9789aadb5ed5967db
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47604681"
---
# <a name="creating-test-cases-oracletosql"></a>테스트 사례 만들기(OracleToSQL)
테스트를 만드는 테스트 사례 마법사를 사용 합니다. 이 마법사를 사용 하면 테스트 매개 변수를 지정 하 고 테스트 하 고 개체를 확인을 선택 하 여 테스트 사례를 만들 수 있습니다.  
  
## <a name="starting-the-test-case-wizard"></a>테스트 사례 마법사 시작  
테스트 사례 마법사를 시작 하려면 **새 테스트 사례는 중...** **테스터** 메뉴.  
  
시작 되 면 마법사는 원본 Oracle 서버의 SSMATESTER_ORACLE 스키마를 찾습니다. 보조 개체를 저장 하는 데 사용 되는 테스터 확장 스키마 이며 테스트 사례 마법사 SSMATESTER_ORACLE를 찾을 수 없는 경우에 스키마를 만들려면 다음을 제안 하는 대화 상자 창이 표시 됩니다. (이 경우 일반적으로 발생 SSMA 테스터의 첫 번째 실행 중입니다.)  
  
대화 상자 창에 표시 되 면 클릭 **예** 원본 서버의 SSMATESTER_ORACLE 스키마를 만들 수 있습니다. 새 사용자를 만들고 Oracle 권한을 해야가이 사용자의 스키마에는 개체입니다.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>마법사를 사용 하 여 테스트 사례 만들기 개요  
테스트 사례를 만드는 프로세스는 5 단계로 구성 됩니다.  
  
1.  [테스트 사례 초기화 &#40;OracleToSQL&#41;](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [테스트할 개체 선택 및 구성 &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [영향을 받는 개체 선택 및 구성 &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [호출 순서 사용자 지정 &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [테스트 사례 준비 완료 &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>관련 항목  
[마이그레이션된 데이터베이스 개체 테스트 &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

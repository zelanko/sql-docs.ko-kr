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
manager: shamikg
ms.openlocfilehash: 697f7049a60aa7ae2b8c89d1fb6c5ce8e3d29312
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68266131"
---
# <a name="creating-test-cases-oracletosql"></a>테스트 사례 만들기(OracleToSQL)
테스트 사례 마법사를 사용 하 여 테스트를 만듭니다. 이 마법사를 사용 하면 테스트 되 고 확인 된 개체를 선택 하 고 테스트 매개 변수를 지정 하 여 테스트 사례를 만들 수 있습니다.  
  
## <a name="starting-the-test-case-wizard"></a>테스트 사례 마법사 시작  
테스트 사례 마법사를 시작 하려면 **테스터** 메뉴에서 **새 테스트 사례 ...** 를 클릭 합니다.  
  
시작 하면 마법사가 원본 Oracle 서버에서 스키마 SSMATESTER_ORACLE를 찾습니다. 보조 개체를 저장 하는 데 사용 되는 테스터 확장 스키마입니다. 테스트 사례 마법사가 SSMATESTER_ORACLE를 찾을 수 없는 경우 스키마를 만들도록 제안 하는 대화 상자 창이 표시 됩니다. 이 상황은 일반적으로 SSMA 테스터를 처음 실행 하는 동안 발생 합니다.  
  
대화 상자가 나타나면 **예** 를 클릭 하 여 원본 서버에 SSMATESTER_ORACLE 스키마를 만듭니다. 새 사용자를 만들고이 사용자의 스키마에서 개체를 만들려면 Oracle 권한이 있어야 합니다.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>마법사를 사용 하 여 테스트 사례 만들기 개요  
테스트 사례를 만드는 프로세스는 다음 5 단계로 구성 됩니다.  
  
1.  [OracleToSQL&#41;&#40;테스트 사례 초기화](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [OracleToSQL&#41;&#40;테스트할 개체 선택 및 구성](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [영향을 받는 개체 선택 및 구성 &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [호출 순서 사용자 지정 &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [OracleToSQL&#41;&#40;테스트 사례 준비 완료](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>참고 항목  
[OracleToSQL&#41;&#40;마이그레이션된 데이터베이스 개체 테스트](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

---
title: 테스트 사례 실행 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Execution Steps
ms.assetid: 195ffdef-cfde-4bf4-a3ae-e7402bb07972
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: d828142d83f21cf38663241d593fe197b9715592
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87930504"
---
# <a name="running-test-cases-sybasetosql"></a>테스트 사례 실행(SybaseToSQL)
SSMA 테스터는 테스트 사례를 실행할 때 테스트를 위해 선택한 개체를 실행 하 고 확인 결과에 대 한 보고서를 만듭니다. 두 플랫폼에서 결과가 동일 하면 테스트에 성공 했습니다. Sybase와 간의 개체 대응은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 현재 SSMA 프로젝트의 스키마 매핑 설정에 따라 결정 됩니다.  
  
성공적인 테스트를 위해 필요한 요구 사항은 모든 Sybase 개체가 변환 되 고 대상 데이터베이스에 로드 되는 것입니다. 또한 두 플랫폼의 테이블 내용이 동기화 되도록 테이블 데이터를 마이그레이션해야 합니다.  
  
## <a name="run-test-case"></a>테스트 사례 실행  
준비 된 테스트 사례를 실행 하려면 다음을 수행 합니다.  
  
1.  **실행** 단추를 클릭합니다.  
  
2.  **Sybase에 연결** 대화 상자에서 연결 정보를 입력 한 다음 **연결**을 클릭 합니다.  
  
테스트가 완료 되 면 테스트 사례 보고서가 만들어집니다. **보고서** 단추를 클릭 하 여 [테스트 사례 보고서 보기 &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)를 확인 합니다. 테스트의 결과 (테스트 사례 보고서)는 나중에 사용할 수 있도록 [테스트 리포지토리 &#40;SybaseToSQL&#41;를 사용 하](../../ssma/sybase/using-test-repositories-sybasetosql.md) 여 자동으로 저장 됩니다.  
  
## <a name="test-case-execution-steps"></a>테스트 사례 실행 단계  
  
### <a name="prerequisites"></a>필수 구성 요소  
SSMA 테스터는 테스트를 시작 하기 전에 테스트 실행에 대해 모든 필수 구성 요소가 충족 되는지 확인 합니다. 일부 조건이 충족 되지 않으면 오류 메시지가 나타납니다.  
  
### <a name="initialization"></a>초기화  
이 단계에서 SSMA 테스터는 Sybase 및에서 보조 개체 (테이블, 트리거 및 뷰)를 만듭니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 테이블 비교 모드가 변경 된 경우에 **만**확인 하도록 선택한 영향을 받는 테이블에 적용 된 변경 내용을 추적할 수 있습니다.  
  
확인 된 테이블의 이름이 USER_TABLE 이라고 가정 합니다. 이러한 테이블의 경우 다음과 같은 보조 개체가 Sybase로 생성 됩니다.  
  
SSMATESTER2005db 또는 SSMATESTER2008db 데이터베이스와 ssmatesterdb_syb 데이터베이스의에서 Sybase에 생성 되는 개체는 다음과 같습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Name|Type|설명|  
|--------|--------|---------------|  
|USER_TABLE $ Trg|트리거|확인 된 테이블의 변경 내용에 대 한 감사를 트리거합니다.|  
|USER_TABLE $ Aud|테이블|삭제 된 행과 덮어쓴 행을 저장 하는 테이블입니다.|  
|USER_TABLE $|테이블|새 행과 변경 된 행이 저장 되는 테이블입니다.|  
|USER_TABLE|보기|테이블 수정의 단순화 된 표현입니다.|  
|USER_TABLE $ new|보기|삽입 및 덮어쓴 행의 단순화 된 표현입니다.|  
|USER_TABLE $ new_id|보기|삽입 된 행과 변경 된 행의 id입니다.|  
|USER_TABLE $ old|보기|삭제 및 덮어쓴 행의 단순화 된 표현입니다.|  
  
Sybase 및에서 확인 된 테이블의 데이터베이스에 생성 되는 개체는 다음과 같습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Name|Type|설명|  
|--------|--------|---------------|  
|USER_TABLE $ Trg|트리거|확인 된 테이블의 변경 내용에 대 한 감사를 트리거합니다.|  
  
### <a name="test-object-calls"></a>개체 호출 테스트  
이 단계에서 SSMA 테스터는 테스트를 위해 선택한 각 개체를 호출 하 고, 결과를 비교 하 고, 보고서를 표시 합니다.  
  
### <a name="finalization"></a>종료  
종료 하는 동안에는 **초기화** 단계에서 생성 된 보조 개체를 정리 합니다.  
  
## <a name="next-step"></a>다음 단계  
[테스트 사례 보고서 보기 &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)  
  
## <a name="see-also"></a>참고 항목  
[&#40;SybaseToSQL&#41;를 테스트할 개체 선택 및 구성](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)  
[영향을 받는 개체 선택 및 구성 &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
[마이그레이션된 데이터베이스 개체 테스트 &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  

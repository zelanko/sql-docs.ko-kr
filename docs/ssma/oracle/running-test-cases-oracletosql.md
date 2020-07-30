---
title: 테스트 사례 실행 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 7905c76803bf637e581af934f473b070d44a6b09
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394866"
---
# <a name="running-test-cases-oracletosql"></a>테스트 사례 실행(OracleToSQL)
SSMA 테스터는 테스트 사례를 실행할 때 테스트를 위해 선택한 개체를 실행 하 고 확인 결과에 대 한 보고서를 만듭니다. 두 플랫폼에서 결과가 동일 하면 테스트에 성공 했습니다. Oracle과 간의 개체 대응은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 현재 SSMA 프로젝트의 스키마 매핑 설정에 따라 결정 됩니다.  
  
성공적인 테스트를 위해 필요한 요구 사항은 모든 Oracle 개체가 변환 되 고 대상 데이터베이스에 로드 되는 것입니다. 또한 두 플랫폼의 테이블 내용이 동기화 되도록 테이블 데이터를 마이그레이션해야 합니다.  
  
## <a name="run-test-case"></a>테스트 사례 실행  
준비 된 테스트 사례를 실행 하려면 다음을 수행 합니다.  
  
1.  **실행** 단추를 클릭합니다.  
  
2.  **Oracle에 연결** 대화 상자에서 연결 정보를 입력 한 다음 **연결**을 클릭 합니다.  
  
테스트가 완료 되 면 테스트 사례 보고서가 만들어집니다. **보고서** 단추를 클릭 하 여 [테스트 사례 보고서](viewing-test-case-reports-oracletosql.md)를 봅니다. 테스트 결과 (테스트 사례 보고서)는 나중에 사용 하기 위해 [테스트 결과 리포지토리에](using-test-repositories-oracletosql.md) 자동으로 저장 됩니다.  
  
## <a name="test-case-execution-steps"></a>테스트 사례 실행 단계  
  
### <a name="prerequisites"></a>필수 구성 요소  
SSMA 테스터는 테스트를 시작 하기 전에 테스트 실행에 대해 모든 필수 구성 요소가 충족 되는지 확인 합니다. 일부 조건이 충족 되지 않으면 오류 메시지가 나타납니다.  
  
### <a name="initialization"></a>초기화  
이 단계에서 SSMA 테스터는 Oracle 서버의 SSMATESTER_ORACLE 스키마에 보조 개체 (테이블, 트리거 및 뷰)를 만듭니다. 확인을 위해 선택한 영향을 받는 개체에서 적용 된 변경 내용을 추적할 수 있습니다.  
  
확인 된 테이블의 이름이 USER_TABLE 이라고 가정 합니다. 이러한 테이블의 경우 Oracle에서 다음 보조 개체가 생성 됩니다.  
  
|Name|Type|설명|  
|-|-|-|  
|USER_TABLE $ Trg|트리거|확인 된 테이블의 변경 내용에 대 한 감사를 트리거합니다.|  
|USER_TABLE $ AUD|테이블|삭제 된 행과 덮어쓴 행을 저장 하는 테이블입니다.|  
|USER_TABLE $|테이블|새 행과 변경 된 행이 저장 되는 테이블입니다.|  
|USER_TABLE|뷰|테이블 수정의 단순화 된 표현입니다.|  
|USER_TABLE $ NEW|뷰|삽입 및 덮어쓴 행의 단순화 된 표현입니다.|  
|USER_TABLE $ NEW_ID|뷰|삽입 된 행과 변경 된 행의 id입니다.|  
|USER_TABLE $ OLD|뷰|삭제 및 덮어쓴 행의 단순화 된 표현입니다.|  
  
다음 개체는에서 확인 된 테이블의 스키마에 생성 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Name|Type|설명|  
|-|-|-|  
|USER_TABLE $ Trg|트리거|확인 된 테이블의 변경 내용에 대 한 감사를 트리거합니다.|  
  
Ssmatesterdb 데이터베이스의에서 다음 개체가 만들어집니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Name|Type|설명|  
|-|-|-|  
|USER_TABLE $ Aud|테이블|삭제 된 행과 덮어쓴 행을 저장 하는 테이블입니다.|  
|USER_TABLE $|테이블|새 행과 변경 된 행이 저장 되는 테이블입니다.|  
|USER_TABLE|뷰|테이블 수정의 단순화 된 표현입니다.|  
|USER_TABLE $ new|뷰|삽입 및 덮어쓴 행의 단순화 된 표현입니다.|  
|USER_TABLE $ new_id|뷰|삽입 된 행과 변경 된 행의 id입니다.|  
|USER_TABLE $ old|뷰|삭제 및 덮어쓴 행의 단순화 된 표현입니다.|  
  
### <a name="test-object-calls"></a>개체 호출 테스트  
이 단계에서 SSMA 테스터는 테스트를 위해 선택한 각 개체를 호출 하 고, 결과를 비교 하 고, 보고서를 표시 합니다.  
  
### <a name="finalization"></a>종료  
종료 하는 동안에는 **초기화** 단계에서 생성 된 보조 개체를 정리 합니다.  
  
## <a name="next-step"></a>다음 단계  
[OracleToSQL&#41;&#40;테스트 사례 보고서 보기](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)  
  
## <a name="see-also"></a>참고 항목  
[OracleToSQL&#41;&#40;테스트할 개체 선택 및 구성](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
[영향을 받는 개체 선택 및 구성 &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
[OracleToSQL&#41;&#40;마이그레이션된 데이터베이스 개체 테스트](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

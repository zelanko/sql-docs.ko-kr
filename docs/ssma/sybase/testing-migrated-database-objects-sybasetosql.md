---
title: 데이터베이스 개체 (SybaseToSQL) 마이그레이션 테스트 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 4937f6b4-86bd-4070-88df-3d216306c33a
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 02cc2deb2721759f938ba8e0244f46b4464b86fa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="testing-migrated-database-objects-sybasetosql"></a>데이터베이스 개체 (SybaseToSQL) 마이그레이션 테스트
Microsoft SQL Server Migration Assistant (SSMA 테스터) Sybase 테스터를 위한 자동으로 데이터베이스 개체를 변환 및 테스트 데이터 마이그레이션 SSMA 수행 합니다. 모든 SSMA 마이그레이션 단계가 완료 되 면 SSMA 테스터를 사용 하 여 변환 된 개체가 같은 방식으로 작동 하는지 되 고 모든 데이터가 제대로 전송 되었습니다.  
  
> [!NOTE]  
> 테스터 구성 요소는 Azure 연결의 경우 비활성화 됩니다.  
  
개체 유형 SSMA 테스터를 테스트할 수 있습니다.  
  
-   테이블  
  
-   저장 프로시저  
  
-   뷰.  
  
-   독립 실행형 문입니다.  
  
SSMA 테스터 Sybase와 SQL Server의 해당 항목에서 테스트를 위해 선택한 개체를 실행 합니다. 그 후 다음 기준에 따라 결과 비교 합니다.  
  
-   동일한 테이블 데이터에 변경 내용을 있습니까?  
  
-   프로시저 및 함수에 대 한 출력 매개 변수 값 동일는 무엇입니까?  
  
-   함수는 동일한 결과 반환 수행?  
  
-   동일한 결과 집합은?  
  
> [!NOTE]  
> 주의! 프로덕션 시스템에서 SSMA 테스터를 사용 하지 마십시오. 테스터 실행 하는 동안 소스 스키마와 데이터 수정 됩니다. 한편, 원래 상태로의 전체 restoring 일부 유형의 테스트 된 코드에 대 한 가능한 수 있습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
SSMA 테스터를 사용 하려는 경우와 SSMA Sybase 확장 팩을 설치는 **테스터 데이터베이스 설치** 옵션을 설정 합니다.  
  
또한 다음을 확인 합니다.  
  
-   Sybase OLE DB 공급자가 컴퓨터에 설치 되어 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 실행 합니다.  
  
-   에 대해 공용 언어 런타임 (CLR) 통합이 활성화는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 엔진입니다.  
  
Note SSMA 테스터의 현재 버전 동일한 원본 또는 대상 서버에 여러 사용자가 병렬 실행을 지원 하지 않습니다.  
  
## <a name="getting-started"></a>시작  
[테스트 사례 만들기 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-test-cases-sybasetosql.md)  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server에 SSMA 구성 요소 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[프로젝트 설정 &#40;변환&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  

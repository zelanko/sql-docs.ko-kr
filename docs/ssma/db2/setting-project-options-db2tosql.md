---
title: 프로젝트 옵션 설정 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f325a606-97ac-48bc-b344-b55f5e086a48
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: d384433e5a2653291fac4d990bb3660b31c13855
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68060027"
---
# <a name="setting-project-options-db2tosql"></a>프로젝트 옵션 설정 (DB2ToSQL)
각 SSMA 프로젝트에 대해 프로젝트 수준 옵션을 설정할 수 있습니다. 이러한 옵션은 개체 변환, 개체 로드, 사용자 인터페이스 및 데이터 마이그레이션 설정을 지정 합니다. 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 변환 하거나 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를로 마이그레이션하기 전에 구성 옵션이 프로젝트에 적합 한지 확인 합니다.  
  
SSMA를 사용 하면 모든 프로젝트에 대 한 기본 옵션을 구성할 수 있습니다. 이러한 옵션은 사용자가 만드는 모든 새 프로젝트에 적용 됩니다. 그런 다음 각 프로젝트에 대 한 옵션을 사용자 지정할 수 있습니다.  
  
## <a name="configuration-options-and-modes"></a>구성 옵션 및 모드  
SSMA에는 5 개의 프로젝트 설정 집합이 있습니다.  
  
-   프로젝트 정보  
  
-   일반 (변환, 마이그레이션, 개체 로드)  
  
-   동기화  
  
-   GUI  
  
-   형식 매핑  
  
또한 이러한 설정을 구성 하는 네 가지 모드가 있습니다.  
  
-   기본값  
  
-   Optimistic  
  
-   전체  
  
-   사용자 지정  
  
대부분의 사용자에 게 기본 모드를 권장 합니다. 낙관적 모드에서는 더 많은 최신 DB2 구문을 유지 하 고 더 쉽게 읽을 수 있습니다. 그러나 현재 구문을 유지 하는 것은 정확 하지 않을 수 있습니다. DB2 구문을 동등한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구문으로 변환 해야 하는 경우 전체 모드에서 가장 완전 한 변환을 수행 하지만 결과 코드를 읽기가 더 어려울 수 있습니다. 사용자 지정 모드에서 옵션을 설정 합니다.  
  
설정 및 설정 설정에 대 한 자세한 내용은 다음 항목을 참조 하십시오.  
  
-   [프로젝트 설정 &#40;변환&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)  
  
-   [마이그레이션&#41; &#40;DB2ToSQL 프로젝트 설정 &#40;&#41;](../../ssma/db2/project-settings-migration-db2tosql.md)  
  
-   [프로젝트 설정&#40;동기화&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)  
  
-   [프로젝트 설정 &#40;GUI&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-gui-db2tosql.md)  
  
-   [프로젝트 설정 &#40;형식 매핑&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)  
  
## <a name="setting-project-options"></a>프로젝트 옵션 설정  
SSMA에서 모든 프로젝트에 대 한 기본 설정을 구성할 수 있습니다. 이러한 설정은 SSMA 구성 파일에 저장 되 고 사용자가 만드는 모든 새 프로젝트에 적용 됩니다.  
  
**기본 프로젝트 옵션을 설정 하려면**  
  
1.  **도구** 메뉴에서 **기본 프로젝트 설정**을 클릭 합니다.  
  
2.  **기본 프로젝트 설정** 대화 상자에서 다음 절차 중 하나를 사용 합니다.  
  
    -   마이그레이션 **대상 버전** 드롭다운에서 설정을 보거나 변경 해야 하는 마이그레이션 프로젝트 유형을 선택 합니다. 왼쪽 창의 맨 아래에서 **일반** 을 클릭 한 다음 변환 또는 마이그레이션을 선택 합니다.  
  
    -   미리 정의 된 모드를 선택 하려면 **모드** 드롭다운 상자에서 **기본값**, **낙관적**또는 **전체**를 선택 합니다.  
  
    -   사용자 지정 설정을 지정 하려면 새 설정 또는 값을 선택 하거나 입력 합니다.  
  
3.  
  **확인**을 클릭하여 설정을 저장합니다.  
  
현재 프로젝트에 대 한 설정을 사용자 지정할 수도 있습니다. 이러한 설정은 현재 프로젝트 파일에 저장 됩니다.  
  
**현재 프로젝트에 대 한 설정을 사용자 지정 하려면**  
  
1.  **도구** 메뉴에서 **프로젝트 설정**을 클릭 합니다.  
  
2.  **프로젝트 설정** 대화 상자에서 다음 절차 중 하나를 사용 합니다.  
  
    -   미리 정의 된 모드를 선택 하려면 **모드** 드롭다운 상자에서 **기본값**, **낙관적**또는 **전체**를 선택 합니다.  
  
    -   사용자 지정 모드를 지정 하려면 **모드** 상자에서 **사용자 지정**을 선택 하 고 적절 한 프로젝트 설정을 선택 합니다.  
  
3.  
  **확인**을 클릭하여 설정을 저장합니다.  
  
## <a name="next-steps"></a>다음 단계  
마이그레이션의 다음 단계는 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   원본 및 대상 데이터 형식의 매핑을 사용자 지정 하려면 [DB2 매핑 및 SQL Server 데이터 형식 &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)를 참조 하세요.  
  
-   그렇지 않으면 DB2 데이터베이스 개체 정의를 개체 정의로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변환할 수 있습니다. 자세한 내용은 [DB2 스키마 변환 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
[DB2 및 SQL Server 데이터 형식 매핑 &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)  
  

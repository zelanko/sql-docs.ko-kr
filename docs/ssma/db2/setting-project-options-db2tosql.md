---
title: "프로젝트 옵션 (DB2ToSQL) 설정 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: f325a606-97ac-48bc-b344-b55f5e086a48
caps.latest.revision: 5
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1f5b71db23d56150fbc6a2f7990ba9960d83d2d1
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="setting-project-options-db2tosql"></a>프로젝트 옵션 설정 (DB2ToSQL)
각 SSMA 프로젝트에 대해 프로젝트 수준 옵션을 설정할 수 있습니다. 이러한 옵션에는 변환 개체, 개체 로드, 사용자 인터페이스 및 데이터 마이그레이션 설정을 지정합니다. 개체를 변환 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터를 마이그레이션하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 구성 옵션은 프로젝트에 대 한 적절 한지 확인 하십시오.  
  
SSMA를 사용 하면 모든 프로젝트에 대 한 기본 옵션을 구성할 수 있습니다. 이러한 옵션은 만들어지는 모든 새 프로젝트에 적용 됩니다. 그런 다음 각 프로젝트에 대 한 옵션을 사용자 지정할 수 있습니다.  
  
## <a name="configuration-options-and-modes"></a>구성 옵션 및 모드  
SSMA는 프로젝트 설정의 5 개 세트:  
  
-   프로젝트 정보  
  
-   일반 (변환, 로드 하는 개체 마이그레이션)  
  
-   Synchronization  
  
-   GUI  
  
-   형식 매핑  
  
구성이 설정에 대 한 네 가지 모드에 있습니다.  
  
-   기본값  
  
-   Optimistic  
  
-   전체  
  
-   사용자 지정  
  
대부분의 사용자에 대 한 기본 모드를 사용 하는 것이 좋습니다. 최적 모드 중 현재 DB2 구문을 유지 되며 더 쉽게 읽을 수 있습니다. 그러나 현재 구문을 유지 하지 정확할 수도 있습니다. DB2 구문으로 변환 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구문, 전체 모드 가장 완벽 변환을 수행 하지만 결과 코드를 읽기가 어려울 수 있습니다. 사용자 지정 모드에서 옵션을 설정 합니다.  
  
설정과 각 모드에서 설정이 적용 되는 방식을 대 한 자세한 내용은 다음 항목을 참조 합니다.  
  
-   [프로젝트 설정 &#40; 변환 &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)  
  
-   [프로젝트 설정 &#40; 마이그레이션 &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-migration-db2tosql.md)  
  
-   [프로젝트 설정 &#40; 동기화 &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)  
  
-   [프로젝트 설정 &#40; GUI &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-gui-db2tosql.md)  
  
-   [프로젝트 설정 &#40; 형식 매핑 &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)  
  
## <a name="setting-project-options"></a>프로젝트 옵션 설정  
SSMA를 모든 프로젝트에 대 한 기본 설정을 구성할 수 있습니다. 이러한 설정은 SSMA 구성 파일에 저장 되며 만드는 모든 새 프로젝트에 적용 됩니다.  
  
**기본 프로젝트 옵션을 설정 하려면**  
  
1.  에 **도구** 메뉴를 클릭 하 여 **기본 프로젝트 설정**합니다.  
  
2.  에 **기본 프로젝트 설정** 대화 상자에서 다음 절차 중 하나를 사용 합니다.  
  
    -   설정을 보거나에서 변경 하는 데 필요한는 마이그레이션 프로젝트 형식을 선택 **마이그레이션 대상 버전** 클릭 드롭다운 **일반** 왼쪽된 창 및 선택 변환 또는 마이그레이션을 맨 아래에 있습니다.  
  
    -   미리 정의 된 모드를 선택 하 고 **모드** 드롭다운 상자 **기본**, **Optimistic**, 또는 **전체**합니다.  
  
    -   사용자 지정 설정을 지정 하려면에서 선택 하거나 새 설정이 나 값을 입력 합니다.  
  
3.  클릭 **확인** 설정을 저장할 수 있습니다.  
  
현재 프로젝트에 대 한 설정을 사용자 지정할 수도 있습니다. 이러한 설정은 현재 프로젝트 파일에 저장 됩니다.  
  
**현재 프로젝트에 대 한 설정을 사용자 지정 하려면**  
  
1.  에 **도구** 메뉴를 클릭 하 여 **프로젝트 설정**합니다.  
  
2.  에 **프로젝트 설정** 대화 상자에서 다음 절차 중 하나를 사용 합니다.  
  
    -   미리 정의 된 모드를 선택 하 고 **모드** 드롭다운 상자 **기본**, **Optimistic**, 또는 **전체**합니다.  
  
    -   사용자 지정 모드를 지정 하는 **모드** 상자 선택 **사용자 지정**, 한 다음 적절 한 프로젝트 설정을 선택 합니다.  
  
3.  클릭 **확인** 설정을 저장할 수 있습니다.  
  
## <a name="next-steps"></a>다음 단계  
다음 단계는 마이그레이션에서 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   원본 및 대상 데이터 형식 매핑, 사용자 지정 하려면 참조 [매핑 DB2 및 SQL Server 데이터 형식 &#40; DB2ToSQL &#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)합니다.  
  
-   그렇지 않은 경우에 DB2 데이터베이스 개체 정의 변환할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 개체 정의 합니다. 자세한 내용은 참조 [DB2 스키마로 변환 &#40; DB2ToSQL &#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
[매핑 DB2 및 SQL Server 데이터 형식 &#40; DB2ToSQL &#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)  
  


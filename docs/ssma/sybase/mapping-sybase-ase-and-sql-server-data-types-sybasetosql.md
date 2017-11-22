---
title: "Sybase ASE 및 SQL Server 데이터 형식 (SybaseToSQL) 매핑 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping Sybase ASE Schemas to SQL Server Schemas
- Type Mapping Settings
ms.assetid: 784365d3-df4e-47ab-8ee0-d8392b52f510
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6952149829845872a78d5732671c1f9f9cd6a323
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="mapping-sybase-ase-and-sql-server-data-types-sybasetosql"></a>Sybase ASE 및 SQL Server 데이터 형식 (SybaseToSQL) 매핑
Sybase 적응형 Server Enterprise (ASE) 데이터베이스 형식에서 다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 데이터베이스 유형입니다. ASE 데이터베이스 개체를 변환 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 개체를 ASE의 데이터 형식을 매핑하는 방법을 지정 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다. 기본 데이터 형식 매핑을 사용할 수도 있고 다음 섹션에 나와 있는 것 처럼 매핑을 사용자 지정할 수 있습니다.  
  
## <a name="default-mappings"></a>기본 매핑  
SSMA에 기본 데이터 형식 매핑 집합이 있습니다. 기본 매핑 목록이 참조 [프로젝트 설정 &#40; 형식 매핑 &#41; &#40; SybaseToSQL &#41; ](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
## <a name="type-mapping-inheritance"></a>형식 상속 매핑  
프로젝트 수준, (예: 모든 저장된 프로시저), 범주 수준 개체 또는 개체 수준에서 형식 매핑을 사용자 지정할 수 있습니다. 설정은 낮은 수준에서 재정의 되지 않는 한 상위 수준에서 상속 됩니다. 예를 들어, 매핑하는 경우 **smallmoney** 를 **money** 프로젝트 수준에서 프로젝트의 모든 개체 범주 수준 개체 또는 개체 수준에서 매핑을 사용자 지정 하지 않으면이 매핑을 사용 합니다.  
  
볼 때의 **유형 매핑** SSMA 백그라운드 탭이 상속 되는 형식 매핑 표시 하도록 색이 지정 되어 있습니다. 형식 매핑을 배경은 노란색은 상속 된 형식 매핑 및 흰색으로 현재 수준에서 지정 된 모든 매핑이 모든.  
  
## <a name="customizing-data-type-mappings"></a>사용자 정의 데이터 형식 매핑  
다음 절차에는 프로젝트, 데이터베이스 또는 개체 수준에서의 데이터 형식을 매핑하는 방법을 보여 줍니다.  
  
**데이터 형식을 매핑할**  
  
1.  전체 프로젝트에 대 한 데이터 형식 매핑을 사용자 지정 하려면 열에서 **프로젝트 설정** 대화 상자:  
  
    1.  에 **도구** 메뉴 선택 **프로젝트 설정**합니다.  
  
    2.  왼쪽된 창에서 선택 **유형 매핑**합니다.  
  
        형식 매핑 차트 및 단추 오른쪽 창에 나타납니다.  
  
    또는 데이터 형식을 사용자 지정 하려면 데이터베이스, 테이블, 뷰 또는 저장된 프로시저 수준부터 매핑을 데이터베이스, 개체 범주 또는 개체 탐색기에서 선택 Sybase 메타 데이터:  
  
    1.  Sybase 메타 데이터 탐색기에서 폴더 또는 사용자 지정 하려면 개체를 선택 합니다.  
  
    2.  오른쪽 창에서 클릭 하 고 **유형 매핑** 탭 합니다.  
  
2.  새 매핑을 추가 하려면 다음을 수행 합니다.  
  
    1.  **추가**를 클릭합니다.  
  
    2.  아래 **소스 형식**를 매핑할 ASE 데이터 형식을 선택 합니다.  
  
    3.  형식 길이 지정에 대 한 매핑에 대 한 최소한의 데이터 길이 **에서** 고에서 매핑에 대 한 최대 데이터 길이 지정는 **를** 상자입니다.  
  
        이렇게 하면 동일한 데이터 형식의 크기가 작고 더 큰 값에 대 한 데이터 매핑을 사용자 지정할 수 있습니다.  
  
    4.  아래 **대상 유형**, 대상을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 데이터 형식입니다.  
  
        일부 형식은 대상 데이터 형식의 길이가 필요합니다. 필요한 경우 입력에 새 데이터 길이 **바꿉니다** 상자입니다.  
  
    5.  **확인**을 클릭합니다.  
  
3.  데이터 형식 매핑을 편집 하려면 다음을 수행 합니다.  
  
    1.  **편집**을 클릭합니다.  
  
    2.  아래 **소스 형식**를 매핑할 ASE 데이터 형식을 선택 합니다.  
  
    3.  형식 길이 지정에 대 한 매핑에 대 한 최소한의 데이터 길이 **에서** 고에서 매핑에 대 한 최대 데이터 길이 지정는 **를** 상자입니다.  
  
        이렇게 하면 동일한 데이터 형식의 크기가 작고 더 큰 값에 대 한 데이터 매핑을 사용자 지정할 수 있습니다.  
  
    4.  아래 **대상 유형**, 대상을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 데이터 형식입니다.  
  
        일부 형식은 대상 데이터 형식의 길이가 필요합니다. 필요한 경우 입력에 새 데이터 길이 **바꿉니다** 상자를 선택한 다음 클릭 **확인**합니다.  
  
4.  사용자 지정 데이터 형식 매핑을 제거 하려면 다음을 수행 합니다.  
  
    1.  제거 하려는 데이터 형식 매핑을 포함 하는 형식 매핑 목록에서 행을 선택 합니다.  
  
    2.  **제거**를 클릭합니다.  
  
        상속 된 매핑을 제거할 수 없습니다. 그러나 상속 된 매핑은 특정 개체 또는 개체 범주에 대 한 사용자 지정 매핑에 의해 무시 됩니다.  
  
## <a name="next-steps"></a>다음 단계  
마이그레이션 프로세스의 다음 단계 중 하나로 [평가 보고서를 만들](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c) 또는 [Sybase ASE 변환 데이터베이스 개체를 SQL Server 또는 SQL Azure 구문](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3)합니다. 평가 보고서를 만드는 경우 Sybase ASE 개체는 자동으로 평가 하는 동안 변환 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
[Azure SQL DB &#40; SQL Server-Sybase ASE 데이터베이스 마이그레이션 SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

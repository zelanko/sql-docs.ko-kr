---
title: 변환 및 마이그레이션 옵션 (AccessToSQL) 설정 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- conversion, setting options
- migration options
- modes
- options, conversion settings
- project settings
- schemas
ms.assetid: 0a7304df-2f35-4453-96ef-7ac83dea1167
caps.latest.revision: 20
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 21cbf6f3a5dac0b77669b940bf27be26198a4456
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393538"
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>변환 및 마이그레이션 옵션 (AccessToSQL) 설정
각 SSMA 프로젝트에 대 한 프로젝트 수준 옵션을 설정할 수 있습니다. 이러한 옵션에는 개체를 변환 하는 방법을, 데이터가 마이그레이션되는 방식 및 원본 데이터 형식을 대상 데이터 형식에 매핑하는 방법을 지정 합니다. 개체를 변환 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터를 마이그레이션하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure, 구성 옵션을 프로젝트에 적절 한지 확인 합니다.  
  
## <a name="configuration-options-and-modes"></a>구성 옵션 및 모드  
SSMA는 4 개의 집합이 구성 설정과 이러한 설정을 구성 하기 위한 4 가지 모드: 기본, Optimistic, 전체 및 사용자 지정 합니다. 대부분의 사용자에 대 한 기본 모드를 사용 하는 것이 좋습니다. 간단한 변환에 대 한 최적 모드를 사용 합니다. 모든 메시지를 확인 하려는 경우 전체 모드를 사용 합니다. 사용자 지정 모드 옵션을 설정합니다.  
  
설정은이 설명서의 "사용자 인터페이스 참조" 섹션에 설명 되어 있습니다. 설정 및 각 모드에는 설정 적용 방법에 대 한 자세한 내용은 다음 항목을 참조 합니다.  
  
-   [프로젝트 설정(변환)](http://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
-   [프로젝트 설정(마이그레이션)](http://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)  
  
-   [프로젝트 설정(GUI)](http://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [프로젝트 설정(형식 매핑)](http://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)  
  
-   [프로젝트 설정 (SQL Azure)](http://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e)  
  
## <a name="setting-project-options"></a>프로젝트 옵션 설정  
SSMA에 모든 프로젝트에 대 한 기본 설정을 구성할 수 있습니다. 이러한 설정은 SSMA 구성 파일에 저장 되며 사용자가 만든 모든 새 프로젝트에 적용 됩니다.  
  
**기본 프로젝트 옵션을 설정 하려면**  
  
1.  에 **도구** 메뉴에서 **기본 프로젝트 설정**합니다.  
  
2.  에 **기본 프로젝트 설정** 대화 상자에서 다음 중 하나를 수행 합니다.  
  
    -   설정을 볼 /에서 변경 하는 데 필요한는 마이그레이션 프로젝트 형식을 선택 **마이그레이션 대상 버전** 드롭다운을 클릭 합니다 **일반** 선택 고왼쪽된창맨아래에**변환 또는 SQL Azure 마이그레이션**합니다.  
  
        > [!NOTE]  
        > SQL Azure 옵션을 사용할 수는 **일반** 만들 프로젝트 형식에는 SQL Azure 경우에 탭 합니다.  
  
    -   미리 정의 된 모드를 선택 하려면 **기본**를 **Optimistic**, 또는 **전체** 에 **모드** 드롭다운 목록 상자입니다.  
  
    -   사용자 지정 모드를 지정 하려면 **사용자 지정** 에 **모드** 상자에서 왼쪽된 창에서 옵션을 선택, 설정 또는 오른쪽 창에서 값을 클릭 한 다음 선택 하거나 새 설정이 나 값을 입력 합니다.  
  
3.  클릭 **확인** 설정을 저장 합니다.  
  
현재 프로젝트에 대 한 설정을 사용자 지정할 수도 있습니다. 이러한 설정은 현재 프로젝트 파일에 저장 됩니다.  
  
**현재 프로젝트에 대 한 설정을 사용자 지정 하려면**  
  
1.  에 **도구** 메뉴에서 **프로젝트 설정을**합니다.  
  
2.  에 **프로젝트 설정** 대화 상자에서 다음 중 하나를 수행 합니다.  
  
    -   미리 정의 된 모드를 선택 하려면 **기본**를 **Optimistic**, 또는 **전체** 에 **모드** 드롭다운 목록 상자입니다.  
  
    -   사용자 지정 모드를 지정 하려면 **사용자 지정** 에 **모드** 상자에서 왼쪽된 창에서 옵션을 선택, 설정 또는 오른쪽 창에서 값을 클릭 한 다음 선택 하거나 새 설정이 나 값을 입력 합니다.  
  
3.  클릭 **확인** 설정을 저장 합니다.  
  
## <a name="next-steps"></a>다음 단계  
다음 단계는 마이그레이션 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   원본 및 대상 데이터 형식 매핑을 사용자 지정 참조 [매핑 소스 및 대상 데이터 형식](mapping-source-and-target-data-types-accesstosql.md)  
  
-   원본 및 대상 데이터베이스의 매핑을 사용자 지정 참조 [매핑 소스 및 대상 데이터베이스](mapping-source-and-target-databases-accesstosql.md)  
  
-   에 대 한 액세스 데이터베이스 개체 정의 변환할 수이 고, 그렇지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체를 정의 합니다. 자세한 내용은 참조 하세요. [Access 데이터베이스 개체 변환](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>관련 항목  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  

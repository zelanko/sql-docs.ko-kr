---
description: 변환 및 마이그레이션 옵션 설정 (AccessToSQL)
title: 변환 및 마이그레이션 옵션 설정 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- conversion, setting options
- migration options
- modes
- options, conversion settings
- project settings
- schemas
ms.assetid: 0a7304df-2f35-4453-96ef-7ac83dea1167
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: cc9a5328095f2ef839eb0c9617798299e46371fd
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987686"
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>변환 및 마이그레이션 옵션 설정 (AccessToSQL)
각 SSMA 프로젝트에 대해 프로젝트 수준 옵션을 설정할 수 있습니다. 이러한 옵션은 개체가 변환 되는 방법, 데이터를 마이그레이션하는 방법 및 원본 데이터 형식을 대상 데이터 형식에 매핑하는 방법을 지정 합니다. 개체를로 변환 하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure 하거나 데이터를 또는 SQL Azure로 마이그레이션하려면 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 옵션이 프로젝트에 적합 한지 확인 합니다.  
  
## <a name="configuration-options-and-modes"></a>구성 옵션 및 모드  
SSMA에는 네 가지 구성 설정 집합과 이러한 설정을 구성 하기 위한 4 가지 모드 (기본, 낙관적, 전체 및 사용자 지정)가 있습니다. 대부분의 사용자에 게 기본 모드를 권장 합니다. 단순 변환에는 낙관적 모드를 사용 합니다. 모든 메시지를 표시 하려면 전체 모드를 사용 합니다. 사용자 지정 모드에서 옵션을 설정 합니다.  
  
설정은이 설명서의 "사용자 인터페이스 참조" 단원에 설명 되어 있습니다. 설정 및 설정 설정에 대 한 자세한 내용은 다음 항목을 참조 하십시오.  
  
-   [프로젝트 설정(변환)](./project-settings-conversion-accesstosql.md)  
  
-   [프로젝트 설정(마이그레이션)](./project-settings-migration-accesstosql.md)  
  
-   [프로젝트 설정(GUI)](../sybase/project-settings-gui-sybasetosql.md)  
  
-   [프로젝트 설정(형식 매핑)](./project-settings-type-mapping-accesstosql.md)  
  
-   [프로젝트 설정 (SQL Azure)](./project-settings-azure-sql-db-accesstosql.md)  
  
## <a name="setting-project-options"></a>프로젝트 옵션 설정  
SSMA에서 모든 프로젝트에 대 한 기본 설정을 구성할 수 있습니다. 이러한 설정은 SSMA 구성 파일에 저장 되 고 사용자가 만드는 모든 새 프로젝트에 적용 됩니다.  
  
**기본 프로젝트 옵션을 설정 하려면**  
  
1.  **도구** 메뉴에서 **기본 프로젝트 설정**을 선택 합니다.  
  
2.  **기본 프로젝트 설정** 대화 상자에서 다음 중 하나를 수행 합니다.  
  
    -   마이그레이션 **대상 버전** 드롭다운에서 설정 하거나 변경 해야 하는 설정에 대 한 마이그레이션 프로젝트 유형을 선택 하 고 왼쪽 창의 맨 아래에 있는 **일반** 을 클릭 한 다음 **변환 또는 마이그레이션 또는 SQL Azure**를 선택 합니다.  
  
        > [!NOTE]  
        > SQL Azure 옵션은 만든 프로젝트 형식이 SQL Azure 되는 경우에만 **일반** 탭에서 사용할 수 있습니다.  
  
    -   미리 정의 된 모드를 선택 하려면 **모드** 드롭다운 상자에서 **기본**, **낙관적**또는 **전체** 를 선택 합니다.  
  
    -   사용자 지정 모드를 지정 하려면 **모드** 상자에서 **사용자 지정** 을 선택 하 고 왼쪽 창에서 옵션을 선택한 다음 오른쪽 창에서 설정 또는 값을 클릭 하 고 새 설정 또는 값을 선택 하거나 입력 합니다.  
  
3.  **확인**을 클릭하여 설정을 저장합니다.  
  
현재 프로젝트에 대 한 설정을 사용자 지정할 수도 있습니다. 이러한 설정은 현재 프로젝트 파일에 저장 됩니다.  
  
**현재 프로젝트에 대 한 설정을 사용자 지정 하려면**  
  
1.  **도구** 메뉴에서 **프로젝트 설정**을 선택 합니다.  
  
2.  **프로젝트 설정** 대화 상자에서 다음 중 하나를 수행 합니다.  
  
    -   미리 정의 된 모드를 선택 하려면 **모드** 드롭다운 상자에서 **기본**, **낙관적**또는 **전체** 를 선택 합니다.  
  
    -   사용자 지정 모드를 지정 하려면 **모드** 상자에서 **사용자 지정** 을 선택 하 고 왼쪽 창에서 옵션을 선택한 다음 오른쪽 창에서 설정 또는 값을 클릭 하 고 새 설정 또는 값을 선택 하거나 입력 합니다.  
  
3.  **확인**을 클릭하여 설정을 저장합니다.  
  
## <a name="next-steps"></a>다음 단계  
마이그레이션의 다음 단계는 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   원본 및 대상 데이터 형식의 매핑을 사용자 지정 하려면 [원본 및 대상 데이터 형식 매핑](mapping-source-and-target-data-types-accesstosql.md) 을 참조 하세요.  
  
-   원본 및 대상 데이터베이스의 매핑을 사용자 지정 하려면 [원본 및 대상 데이터베이스 매핑](mapping-source-and-target-databases-accesstosql.md) 을 참조 하세요.  
  
-   그렇지 않은 경우 Access 데이터베이스 개체 정의를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체 정의로 변환할 수 있습니다. 자세한 내용은 [Access 데이터베이스 개체 변환](converting-access-database-objects-accesstosql.md) 을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  

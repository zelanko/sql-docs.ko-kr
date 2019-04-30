---
title: MySQL 및 SQL Server 데이터 형식 (MySQLToSQL) 매핑 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping, customize data type mapping
- Mapping, Type mapping
ms.assetid: 14f98054-13b4-4231-a6b0-2452f3b9941d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ffe475b53048a97f878bfad1d8bef68d6fb3cfc6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312506"
---
# <a name="mapping-mysql-and-sql-server-data-types-mysqltosql"></a>MySQL 및 SQL Server 데이터 형식 매핑(MySQLToSQL)
MySQL 데이터베이스 형식에서 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터베이스 형식입니다. MySQL 데이터베이스 개체를 변환 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체를 MySQL에서 데이터 형식을 매핑하는 방법을 지정 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다. 기본 데이터 형식 매핑을 그대로 사용 하거나 다음 절차에 표시 된 대로 매핑을 사용자 지정할 수 있습니다.  
  
## <a name="default-mappings"></a>기본 매핑  
SSMA에 기본 데이터 형식 매핑 집합이 있습니다. 기본 매핑 목록을 참조 하세요 [프로젝트 설정 &#40;형식 매핑&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)합니다.  
  
## <a name="type-mapping-inheritance"></a>형식 상속 매핑  
프로젝트 수준, 개체 범주 수준 (예: 모든 저장된 프로시저) 또는 개체 수준에서 형식 매핑을 사용자 지정할 수 있습니다. 하위 수준에서 재정의 되지 않으면 설정이 더 높은 수준에서 상속 됩니다. 예를 들어, 매핑하는 경우 **smallint** 하 **int** 프로젝트 수준에서 프로젝트의 모든 개체 개체나 범주 수준에서 매핑을 사용자 지정 하지 않으면이 매핑을 사용 합니다.  
  
보면 합니다 **형식 매핑** SSMA 백그라운드에서에서 탭은 상속 되는 형식 매핑을 표시할 색으로 구분 합니다. 형식 매핑의 배경이 노란색 상속 된 형식 매핑 및 현재 수준에서 지정 된 모든 매핑에 대 한 백서입니다.  
  
## <a name="customizing-data-type-mappings"></a>사용자 지정 데이터 형식 매핑  
  
-   **데이터 형식을 매핑하려면.**  
  
    다음 절차에는 프로젝트, 데이터베이스 또는 데이터베이스 개체 수준에서의 데이터 형식을 매핑하는 방법을 보여 줍니다.  
  
    1.  전체 프로젝트에 대 한 데이터 형식 매핑 사용자 지정을 하려면 엽니다는 **프로젝트 설정** 대화 상자. 도구 메뉴에서 선택 **프로젝트 설정**합니다.  
  
        왼쪽된 창에서 선택 **형식 매핑**합니다. 형식 매핑 차트 및 단추를 오른쪽 창에 나타납니다.  
  
    2.  데이터베이스 또는 테이블 수준에서 데이터 형식 매핑 사용자 지정 하려면 MySQL 메타 데이터 탐색기에서 데이터베이스 또는 테이블을 선택 합니다. MySQL 메타 데이터 탐색기에서 폴더 또는 사용자 지정 하는 개체를 선택 합니다.  
  
        오른쪽 창에서 클릭 **형식 매핑**합니다.  
  
-   **새 매핑을 추가 하려면 다음을 수행 합니다.**  
  
    1.  형식 매핑 창에서 클릭 **추가** 합니다.  
  
    2.  새 매핑 대화 상자를 아래에 있는 입력 **원본 유형**를 매핑할 MySQL 데이터 형식을 선택 합니다.  
  
    3.  형식에서 길이가 필요한 경우 선택 하 여 매핑에 대 한 최소 및 최대 데이터 길이 지정 합니다 **에서** 및 **에** 확인란을 선택한 다음 값을 입력 합니다.  
  
    4.  이렇게 하면 동일한 데이터 형식의 작고 큰 값 데이터 매핑을 사용자 지정할 수 있습니다. 아래 **대상 유형**, 대상 SQL Server 또는 SQL Azure 데이터 형식을 선택 합니다.  
  
        1.  일부 유형의 대상 데이터 형식의 길이 해야합니다. 필요한 경우 새 데이터 길이 입력 합니다 **바꿀 내용** 상자를 선택한 다음 클릭 **확인**합니다.  
  
        2.  일부 형식에는 대상 데이터 형식이 필요 **정밀도** 하 고 **확장**합니다. 필요한 경우 새 전체 자릿수를 입력 하 고 감축 합니다 **바꿀 내용** 상자를 선택한 다음 클릭 **확인**합니다.  
  
-   **형식 매핑을 편집 하려면 다음을 수행 합니다.**  
  
    1.  형식 매핑 창에서 클릭 **편집**합니다.  
  
    2.  형식 매핑에서 목록 대화 상자, 아래 **원본 유형**를 매핑할 MySQL 데이터 형식을 선택 합니다.  
  
    3.  형식에서 길이가 필요한 경우 선택 하 여 매핑에 대 한 최소 및 최대 데이터 길이 지정 합니다 **에서** 및 **에** 확인란을 선택한 다음 값을 입력 합니다.  
  
    이렇게 하면 동일한 데이터 형식의 작고 큰 값 데이터 매핑을 사용자 지정할 수 있습니다. 아래 **대상 유형**, 대상 SQL Server 또는 SQL Azure 데이터 형식을 선택 합니다.  
  
    1.  일부 유형의 대상 데이터 형식의 길이 해야합니다. 필요한 경우 새 데이터 길이 입력 합니다 **바꿀 내용** 상자를 선택한 다음 클릭 **확인**합니다.  
  
    2.  일부 형식에는 대상 데이터 형식이 필요 **정밀도** 하 고 **확장** 합니다. 필요한 경우 새 전체 자릿수를 입력 하 고 감축 합니다 **바꿀 내용** 상자를 선택한 다음 클릭 **확인** 합니다.  
  
-   **데이터 형식 매핑을 제거 하려면 다음을 수행 합니다.**  
  
    1.  형식 매핑 창에서 제거 하려는 데이터 형식 매핑을 포함 하는 형식 매핑 목록에서 행을 선택 합니다.  
  
    2.  **제거**를 클릭합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는가 중 하나로 [평가 보고서를 만드는](assessing-mysql-databases-for-conversion-mysqltosql.md) 또는 [SQL Server 또는 SQL Azure 구문으로 변환 하는 MySQL 데이터베이스 개체](converting-mysql-databases-mysqltosql.md)합니다. 보고서를 만드는 경우 MySQL 개체를 평가 하는 동안 자동으로 변환 됩니다.  
  
## <a name="see-also"></a>관련 항목  
[SQL Server-Azure SQL DB로 마이그레이션 MySQL 데이터베이스 &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

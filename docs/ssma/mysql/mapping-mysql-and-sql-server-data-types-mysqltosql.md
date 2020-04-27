---
title: MySQL 및 SQL Server 데이터 형식 매핑 (MySQLToSQL) | Microsoft Docs
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
ms.openlocfilehash: 99e86d99a4214b1ccdf317e75218fe22bb2c7af7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67908997"
---
# <a name="mapping-mysql-and-sql-server-data-types-mysqltosql"></a>MySQL 및 SQL Server 데이터 형식 매핑(MySQLToSQL)
MySQL 데이터베이스 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터베이스 형식과 다릅니다. MySQL 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체로 변환 하는 경우 mysql의 데이터 형식 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure를 매핑하는 방법을 지정 해야 합니다. 기본 데이터 형식 매핑을 그대로 적용 하거나 다음 절차에 표시 된 대로 매핑을 사용자 지정할 수 있습니다.  
  
## <a name="default-mappings"></a>기본 매핑  
SSMA에는 기본 데이터 형식 매핑 집합이 있습니다. 기본 매핑 목록은 [프로젝트 설정 &#40;형식 매핑&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)을 참조 하세요.  
  
## <a name="type-mapping-inheritance"></a>형식 매핑 상속  
프로젝트 수준, 개체 범주 수준 (예: 모든 저장 프로시저) 또는 개체 수준에서 형식 매핑을 사용자 지정할 수 있습니다. 낮은 수준에서 재정의 되지 않는 한 설정은 상위 수준에서 상속 됩니다. 예를 들어 프로젝트 수준에서 **smallint** 를 **int** 에 매핑하면 개체 또는 범주 수준에서 매핑을 사용자 지정 하지 않으면 프로젝트의 모든 개체가이 매핑을 사용 합니다.  
  
SSMA에서 **형식 매핑** 탭을 보면 상속 된 형식 매핑을 보여 주기 위해 배경이 색으로 구분 됩니다. 형식 매핑의 배경은 상속 된 형식 매핑의 경우 노란색이 고 현재 수준에서 지정 된 매핑의 경우에는 흰색입니다.  
  
## <a name="customizing-data-type-mappings"></a>데이터 형식 매핑 사용자 지정  
  
-   **데이터 형식을 매핑하려면:**  
  
    다음 절차에서는 프로젝트, 데이터베이스 또는 데이터베이스 개체 수준에서 데이터 형식을 매핑하는 방법을 보여 줍니다.  
  
    1.  전체 프로젝트에 대 한 데이터 형식 매핑을 사용자 지정 하려면 **프로젝트 설정** 대화 상자를 엽니다. 도구 메뉴에서 **프로젝트 설정**을 선택 합니다.  
  
        왼쪽 창에서 **형식 매핑**을 선택 합니다. 오른쪽 창에 형식 매핑 차트와 단추가 표시 됩니다.  
  
    2.  데이터베이스 또는 테이블 수준에서 데이터 형식 매핑을 사용자 지정 하려면 MySQL 메타 데이터 탐색기에서 데이터베이스 또는 테이블을 선택 합니다. MySQL 메타 데이터 탐색기에서 사용자 지정할 폴더나 개체를 선택 합니다.  
  
        오른쪽 창에서 **형식 매핑**을 클릭 합니다.  
  
-   **새 매핑을 추가 하려면 다음을 수행 합니다.**  
  
    1.  형식 매핑 창에서 **추가** 를 클릭 합니다.  
  
    2.  새 형식 매핑 대화 상자의 **원본 유형**에서 매핑할 MySQL 데이터 형식을 선택 합니다.  
  
    3.  형식에 길이가 필요 하면 **시작 및 시작** 확인란을 선택한 다음 **값을 입력** 하 여 매핑에 대 한 최소 및 최대 데이터 길이를 지정 합니다.  
  
    4.  이렇게 하면 동일한 데이터 형식의 더 작고 큰 값에 대 한 데이터 매핑을 사용자 지정할 수 있습니다. **대상 유형**에서 대상 SQL Server 또는 SQL Azure 데이터 형식을 선택 합니다.  
  
        1.  일부 형식에는 대상 데이터 형식 길이가 필요 합니다. 필요한 경우 **바꿀 내용** 상자에 새 데이터 길이를 입력 한 다음 **확인**을 클릭 합니다.  
  
        2.  일부 형식에는 대상 데이터 형식 **전체 자릿수** 와 **소수**자릿수가 필요 합니다. 필요한 경우 **바꿀 내용** 상자에 새로운 전체 자릿수와 소수 자릿수를 입력 한 다음 **확인**을 클릭 합니다.  
  
-   **형식 매핑을 편집 하려면 다음을 수행 합니다.**  
  
    1.  형식 매핑 창에서 **편집**을 클릭 합니다.  
  
    2.  유형 매핑 목록 대화 상자의 **원본 유형**에서 매핑할 MySQL 데이터 형식을 선택 합니다.  
  
    3.  형식에 길이가 필요 하면 **시작 및 시작** 확인란을 선택한 다음 **값을 입력** 하 여 매핑에 대 한 최소 및 최대 데이터 길이를 지정 합니다.  
  
    이렇게 하면 동일한 데이터 형식의 더 작고 큰 값에 대 한 데이터 매핑을 사용자 지정할 수 있습니다. **대상 유형**에서 대상 SQL Server 또는 SQL Azure 데이터 형식을 선택 합니다.  
  
    1.  일부 형식에는 대상 데이터 형식 길이가 필요 합니다. 필요한 경우 **바꿀 내용** 상자에 새 데이터 길이를 입력 한 다음 **확인**을 클릭 합니다.  
  
    2.  일부 형식에는 대상 데이터 형식 **전체 자릿수** 와 **소수** 자릿수가 필요 합니다. 필요한 경우 **바꿀 내용** 상자에 새로운 전체 자릿수와 소수 자릿수를 입력 한 다음 **확인** 을 클릭 합니다.  
  
-   **데이터 형식 매핑을 제거 하려면 다음을 수행 합니다.**  
  
    1.  형식 매핑 창의 제거 하려는 데이터 형식 매핑이 포함 된 형식 매핑 목록에서 행을 선택 합니다.  
  
    2.  **제거**를 클릭합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [평가 보고서를 만들거나](assessing-mysql-databases-for-conversion-mysqltosql.md) [MySQL 데이터베이스 개체를 SQL Server 또는 SQL Azure 구문으로 변환](converting-mysql-databases-mysqltosql.md)하는 것입니다. 보고서를 만드는 경우 MySQL 개체는 평가 중에 자동으로 변환 됩니다.  
  
## <a name="see-also"></a>참고 항목  
[MySQL 데이터베이스를 SQL Server로 마이그레이션-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

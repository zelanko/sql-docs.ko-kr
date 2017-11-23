---
title: "매핑 MySQL 및 SQL Server 데이터 형식 (MySQLToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping, customize data type mapping
- Mapping, Type mapping
ms.assetid: 14f98054-13b4-4231-a6b0-2452f3b9941d
caps.latest.revision: "15"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 48c2a4a1439065bc80f1f233fa500bf8c6f795f3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="mapping-mysql-and-sql-server-data-types-mysqltosql"></a>MySQL 및 SQL Server 데이터 형식 (MySQLToSQL) 매핑
MySQL 데이터베이스 형식이 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 데이터베이스 유형입니다. MySQL 데이터베이스 개체를 변환 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 개체를 MySQL의 데이터 형식을 매핑하는 방법을 지정 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다. 기본 데이터 형식 매핑을 그대로 사용 하거나 다음 절차에 나와 있는 것 처럼 매핑을 사용자 지정할 수 있습니다.  
  
## <a name="default-mappings"></a>기본 매핑  
SSMA에 기본 데이터 형식 매핑 집합이 있습니다. 기본 매핑 목록이 참조 [프로젝트 설정 &#40; 형식 매핑 &#41; &#40; MySQLToSQL &#41; ](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md).  
  
## <a name="type-mapping-inheritance"></a>형식 상속 매핑  
프로젝트 수준, (예: 모든 저장된 프로시저), 범주 수준 개체 또는 개체 수준에서 형식 매핑을 사용자 지정할 수 있습니다. 낮은 수준에서 재정의 되지 않으면 설정은 상위 수준에서 상속 됩니다. 예를 들어, 매핑하는 경우 **smallint** 를 **int** 프로젝트 수준에서 프로젝트의 모든 개체 범주 또는 개체 수준에서 매핑을 사용자 지정 하지 않으면이 매핑을 사용 합니다.  
  
볼 때의 **유형 매핑** SSMA 백그라운드 탭이 상속 되는 형식 매핑 표시 하도록 색이 지정 되어 있습니다. 형식 매핑 배경은 노란색 모든 상속 된 형식 매핑 및 흰색으로 현재 수준에서 지정 된 모든 매핑에 대 한 합니다.  
  
## <a name="customizing-data-type-mappings"></a>사용자 정의 데이터 형식 매핑  
  
-   **데이터 형식을 매핑할:**  
  
    다음 절차에는 프로젝트, 데이터베이스 또는 데이터베이스 개체 수준에서의 데이터 형식을 매핑하는 방법을 보여 줍니다.  
  
    1.  전체 프로젝트에 대 한 데이터 형식 매핑을 사용자 지정 하려면 열에서 **프로젝트 설정** 대화 상자. 도구 메뉴에서 선택 **프로젝트 설정**합니다.  
  
        왼쪽된 창에서 선택 **유형 매핑**합니다. 형식 매핑 차트 및 단추 오른쪽 창에 나타납니다.  
  
    2.  데이터베이스 또는 테이블 수준에서 데이터 형식 매핑을 사용자 지정 하려면 MySQL 메타 데이터 탐색기에서 데이터베이스 또는 테이블을 선택 합니다. MySQL 메타 데이터 탐색기에서 폴더 또는 사용자 지정 하는 개체를 선택 합니다.  
  
        오른쪽 창에서 클릭 **유형 매핑**합니다.  
  
-   **새 매핑을 추가 하려면 다음을 수행 합니다.**  
  
    1.  유형 매핑 창을 클릭 **추가** 합니다.  
  
    2.  New 매핑 대화 상자를 아래에서 입력 **소스 형식**를 매핑할 MySQL 데이터 형식을 선택 합니다.  
  
    3.  형식 길이 필요한 경우 선택 하 여 매핑에 대 한 최소 및 최대 데이터 길이 지정 된 **에서** 및 **를** 확인란을 선택한 다음 값을 입력 합니다.  
  
    4.  이렇게 하면 동일한 데이터 형식의 크기가 작고 더 큰 값에 대 한 데이터 매핑을 사용자 지정할 수 있습니다. 아래 **대상 유형**를 대상 SQL Server 또는 SQL Azure 데이터 형식을 선택 합니다.  
  
        1.  일부 형식은 대상 데이터 형식의 길이가 필요합니다. 필요한 경우 입력에 새 데이터 길이 **바꿀 내용** 상자를 선택한 다음 클릭 **확인**합니다.  
  
        2.  일부 형식은 대상 데이터 유형이 필요한 **정밀도** 및 **배율**합니다. 필요한 경우 새 전체 자릿수를 입력 하 고 확장에 **바꿀 내용** 상자를 선택한 다음 클릭 **확인**합니다.  
  
-   **형식 매핑을 편집 하려면 다음을 수행 합니다.**  
  
    1.  유형 매핑 창을 클릭 **편집**합니다.  
  
    2.  형식 매핑에 목록 대화 상자, 아래에서 **소스 형식**를 매핑할 MySQL 데이터 형식을 선택 합니다.  
  
    3.  형식 길이 필요한 경우 선택 하 여 매핑에 대 한 최소 및 최대 데이터 길이 지정 된 **에서** 및 **를** 확인란을 선택한 다음 값을 입력 합니다.  
  
    이렇게 하면 동일한 데이터 형식의 크기가 작고 더 큰 값에 대 한 데이터 매핑을 사용자 지정할 수 있습니다. 아래 **대상 유형**를 대상 SQL Server 또는 SQL Azure 데이터 형식을 선택 합니다.  
  
    1.  일부 형식은 대상 데이터 형식의 길이가 필요합니다. 필요한 경우 입력에 새 데이터 길이 **바꿀 내용** 상자를 선택한 다음 클릭 **확인**합니다.  
  
    2.  일부 형식은 대상 데이터 유형이 필요한 **정밀도** 및 **배율** 합니다. 필요한 경우 새 전체 자릿수를 입력 하 고 확장에 **바꿀 내용** 상자를 선택한 다음 클릭 **확인** 합니다.  
  
-   **데이터 형식 매핑을 제거 하려면 다음을 수행 합니다.**  
  
    1.  형식 매핑 창에서 제거 하려는 데이터 형식 매핑을 포함 하는 형식 매핑 목록에서 행을 선택 합니다.  
  
    2.  **제거**를 클릭합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계 중 하나로 [평가 보고서를 만들](http://msdn.microsoft.com/en-us/2a56a003-3b0f-453a-963c-00c9e40933ec) 또는 [SQL Server 또는 SQL Azure 구문으로 변환 하는 MySQL 데이터베이스 개체](http://msdn.microsoft.com/en-us/ac21850b-fb32-4704-9985-5759b7c688c7)합니다. 보고서를 만들면 MySQL 개체는 자동으로 평가 하는 동안 변환 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
[Azure SQL DB &#40; SQL Server-MySQL 데이터베이스 마이그레이션 MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

---
title: Access 데이터베이스 개체 변환 (AccessToSQL) | Microsoft Docs
description: SQL Server/Azure SQL Database에 연결한 다음 스키마를 SQL Server/SQL Database 스키마로 변환 하 여 데이터베이스 개체에 액세스를 선택 하는 방법을 알아봅니다.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, converting schemas
- conversion
- conversion, converting schemas
- indexes, altering
- metadata
- metadata, altering
- metadata, converting
- migrating databases, one-click
- one-click migration
- schemas
- schemas, converting
- SQL
- SQL, converting
- syntax
- syntax, converting
- tables, altering
- translating Access to SQL Azure
- translating Access to SQL Server
ms.assetid: e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: f15fc6cee7f66128af7646b9605234e60830b8db
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84302808"
---
# <a name="converting-access-database-objects-accesstosql"></a>Access 데이터베이스 개체 변환 (AccessToSQL)
Access 데이터베이스를 추가 하 고 SQL Azure 또는에 연결 하 고 나면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA에서 access 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure database 개체에 대 한 메타 데이터를 표시 합니다. 이제 데이터베이스 개체에 액세스를 선택한 다음 스키마를 또는 SQL Azure 스키마로 변환할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="the-conversion-process"></a>변환 프로세스  
데이터베이스 개체를 변환 하면 액세스 메타 데이터의 개체 정의를 가져와 동일한 구문으로 변환한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 다음 프로젝트에이 정보를 로드 합니다. 그런 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 메타 데이터 탐색기를 사용 하 여 또는 SQL Azure 개체와 해당 속성을 볼 수 있습니다.  
  
> [!IMPORTANT]  
> 개체를 변환 해도 또는 SQL Azure 개체는 생성 되지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 개체 정의를 변환 하 고 정보를 SSMA 프로젝트에 저장 합니다.  
  
변환 하는 동안 SSMA는 출력 창에 상태를 인쇄 하 고, 오류, 경고 및 정보 메시지를 오류 목록 창에 인쇄 합니다. 이 정보를 사용 하 여 원하는 변환 결과를 얻기 위해 액세스 데이터베이스 또는 변환 프로세스를 수정 해야 하는지 여부를 결정할 수 있습니다. [마이그레이션에 대 한 액세스 데이터베이스 준비](preparing-access-databases-for-migration-accesstosql.md) 항목의 정보를 사용 하 여 변환 되지 않을 항목을 확인할 수도 있습니다.  
  
## <a name="setting-conversion-options"></a>변환 옵션 설정  
개체를 변환 하기 전에 **프로젝트 설정** 대화 상자에서 프로젝트 변환 옵션을 검토 합니다. 이 대화 상자를 사용 하면 SSMA가 인덱싱된 메모 열, 기본 키, 외래 키 제약 조건, 타임 스탬프 및 인덱스 없이 테이블을 변환 하는 방법을 설정할 수 있습니다. 자세한 내용은 [프로젝트 설정 (변환)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388) 을 참조 하세요.  
  
## <a name="conversion-results"></a>변환 결과  
다음 표에서는 변환 된 액세스 개체 및 결과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체를 보여 줍니다.  
  
|Access 개체|결과 SQL Server 개체|  
|-----------------|-------------------------------|  
|테이블|테이블|  
|열|열|  
|인덱스|인덱스|  
|외래 키(foreign key)|외래 키(foreign key)|  
|Query|뷰<br /><br />대부분의 SELECT 쿼리가 뷰로 변환 됩니다. 업데이트 쿼리와 같은 다른 쿼리는 마이그레이션되지 않습니다.<br /><br />매개 변수를 사용 하는 SELECT 쿼리는 변환 되지 않으며 다중 탭 쿼리가 됩니다.|  
|보고서|변환 되지 않음|  
|양식|변환 되지 않음|  
|매크로|변환 되지 않음|  
|모듈(module)|변환 되지 않음|  
|기본값|기본값|  
|길이가 0 인 열 속성 허용|check 제약 조건|  
|열 유효성 검사 규칙|check 제약 조건|  
|테이블 유효성 검사 규칙|check 제약 조건|  
|기본 키(primary key)|기본 키(primary key)|  
  
## <a name="converting-access-objects"></a>액세스 개체 변환  
Access 데이터베이스 개체를 변환 하려면 먼저 변환할 개체를 선택 하 고 SSMA에서 변환을 수행 하도록 해야 합니다. 변환 하는 동안 출력 메시지를 보려면 **보기** 메뉴에서 **출력**을 선택 합니다.  
  
**Access 데이터베이스 개체를 선택 하 여 SQL Server 또는 SQL Azure 구문으로 변환 하려면**  
  
1.  액세스 메타 데이터 탐색기에서 **액세스-메타 베이스**를 확장 한 다음 **데이터베이스**를 확장 합니다.  
  
2.  다음 중 하나 이상을 수행합니다.  
  
    -   모든 데이터베이스를 변환 하려면 **데이터베이스**옆의 확인란을 선택 합니다.  
  
    -   개별 데이터베이스를 변환 하거나 생략 하려면 데이터베이스 이름 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
    -   쿼리를 변환 하거나 생략 하려면 데이터베이스를 확장 한 다음 **쿼리** 확인란을 선택 하거나 선택 취소 합니다.  
  
    -   개별 테이블을 변환 하거나 생략 하려면 데이터베이스를 확장 하 고 **테이블**을 확장 한 다음 테이블 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
3.  다음 작업 중 하나를 수행합니다.  
  
    -   스키마를 변환 하려면 **데이터베이스** 를 마우스 오른쪽 단추로 클릭 하 고 **스키마 변환**을 선택 합니다.  
  
        개별 개체를 변환할 수도 있습니다. 개체를 변환 하려면 선택 된 개체에 관계 없이 개체를 마우스 오른쪽 단추로 클릭 하 고 **스키마 변환**을 선택 합니다.  
  
        개체가 변환 되 면 Access 메타 데이터 탐색기에서 굵게 표시 됩니다.  
  
    -   한 단계에서 스키마 및 데이터를 변환, 로드 및 마이그레이션하려면 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 **변환, 로드 및 마이그레이션**을 선택 합니다.  
  
4.  **출력** 창의 메시지와 **오류 목록** 창에서 발생 하는 오류 및 경고를 검토 합니다.  
  
## <a name="altering-tables-and-indexes"></a>테이블 및 인덱스 변경  
액세스 메타 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 메타 데이터로 변환 하 고 또는 SQL Azure 개체를 로드 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 및 인덱스를 변경 하거나 SQL Azure 수 있습니다.  
  
**테이블 또는 인덱스 속성을 변경 하려면**  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]또는 SQL Azure Metadata 탐색기에서 변경 하려는 테이블이 나 인덱스를 선택 합니다.  
  
2.  **테이블** 탭에서 변경할 속성을 클릭 한 다음 새 설정을 입력 하거나 선택 합니다. 예를 들어 nvarchar (15)를 nvarchar (20)로 변경 하거나 확인란을 선택 하 여 테이블 열을 nullable로 설정할 수 있습니다.  
  
    커서를 변경 된 속성 셀에서 밖으로 이동 합니다. 이렇게 하려면 다른 행을 클릭 하거나 Tab 키를 누릅니다.  
  
3.  **적용**을 클릭합니다.  
  
이제 **SQL** 탭에서 코드의 변경 내용을 볼 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 변환 된 [데이터베이스 개체를로 로드](loading-converted-database-objects-into-sql-server-accesstosql.md) 하는 것입니다 SQL Server  
  
## <a name="see-also"></a>참고 항목  
[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  

---
title: Access 데이터베이스 개체 (AccessToSQL) 변환 | Microsoft Docs
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
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9519ef6b157b1f1d951b93c791f856d6066e7b19
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38981935"
---
# <a name="converting-access-database-objects-accesstosql"></a>Access 데이터베이스 개체 (AccessToSQL) 변환
Access 데이터베이스를 추가 하 고 연결한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure, SSMA 액세스에 대 한 메타 데이터를 표시 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 데이터베이스 개체입니다. 이제 Access 데이터베이스 개체를 선택 하 고 다음 스키마를 변환할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 스키마입니다.  
  
## <a name="the-conversion-process"></a>변환 프로세스  
액세스 메타 데이터에서 개체 정의 데이터베이스 개체 변환, 해당 변환 [!INCLUDE[tsql](../../includes/tsql_md.md)] 구문, 한 다음 프로젝트에이 정보를 로드 합니다. 볼 수 있습니다 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 개체와 해당 속성을 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 메타 데이터 탐색기입니다.  
  
> [!IMPORTANT]  
> 개체 변환에서 개체를 만들지 않으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다. 만 개체 정의 변환 하 고 SSMA 프로젝트에서 정보를 저장 합니다.  
  
변환 중 SSMA 상태 출력 창 및 오류, 경고 및 오류 목록 창에 정보 메시지를 인쇄합니다. 이 정보를 사용 하 여 Access 데이터베이스 또는 원하는 변환 결과 얻으려면 변환 프로세스를 수정 해야 하는지 여부를 결정 합니다. 정보를 사용할 수도 있습니다는 [Access 데이터베이스 마이그레이션에 대 한 준비](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114) 항목 확인 하는 고 변환할 수 없습니다.  
  
## <a name="setting-conversion-options"></a>변환 옵션 설정  
개체를 변환 하기 전에 프로젝트 변환 옵션을 검토 합니다 **프로젝트 설정** 대화 상자. 이 대화 상자를 사용 하 여 SSMA 인덱싱된 메모 열, 기본 키, 외래 키 제약 조건, 타임 스탬프 및 인덱스가 없는 테이블을 변환 하는 방법을 설정할 수 있습니다. 자세한 내용은 참조 하세요. [프로젝트 설정 (변환)](http://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
## <a name="conversion-results"></a>변환 결과  
다음 표에서 변환 되는 경우 개체를 액세스 하 고 결과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 개체:  
  
|개체 액세스|결과 SQL Server 개체|  
|-----------------|-------------------------------|  
|테이블|테이블|  
|column|column|  
|인덱스|인덱스|  
|외래 키(foreign key)|외래 키(foreign key)|  
|Query|뷰<br /><br />가장 선택 쿼리 보기로 변환 됩니다. 업데이트 쿼리와 같은 다른 쿼리는 마이그레이션되지 않습니다.<br /><br />크로스탭 쿼리 매개 변수를 사용 하는 SELECT 쿼리가 없으며 변환 되지 않습니다.|  
|보고서|변환 되지 않음|  
|폼|변환 되지 않음|  
|매크로|변환 되지 않음|  
|module|변환 되지 않음|  
|기본값|기본값|  
|0 길이 열 속성 허용|check 제약 조건|  
|열 유효성 검사 규칙|check 제약 조건|  
|테이블 유효성 검사 규칙|check 제약 조건|  
|기본 키(primary key)|기본 키(primary key)|  
  
## <a name="converting-access-objects"></a>변환 개체에 액세스  
Access 데이터베이스 개체를 변환 하려면 먼저 변환 하 고을 SSMA 변환을 수행 하려는 개체를 선택 해야 합니다. 변환 하는 동안 출력 메시지를 볼 수는 **뷰** 메뉴에서 **출력**합니다.  
  
**선택한 SQL Server 또는 SQL Azure 구문에 Access 데이터베이스 개체 변환**  
  
1.  액세스 메타 데이터 탐색기에서 확장 **액세스-메타 베이스**를 차례로 확장 하 고 **데이터베이스**합니다.  
  
2.  다음 중 하나 이상을 수행 합니다.  
  
    -   모든 데이터베이스를 변환 하려면 확인란을 선택 합니다 옆 **데이터베이스**합니다.  
  
    -   변환 또는 생략 개별 데이터베이스를 선택 하거나 데이터베이스 이름 옆에 있는 확인란의 선택을 취소 합니다.  
  
    -   를 변환 하거나 쿼리를 생략 하려면 데이터베이스를 확장 하 고 다음 선택 하거나 선택을 취소 합니다 **쿼리** 확인란 합니다.  
  
    -   를 변환 하거나 개별 테이블을 생략 하려면 데이터베이스를 확장 **테이블**, 다음을 선택 하거나 표 옆의 확인란의 선택을 취소 합니다.  
  
3.  다음 중 하나를 수행합니다.  
  
    -   스키마로 변환 하려면 마우스 오른쪽 단추로 클릭 **데이터베이스** 선택한 **스키마 변환**합니다.  
  
        또한 개별 개체를 변환할 수 있습니다. 에 관계 없이 선택한 개체가 개체를 변환 하는 개체를 마우스 오른쪽 단추로 클릭 하 고 선택 **스키마 변환**합니다.  
  
        개체로 변환 될 때 액세스 메타 데이터 탐색기에서 굵게 표시 됩니다.  
  
    -   변환, 로드 하 고 한 번의 스키마 및 데이터 마이그레이션, 데이터베이스 및 선택을 마우스 오른쪽 단추로 **변환, 로드 및 마이그레이션**합니다.  
  
4.  메시지를 검토 합니다 **출력** 창 및 모든 오류 및 경고에는 **오류 목록** 창입니다.  
  
## <a name="altering-tables-and-indexes"></a>테이블 및 인덱스 변경  
액세스 메타 데이터를 변환한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 메타 데이터 및 개체를 로드 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 변경할 수 있습니다 SQL Azure 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 테이블 및 인덱스입니다.  
  
**테이블 또는 인덱스 속성을 변경 하려면**  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 메타 데이터 탐색기에서 테이블이 나 인덱스를 변경 하려면 선택 합니다.  
  
2.  에 **테이블** 탭을 변경 하 고을 입력 하거나 새 설정을 선택 하려면 속성을 클릭 합니다. 예를 들어 nvarchar(20), nvarchar(15) 변경 하거나 테이블 열을 null을 허용 하도록 확인란을 선택 수 있습니다.  
  
    변경 된 속성 셀에서 커서를 이동 합니다. Tab 키를 누르거나 다른 행을 클릭 하 여이 수행할 수 있습니다.  
  
3.  **적용**을 클릭합니다.  
  
코드에서 변경 내용을 볼 수 있습니다 합니다 **SQL** 탭 합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [SQL Server로 변환 된 데이터베이스 개체를 로드](http://msdn.microsoft.com/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba)  
  
## <a name="see-also"></a>관련 항목  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

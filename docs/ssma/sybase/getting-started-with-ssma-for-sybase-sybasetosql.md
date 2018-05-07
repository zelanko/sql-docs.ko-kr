---
title: SAP ASE (SybaseToSQL) 용 SSMA 시작 | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: c4098516-f0fc-4690-97bb-3766dfd43156
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2ca14c9049a2f29b8997b59103c4025fea4fd23a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getting-started-with-ssma-for-sap-ase-sybasetosql"></a>SAP ASE (SybaseToSQL) 용 SSMA 시작
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) SAP ASE 사용 하면 신속 하 게에 대 한 변환 SAP 적응형 Server Enterprise (ASE) 데이터베이스 스키마를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스 스키마 결과 스키마 업로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스에서 데이터 및 마이그레이션 SAP ASE를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스입니다.  
  
이 항목 설치 프로세스를 소개 하 고 SSMA 사용자 인터페이스에 익숙해질 수 있습니다.  
  
## <a name="installing-and-licensing-ssma"></a>SSMA 라이선스 및 설치  
SSMA를 사용 하려면 먼저 설치 해야 SSMA 클라이언트 프로그램 소스 인스턴스의 SAP ASE와의 대상 인스턴스 모두에 액세스할 수 있는 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스입니다. 서버 쪽 데이터 마이그레이션을 사용 하려면 설치 해야 확장 팩 및 SAP ASE 공급자 (OLE DB 또는 ADO.NET) 중 하나 이상을 실행 하는 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 이러한 구성 요소는 데이터 마이그레이션 및 SAP ASE 시스템 함수의 에뮬레이션을 지원합니다. 설치 지침을 참조 하십시오. [SAP ASE 용 SSMA 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)합니다.  
  
SSMA를 시작 하려면 **시작**, 가리킨 **모든 프로그램**, 가리킨  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for Sybase**를 선택한 후  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for Sybase**합니다. SSMA를 시작 하는 처음으로 라이선스 대화 상자가 나타납니다. SSMA를 사용 하려면 먼저 Windows Live ID를 사용 하 여 SSMA를 사용 해야 합니다. 라이선스 지침의 설치 지침와 함께 제공 되는 [Sybase 클라이언트에 대 한 설치 SSMA &#40;SybaseToSQL&#41; ](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md) 항목입니다.  
  
## <a name="ssma-for-sap-ase-user-interface"></a>SAP ASE 사용자 인터페이스용 SSMA  
SSMA 설치 및 사용이 허가 된 후에 SAP ASE 데이터베이스를 마이그레이션할 SSMA를 사용할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스입니다. 시작 하기 전에 SSMA 사용자 인터페이스에 잘 알고 있을 수 있습니다. 다음 다이어그램은 SSMA를 메타 데이터 탐색기, 메타 데이터, 도구 모음, 출력 창 및 오류 목록 창에 대 한 사용자 인터페이스를 보여 줍니다.  
  
![SAP ASE 사용자 인터페이스용 SSMA](../../ssma/sybase/media/ssmaforsybaseuserinterface.jpg "SAP ASE 사용자 인터페이스용 SSMA")  
  
마이그레이션을 시작 하려면 새 프로젝트를 먼저 만들어야 할 합니다. 그런 다음, SAP ASE에 연결할 수도 있습니다. 연결 완료 후 SAP ASE 데이터베이스의 계층 구조는 Sybase 메타 데이터 탐색기에 표시 됩니다. Sybase 메타 데이터 탐색기와 같은 작업을 수행 하에서 마우스 오른쪽 단추로 개체 변환이 평가 하는 보고서를 만들 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스입니다. 또한 도구 모음과 메뉴를 통해 이러한 작업을 수행할 수 있습니다.  
  
또한의 인스턴스에 연결 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스입니다. 계층 구조 라는 연결 완료 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 하거나 Azure SQL 데이터베이스에 표시 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 메타 데이터 탐색기입니다. SAP ASE 스키마를 변환한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Azure SQL 데이터베이스 스키마의 이러한 변환 된 스키마를 선택 하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 메타 데이터 탐색기를 다음으로 스키마를 로드 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스입니다.  
  
으로 변환 된 스키마를 로드 한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 있고 Azure SQL 데이터베이스, Sybase 메타 데이터 탐색기로 돌아갑니다로 SAP ASE 데이터베이스에서 데이터를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스입니다.  
  
이러한 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 [SAP ASE 데이터베이스를 SQL Server-Azure SQL 데이터베이스 마이그레이션 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)합니다.  
  
다음 섹션에서는 SSMA 사용자 인터페이스의 기능을 설명 합니다.  
  
### <a name="metadata-explorers"></a>메타 데이터 탐색기  
SSMA 포함을 찾아서 SAP ASE에서 작업을 수행할 두 메타 데이터 탐색기 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스입니다.  
  
#### <a name="sybase-metadata-explorer"></a>Sybase 메타 데이터 탐색기  
Sybase 메타 데이터 탐색기 SAP ASE 원본 인스턴스의 데이터베이스에 대 한 정보를 보여 줍니다.  
  
Sybase 메타 데이터 탐색기를 사용 하 여 다음 작업을 수행할 수 있습니다.  
  
-   각 데이터베이스의 테이블을 탐색 합니다.  
  
-   변환에 대 한 개체를 선택 하 고 다음 개체를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스 구문이 있습니다. 자세한 내용은 참조 [SAP ASE 데이터베이스 개체 변환 &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)합니다.  
  
-   데이터 마이그레이션에 대 한 개체를 선택한 다음 해당 개체에서 데이터를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스입니다. 자세한 내용은 참조 [SAP ASE 데이터를 SQL Server-Azure SQL 데이터베이스 마이그레이션 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md)합니다.  
  
#### <a name="sql-server-or-sql-azure-metadata-explorer"></a>SQL Server 또는 SQL Azure 메타 데이터 탐색기  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스에 대 한 정보를 표시 하는 SQL Azure 메타 데이터 탐색기 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스입니다. 인스턴스로 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스, SSMA 해당 인스턴스에 대 한 메타 데이터를 검색 하 고 프로젝트 파일에 저장 합니다.  
  
사용할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 변환 된 SAP ASE 데이터베이스 개체를 선택한 후 로드 하는 SQL Azure 메타 데이터 탐색기 (동기화)의 인스턴스로 해당 개체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스입니다.  
  
자세한 내용은 참조 [를 SQL Server로 변환 된 데이터베이스 개체를 로드 &#40;SybaseToSQL&#41;](../../ssma/sybase/loading-converted-database-objects-into-sql-server-sybasetosql.md)합니다.  
  
### <a name="metadata"></a>메타데이터  
각 메타 데이터 탐색기의 오른쪽에는 선택한 개체를 설명 하는 탭이 있습니다. 예를 들어 Sybase 메타 데이터 탐색기에서 테이블을 선택 하는 경우 6 개의 탭에 나타납니다: **테이블**, **SQL**, **유형 매핑**, **데이터**,  **속성**, 및 **보고서**합니다. **보고서** 탭 선택된 된 개체를 포함 하는 보고서를 만든 후에 정보를 포함 합니다. 테이블을 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SQL Azure 메타 데이터 탐색기에서 세 개의 탭 표시 또는: **테이블**, **SQL**, 및 **데이터**합니다.  
  
대부분의 설정은 메타 데이터는 읽기 전용입니다. 그러나 다음과 같은 메타 데이터를 변경할 수 있습니다.  
  
-   Sybase 메타 데이터 탐색기에서 프로시저를 변경 하 고 형식 매핑을 수 있습니다. 스키마를 변환 하기 전에 이러한 변경 내용을 확인 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 하거나 변경할 수 SQL Azure 메타 데이터 탐색기는 [!INCLUDE[tsql](../../includes/tsql_md.md)] 저장된 프로시저에 대 한 합니다. 스키마를 로드 하기 전에 이러한 변경 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
메타 데이터 탐색기에서 변경 내용을 원본 또는 대상 데이터베이스에 없는 프로젝트 메타 데이터에 반영 됩니다.  
  
### <a name="toolbars"></a>도구 모음  
SSMA는 두 개의 도구 모음: 프로젝트 도구 모음 및 마이그레이션 도구 모음입니다.  
  
#### <a name="the-project-toolbar"></a>프로젝트 도구 모음  
프로젝트 도구 모음 프로젝트 작업, SAP ASE에 연결에 연결 하기 위한 단추가 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스입니다. 이 단추에 명령을 유사는 **파일** 메뉴.  
  
#### <a name="the-migration-toolbar"></a>마이그레이션 도구 모음  
마이그레이션 도구 모음에는 다음 명령도 포함 됩니다.  
  
|단추|함수|  
|----------|------------|  
|**보고서 만들기**|선택한 SAP ASE 개체를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구문 다음 얼마나 성공적인 변환 작업이 보여 주는 보고서를 만듭니다.<br /><br />이 명령은 Sybase 메타 데이터 탐색기에서 개체를 선택한 경우에 있습니다.|  
|**스키마 변환**|선택한 SAP ASE 개체를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스 개체입니다.<br /><br />이 명령은 Sybase 메타 데이터 탐색기에서 개체를 선택한 경우에 있습니다.|  
|**데이터 마이그레이션**|SAP ASE 데이터베이스에서 데이터를 마이그레이션하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스입니다. 이 명령을 실행 하기 전에 SAP ASE 스키마를 변환 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스 스키마가 개체를 로드 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스입니다.<br /><br />이 명령은 Sybase 메타 데이터 탐색기에서 개체를 선택한 경우에 있습니다.|  
|**중지**|개체를 쓰는 등 현재 프로세스를 중단 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스 구문이 있습니다.|  
  
### <a name="menus"></a>메뉴  
SSMA 메뉴가 포함 되어 있습니다.  
  
|메뉴|Description|  
|--------|---------------|  
|**파일**|프로젝트 작업, SAP ASE에 연결에 연결 하기 위한 명령이 포함 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스입니다.|  
|**편집**|검색 및 텍스트를 복사 하는 등의 세부 정보 페이지에서 작업 하기 위한 명령이 포함 되어 [!INCLUDE[tsql](../../includes/tsql_md.md)] SQL 세부 정보 창에서. 도 포함 되어는 **관리 책갈피** 기존 책갈피의 목록을 볼 수 있는 옵션입니다. 책갈피를 관리 하는 대화 상자의 오른쪽에 단추를 사용할 수 있습니다.|  
|**보기**|포함 된 **동기화 메타 데이터 탐색기** 명령입니다. Sybase 메타 데이터 탐색기 간에 개체를 동기화 하는이 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 메타 데이터 탐색기입니다. 표시 하거나 숨기려면 명령도 포함는 **출력** 및 **오류 목록** 창 및 옵션 **레이아웃** 레이아웃을 관리할 수 있습니다.|  
|**Tools**|보고서를 만들 데이터를 내보내고 개체와 데이터를 마이그레이션하는 명령이 포함 됩니다. 또한에 대 한 액세스를 제공 된 **전역 설정** 및 **프로젝트 설정** 대화 상자.|  
|**테스터**|테스트 사례, 테스트 결과 보기 및 백업 관리 데이터베이스에 대 한 명령을 만드는 명령을 포함 합니다.|  
|**도움말**|SSMA 있도록 및에 대 한 액세스를 제공는 **에 대 한** 대화 상자.|  
  
### <a name="output-pane-and-error-list-pane"></a>출력 창 및 오류 목록 창  
**보기** 메뉴는 출력 창 및 오류 목록 창 표시 유형을 전환 하려면 명령을 제공 합니다.  
  
-   출력 창 개체 변환, 개체 동기화 및 데이터 마이그레이션 중 SSMA에서 상태 메시지를 표시 합니다.  
  
-   오류 목록 창에 정렬할 수 있는 목록의 오류, 경고 및 정보 메시지를 표시 합니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server-Azure SQL 데이터베이스에 SAP ASE 데이터베이스 마이그레이션 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[사용자 인터페이스 참조 &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  

---
title: SAP ASE 용 SSMA 시작 (SybaseToSQL) | Microsoft Docs
description: SAP ASE 설치 프로세스에 대 한 SSMA (SQL Server Migration Assistant)에 대해 알아보고 SSMA 사용자 인터페이스를 숙지 합니다.
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c4098516-f0fc-4690-97bb-3766dfd43156
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: cd6e32470673a87a410530298972b251d2807e4b
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87931813"
---
# <a name="getting-started-with-ssma-for-sap-ase-sybasetosql"></a>SAP ASE 용 SSMA 시작 (SybaseToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SAP ASE 용 SSMA (Migration Assistant)를 사용 하면 SAP 적응 서버 엔터프라이즈 (ASE) 데이터베이스 스키마를 또는 Azure SQL Database 스키마로 신속 하 게 변환 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고, 결과 스키마를 또는 Azure SQL Database에 업로드 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고, sap ASE에서 또는 Azure SQL Database로 데이터를 마이그레이션할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
이 항목에서는 설치 프로세스를 소개 하 고 SSMA 사용자 인터페이스를 숙지 하는 방법을 설명 합니다.  
  
## <a name="installing-and-licensing-ssma"></a>SSMA 설치 및 라이선스  
SSMA를 사용 하려면 먼저 SAP ASE의 원본 인스턴스와의 대상 인스턴스 또는 Azure SQL Database 모두에 액세스할 수 있는 컴퓨터에 SSMA 클라이언트 프로그램을 설치 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 서버 쪽 데이터 마이그레이션을 사용 하려면를 실행 하는 컴퓨터에 확장 팩과 하나 이상의 SAP ASE 공급자 (OLE DB 또는 ADO.NET)를 설치 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이러한 구성 요소는 데이터 마이그레이션과 SAP ASE 시스템 함수의 에뮬레이션을 지원 합니다. 설치 지침은 [SAP ASE 용 SSMA 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)를 참조 하세요.  
  
Ssma를 시작 하려면 **시작**을 클릭 하 고 **모든 프로그램**, ** [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sybase Migration Assistant**를 차례로 가리킨 다음 ** [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sybase에 대해 Migration Assistant**를 선택 합니다. SSMA를 처음 시작할 때 라이선스 대화 상자가 나타납니다. SSMA를 사용 하려면 먼저 Windows Live ID를 사용 하 여 SSMA를 사용 하도록 허가 해야 합니다. 라이선스 지침은 [Sybase 용 SSMA 클라이언트 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md) 항목의 설치 지침에 포함 되어 있습니다.  
  
## <a name="ssma-for-sap-ase-user-interface"></a>SAP ASE 사용자 인터페이스용 SSMA  
SSMA가 설치 되 고 사용이 허가 된 후 SSMA를 사용 하 여 SAP ASE 데이터베이스를 또는 Azure SQL Database로 마이그레이션할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 시작 하기 전에 SSMA 사용자 인터페이스에 익숙해질 수 있습니다. 다음 다이어그램은 메타 데이터 탐색기, 메타 데이터, 도구 모음, 출력 창 및 오류 목록 창을 포함 하 여 SSMA의 사용자 인터페이스를 보여 줍니다.  
  
![SAP ASE 사용자 인터페이스용 SSMA](../../ssma/sybase/media/ssmaforsybaseuserinterface.jpg "SAP ASE 사용자 인터페이스용 SSMA")  
  
마이그레이션을 시작 하려면 먼저 새 프로젝트를 만들어야 합니다. 그런 다음 SAP ASE에 연결 합니다. 성공적으로 연결 된 후에는 Sybase 메타 데이터 탐색기에 SAP ASE 데이터베이스의 계층이 표시 됩니다. 그런 다음 Sybase 메타 데이터 탐색기에서 개체를 마우스 오른쪽 단추로 클릭 하 여 변환 또는 Azure SQL Database을 평가 하는 보고서 만들기와 같은 태스크를 수행할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 도구 모음 및 메뉴를 통해 이러한 작업을 수행할 수도 있습니다.  
  
또한 인스턴스에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하거나 Azure SQL Database 해야 합니다. 연결이 성공적으로 완료 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 되 면 또는 AZURE SQL 데이터베이스의 계층 구조가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 메타 데이터 탐색기에 나타납니다. SAP ASE 스키마를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL Database 스키마로 변환한 후에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 메타 데이터 탐색기에서 변환 된 스키마를 선택 하 고 스키마를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL Database로 로드 합니다.  
  
변환 된 스키마를 또는 Azure SQL Database으로 로드 한 후에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sybase Metadata Explorer로 돌아가서 SAP ASE 데이터베이스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL database로 데이터를 마이그레이션할 수 있습니다.  
  
이러한 작업 및 이러한 작업을 수행 하는 방법에 대 한 자세한 내용은 [SAP ASE 데이터베이스를 SQL Server-Azure SQL Database &#40;SybaseToSQL&#41;로 마이그레이션 ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)을 참조 하세요.  
  
다음 섹션에서는 SSMA 사용자 인터페이스의 기능에 대해 설명 합니다.  
  
### <a name="metadata-explorers"></a>메타 데이터 탐색기  
SSMA는 SAP ASE 및 또는 Azure SQL database에 대 한 작업을 탐색 하 고 수행 하는 두 개의 메타 데이터 탐색기를 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
#### <a name="sybase-metadata-explorer"></a>Sybase 메타 데이터 탐색기  
Sybase 메타 데이터 탐색기는 SAP ASE의 원본 인스턴스에 있는 데이터베이스에 대 한 정보를 표시 합니다.  
  
Sybase 메타 데이터 탐색기를 사용 하 여 다음 작업을 수행할 수 있습니다.  
  
-   각 데이터베이스에서 테이블을 찾습니다.  
  
-   변환할 개체를 선택한 다음 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL Database 구문으로 변환 합니다. 자세한 내용은 [SAP ASE 데이터베이스 개체 변환 &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)을 참조 하세요.  
  
-   데이터 마이그레이션을 위한 개체를 선택한 다음 해당 개체의 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL Database로 마이그레이션합니다. 자세한 내용은 [SAP ASE 데이터를 SQL Server로 마이그레이션-Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md)를 참조 하세요.  
  
#### <a name="sql-server-or-sql-azure-metadata-explorer"></a>메타 데이터 탐색기 SQL Server 또는 SQL Azure  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]또는 SQL Azure Metadata 탐색기에 또는 Azure SQL Database의 인스턴스에 대 한 정보가 표시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 됩니다. 또는 Azure SQL Database 인스턴스에 연결 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA는 해당 인스턴스에 대 한 메타 데이터를 검색 하 여 프로젝트 파일에 저장 합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]또는 SQL Azure Metadata 탐색기를 사용 하 여 변환 된 SAP ASE 데이터베이스 개체를 선택한 다음 해당 개체를 인스턴스나 Azure SQL Database 로드 (동기화) 할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
자세한 내용은 [변환 된 데이터베이스 개체를 SQL Server &#40;SybaseToSQL&#41;로드 ](../../ssma/sybase/loading-converted-database-objects-into-sql-server-sybasetosql.md)를 참조 하세요.  
  
### <a name="metadata"></a>메타데이터  
각 메타 데이터 탐색기의 오른쪽에는 선택한 개체를 설명 하는 탭이 있습니다. 예를 들어 Sybase 메타 데이터 탐색기에서 테이블을 선택 하면 **테이블**, **SQL**, **형식 매핑**, **데이터**, **속성**및 **보고서**의 6 개 탭이 표시 됩니다. 선택한 개체가 포함 된 보고서를 만든 후에만 **보고서** 탭에 정보가 포함 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]또는 SQL Azure 메타 데이터 탐색기에서 테이블을 선택 하면 **테이블**, **SQL**및 **데이터**라는 세 개의 탭이 표시 됩니다.  
  
대부분의 메타 데이터 설정은 읽기 전용입니다. 그러나 다음 메타 데이터를 변경할 수 있습니다.  
  
-   Sybase 메타 데이터 탐색기에서 프로시저 및 형식 매핑을 변경할 수 있습니다. 스키마를 변환 하기 전에 이러한 변경을 수행 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]또는 SQL Azure Metadata 탐색기에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저에 대 한를 변경할 수 있습니다. 에 스키마를 로드 하기 전에 이러한 변경을 수행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
메타 데이터 탐색기에서 변경한 내용은 원본 또는 대상 데이터베이스가 아니라 프로젝트 메타 데이터에 반영 됩니다.  
  
### <a name="toolbars"></a>도구 모음  
SSMA에는 프로젝트 도구 모음과 마이그레이션 도구 모음 이라는 두 가지 도구 모음이 있습니다.  
  
#### <a name="the-project-toolbar"></a>프로젝트 도구 모음  
프로젝트 도구 모음에는 프로젝트 작업, SAP ASE에 연결, 또는 Azure SQL Database에 연결 하는 단추가 포함 되어 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이러한 단추는 **파일** 메뉴의 명령과 유사 합니다.  
  
#### <a name="the-migration-toolbar"></a>마이그레이션 도구 모음  
마이그레이션 도구 모음에는 다음 명령이 포함 되어 있습니다.  
  
|단추|기능|  
|----------|------------|  
|**보고서 만들기**|선택한 SAP ASE 개체를 구문으로 변환한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 후 변환의 성공 여부를 보여 주는 보고서를 만듭니다.<br /><br />이 명령은 Sybase 메타 데이터 탐색기에서 개체를 선택한 경우에만 사용할 수 있습니다.|  
|**스키마 변환**|선택한 SAP ASE 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL Database 개체로 변환 합니다.<br /><br />이 명령은 Sybase 메타 데이터 탐색기에서 개체를 선택한 경우에만 사용할 수 있습니다.|  
|**데이터 마이그레이션**|SAP ASE 데이터베이스에서 또는 Azure SQL Database 데이터를 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이 명령을 실행 하기 전에 SAP ASE 스키마를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL Database 스키마로 변환한 다음 개체를 또는 Azure SQL Database로 로드 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br />이 명령은 Sybase 메타 데이터 탐색기에서 개체를 선택한 경우에만 사용할 수 있습니다.|  
|**중지**|개체를로 변환 하거나 구문을 Azure SQL Database 하는 등 현재 프로세스를 중지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.|  
  
### <a name="menus"></a>메뉴  
SSMA에는 다음 메뉴가 포함 됩니다.  
  
|메뉴|Description|  
|--------|---------------|  
|**최근에 사용한 파일**|프로젝트 작업, SAP ASE에 연결, 또는 Azure SQL Database에 연결 하기 위한 명령이 포함 되어 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**편집**|SQL 세부 정보 창에서 복사와 같이 세부 정보 페이지에서 텍스트를 찾고 사용 하는 명령이 포함 되어 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] . 또한 기존 책갈피 목록을 볼 수 있는 **책갈피 관리** 옵션도 포함 되어 있습니다. 대화 상자의 오른쪽에 있는 단추를 사용 하 여 책갈피를 관리할 수 있습니다.|  
|**보기**|**메타 데이터 탐색기 동기화** 명령을 포함 합니다. 그러면 Sybase 메타 데이터 탐색기와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure 메타 데이터 탐색기 간에 개체가 동기화 됩니다. 에는 **출력** 및 **오류 목록** 창과 레이아웃을 관리 하는 옵션 **레이아웃** 을 표시 하 고 숨기는 명령도 포함 됩니다.|  
|**도구**|보고서를 만들고, 데이터를 내보내고, 개체와 데이터를 마이그레이션하는 명령을 포함 합니다. 또한 **전역 설정** 및 **프로젝트 설정** 대화 상자에 대 한 액세스를 제공 합니다.|  
|**테스터**|테스트 사례를 만들고, 테스트 결과를 보고, 데이터베이스 백업 관리 명령을 포함 하는 명령을 포함 합니다.|  
|**도움말**|SSMA 도움말과 정보 대화 상자에 대 **한** 액세스를 제공 합니다.|  
  
### <a name="output-pane-and-error-list-pane"></a>출력 창 및 오류 목록 창  
**보기** 메뉴는 출력 창 및 오류 목록 창의 표시 여부를 전환 하는 명령을 제공 합니다.  
  
-   출력 창에는 개체 변환, 개체 동기화 및 데이터 마이그레이션 중에 SSMA의 상태 메시지가 표시 됩니다.  
  
-   오류 목록 창에는 정렬할 수 있는 목록에서 오류, 경고 및 정보 메시지가 표시 됩니다.  
  
## <a name="see-also"></a>참고 항목  
[SAP ASE 데이터베이스를 SQL Server-Azure SQL Database &#40;SybaseToSQL&#41;로 마이그레이션](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[사용자 인터페이스 참조 &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  

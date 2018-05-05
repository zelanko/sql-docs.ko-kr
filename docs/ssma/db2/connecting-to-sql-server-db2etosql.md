---
title: SQL Server (DB2eToSQL)에 연결 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-db2
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
ms.assetid: b59803cb-3cc6-41cc-8553-faf90851410e
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d257c6b2569eec1677577e8fe98a0fe619ab60f1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-sql-server-db2etosql"></a>SQL Server (DB2eToSQL)에 연결
DB2 데이터베이스를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]의 이러한 대상 인스턴스 중 하나에 연결 해야 하는 2014 또는 Azure SQL DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. SSMA는 인스턴스의 모든 데이터베이스에 대 한 메타 데이터를 가져오며 연결 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에서 데이터베이스 메타 데이터를 표시 하 고는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터 탐색기입니다. SSMA는의 인스턴스에 대 한 정보를 저장 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에 연결 되어 있지만 암호를 저장 하지 않습니다.  
  
에 대 한 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 프로젝트를 닫을 때까지 활성 상태로 유지 합니다. 에 다시 연결 해야 프로젝트를 다시 열 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 활성 서버에 연결 하려는 경우. 데이터베이스 개체에 로드 될 때까지 오프 라인으로 작업할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터를 마이그레이션합니다.  
  
인스턴스에 대 한 메타 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 자동으로 동기화 되지 않습니다. 대신에 메타 데이터를 업데이트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터 탐색기를 수동으로 업데이트 해야는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터입니다. 자세한 내용은 참조는 "Synchronizing [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터"이이 항목의 뒷부분에 나오는 섹션.  
  
## <a name="required-sql-server-permissions"></a>필요한 SQL Server 사용 권한  
에 연결 하는 데 사용 되는 계정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 계정 수행 하는 작업에 따라 다른 사용 권한이 필요 합니다.  
  
-   DB2 개체를 변환 하려면 [!INCLUDE[tsql](../../includes/tsql_md.md)] 구문에서 메타 데이터를 업데이트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 변환 된 구문에 스크립트를 저장 하려면 계정이의 인스턴스에 로그온 할 수 있는 권한이 있어야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
-   에 데이터베이스 개체를 로드 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]의 계정은의 구성원 이어야 합니다는 **sysadmin** 서버 역할입니다. CLR 어셈블리를 설치 해야 합니다.  
  
-   데이터를 마이그레이션하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]의 계정은의 구성원 이어야 합니다는 **sysadmin** 서버 역할입니다. 이것은 실행 하는 데 필요는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 데이터 마이그레이션 패키지 합니다.  
  
-   SSMA에 의해 생성 된 코드를 실행 하려면 계정 있어야 **Execute** 의 모든 사용자 정의 함수에 대 한 권한을 **ssma_DB2** 대상 데이터베이스의 스키마입니다. 이러한 함수는 DB2 시스템 함수의 동일한 기능을 제공 하 고 변환 된 개체에 의해 사용 됩니다.  
  
경우에 연결 하는 데 사용 되는 계정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 모든 마이그레이션을 수행 하기 위해 작업을 계정이의 구성원 이어야 합니다.이 **sysadmin** 서버 역할입니다.  
  
## <a name="establishing-a-sql-server-connection"></a>SQL Server 연결 설정  
DB2 데이터베이스 개체를 변환 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구문의 인스턴스에 대 한 연결을 설정 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] DB2 데이터베이스 또는 데이터베이스를 마이그레이션할 하려는 합니다.  
  
연결 속성을 정의할 때도 데이터베이스 개체와 데이터 마이그레이션할 수를 지정 합니다. 에 연결한 후 DB2 스키마 수준에서이 매핑을 사용자 지정할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 자세한 내용은 참조 [DB2 스키마를 SQL Server 스키마로 매핑 &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md)합니다.  
  
> [!IMPORTANT]  
> 에 연결 하려고 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 있는지 확인 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 실행 중이 고 연결을 허용할 수 있습니다.  
  
**SQL Server에 연결 하려면**  
  
1.  에 **파일** 메뉴 선택 **SQL Server에 연결**합니다.  
  
    이전에 연결한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 명령 이름은 **SQL Server에 다시 연결**합니다.  
  
2.  연결 대화 상자에서 이름을 입력 하거나 선택 된 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
    -   로컬 컴퓨터의 기본 인스턴스에 연결 하는 경우 입력할 수 있는 **localhost** 또는 점 (**.**).  
  
    -   다른 컴퓨터의 기본 인스턴스에 연결 하는 경우에 컴퓨터의 이름을 입력 합니다.  
  
    -   다른 컴퓨터에 명명 된 인스턴스에 연결 하는 경우 그 다음에 백슬래시 및 인스턴스 이름을 MyServer\MyInstance 같은 컴퓨터 이름을 입력 합니다.  
  
3.  경우 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에 사용 되는 포트 번호를 입력, 기본이 아닌 포트에서 연결을 허용 하도록 구성 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 의 연결 모드는 **서버 포트** 상자입니다. 기본 인스턴스에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 기본 포트 번호는 1433입니다. 명명 된 인스턴스에 대 한 SSMA는에서 포트 번호 가져오기를 시도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Browser 서비스입니다.  
  
4.  에 **데이터베이스** 상자 대상 데이터베이스의 이름을 입력 합니다.  
  
    다시 연결할 때이 옵션을 사용할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
5.  에 **인증** 상자에서 연결에 사용할 인증 유형을 선택 합니다. 현재 Windows 계정을 사용 하려면 선택 **Windows 인증**합니다. 사용 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 로그인을 **SQL Server 인증**, 로그인 이름 및 암호를 제공 합니다.  
  
6.  보안 연결에 대 한 두 개의 컨트롤이 추가 되는 **연결 암호화** 및 **TrustServerCertificate** 확인란 합니다. 경우에만 **연결 암호화** 확인란이 **TrustServerCertificate** 확인란이 표시 됩니다. 때 **연결 암호화** (true)을 선택 하 고 **TrustServerCertificate** 선택 하지 않으면 (false) 인 검사지 것입니다 SQL Server SSL 인증서입니다. 서버 인증서의 유효성 검사는 SSL 핸드셰이크의 일부로 서버가 연결할 올바른 서버인지 확인합니다. 이 위해 서버 쪽 뿐만 아니라 클라이언트측에서 인증서를 설치 합니다.  
  
7.  **연결**을 클릭합니다.  
  
**더 높은 버전 호환성**  
  
-   에 연결할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 생성 되는 마이그레이션 프로젝트의 경우 2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005입니다.  
  
-   에 연결할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 생성 되는 마이그레이션 프로젝트의 경우 2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 있지만 즉, 더 낮은 버전에 연결할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
-   에 연결할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 때 생성 되는 프로젝트는 SQL Server 2012.  
  
||||||  
|-|-|-|-|-|  
|**프로젝트 형식 및 대상 서버 버전**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 <br />(Version:13.x)|Azure SQL DB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|예|사용자 계정 컨트롤|예||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014||예|예||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014|||예||  
|Azure SQL DB||||예|  
  
> [!IMPORTANT]  
> 데이터베이스 개체의 변환을 수행 하는 프로젝트 형식에 따라 하지만의 버전에 따라 하지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에 연결 되어 있습니다. 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 년 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 또는 Azure SQL DB입니다.  
  
## <a name="synchronizing-sql-server-metadata"></a>SQL Server 메타 데이터를 동기화합니다.  
메타 데이터에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 자동으로 업데이트 되지 않습니다. 메타 데이터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에 처음 연결 하는 경우 메타 데이터 탐색기는 메타 데이터의 스냅숏으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 마지막 시간을 수동으로 업데이트 된 메타 데이터 또는 합니다. 모든 데이터베이스에 대해 또는 모든 단일 데이터베이스 또는 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 동기화 하려면**  
  
1.  에 연결 되어 있는지 확인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터 탐색기 데이터베이스 옆의 확인란을 선택 하거나 데이터베이스 스키마를 업데이트 합니다.  
  
    예를 들어 모든 데이터베이스에 대 한 메타 데이터를 업데이트 하려면 상자를 옆에 선택 **데이터베이스**합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **데이터베이스**, 또는 개별 데이터베이스 또는 데이터베이스 스키마를 선택한 후 **데이터베이스와 동기화**합니다.  
  
## <a name="next-step"></a>다음 단계  
다음 단계는 마이그레이션에서 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   DB2 스키마 간의 매핑을 사용자 지정 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 및 스키마 참조 [매핑 DB2 스키마를 SQL Server 스키마로 &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md)합니다.  
  
-   참조 프로젝트에 대 한 구성 옵션을 사용자 지정 하려면 [프로젝트 설정 &#40;변환&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md) 및 관련 구역을 합니다.  
  
-   원본 및 대상 데이터 형식 매핑, 사용자 지정 하려면 참조 [매핑 DB2 및 SQL Server 데이터 형식 &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)합니다.  
  
-   이러한 작업을 수행 해야 하는 경우에 DB2 데이터베이스 개체 정의 변환할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 개체 정의 합니다. 자세한 내용은 참조 [DB2 스키마 변환 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server로 데이터베이스 마이그레이션 DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  

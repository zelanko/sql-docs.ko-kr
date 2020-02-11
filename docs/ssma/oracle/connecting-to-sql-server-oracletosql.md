---
title: SQL Server에 연결 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server,Synchronizing SQL Server Metadata
ms.assetid: 1b2a8059-1829-4904-a82f-9c06de1e245f
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: cd8f0e57554f32d3b02a6e0e98d3a3645d683bac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68266161"
---
# <a name="connecting-to-sql-server-oracletosql"></a>SQL Server에 연결(OracleToSQL)
Oracle 데이터베이스를 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 R2 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014로 마이그레이션하려면의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이러한 대상 인스턴스에 연결 해야 합니다. 연결할 때 SSMA는 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 모든 데이터베이스에 대 한 메타 데이터를 가져오고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기에 데이터베이스 메타 데이터를 표시 합니다. SSMA는 연결 된 인스턴스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대 한 정보를 저장 하지만 암호를 저장 하지는 않습니다.  
  
사용자의 연결은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로젝트를 닫을 때까지 활성 상태로 유지 됩니다. 프로젝트를 다시 열 때 서버에 대 한 활성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결을 원하는 경우에 다시 연결 해야 합니다. 데이터베이스 개체를 로드 하 고 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션할 때까지 오프 라인으로 작업할 수 있습니다.  
  
인스턴스에 대 한 메타 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 자동으로 동기화 되지 않습니다. 대신 메타 데이터 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터를 업데이트 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터를 수동으로 업데이트 해야 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "메타 데이터 동기화" 단원을 참조 하십시오.  
  
## <a name="required-sql-server-permissions"></a>필요한 SQL Server 권한  
에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 하는 데 사용 되는 계정에는 해당 계정에서 수행 하는 작업에 따라 다른 사용 권한이 필요 합니다.  
  
-   Oracle 개체를 구문으로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 변환 하거나에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]메타 데이터를 업데이트 하거나 변환 된 구문을 스크립트에 저장 하려면 계정에 인스턴스에 로그온 할 수 있는 권한이 있어야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   데이터베이스 개체를에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로드 하려면 계정이 **sysadmin** 서버 역할의 멤버 여야 합니다. 이는 CLR 어셈블리를 설치 하는 데 필요 합니다.  
  
-   로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터를 마이그레이션하려면 계정이 **sysadmin** 서버 역할의 멤버 여야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 데이터 마이그레이션 패키지를 실행 하는 데 필요 합니다.  
  
-   SSMA에 의해 생성 된 코드를 실행 하려면 계정에 대상 데이터베이스의 **ssma_oracle** 스키마에 있는 모든 사용자 정의 함수에 대 한 **Execute** 권한이 있어야 합니다. 이러한 함수는 Oracle 시스템 함수에 해당 하는 기능을 제공 하며 변환 된 개체에 사용 됩니다.  
  
에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 하는 데 사용 되는 계정이 모든 마이그레이션 작업을 수행 하는 경우 계정은 **sysadmin** 서버 역할의 멤버 여야 합니다.  
  
## <a name="establishing-a-sql-server-connection"></a>SQL Server 연결 설정  
Oracle 데이터베이스 개체를 구문으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변환 하기 전에 oracle 데이터베이스를 마이그레이션하려는 인스턴스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대 한 연결을 설정 해야 합니다.  
  
연결 속성을 정의 하는 경우 개체 및 데이터가 마이그레이션되는 데이터베이스도 지정 합니다. 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결한 후 Oracle 스키마 수준에서이 매핑을 사용자 지정할 수 있습니다. 자세한 내용은 [Oracle 스키마를 SQL Server 스키마에 매핑 &#40;OracleToSQL&#41;을 ](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md)참조 하세요.  
  
> [!IMPORTANT]  
> 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결을 시도 하기 전에 인스턴스가 실행 중 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 고 연결을 허용할 수 있는지 확인 합니다.  
  
**SQL Server에 연결하려면**  
  
1.  **파일** 메뉴에서 **SQL Server에 연결**을 선택 합니다.  
  
    이전에에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결한 경우 명령 이름이 **SQL Server에 다시 연결**됩니다.  
  
2.  연결 대화 상자에서 인스턴스의 이름을 입력 하거나 선택 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   로컬 컴퓨터의 기본 인스턴스에 연결 하는 경우 **localhost** 또는 점 (**.**)을 입력할 수 있습니다.  
  
    -   다른 컴퓨터의 기본 인스턴스에 연결 하는 경우 컴퓨터 이름을 입력 합니다.  
  
    -   다른 컴퓨터의 명명 된 인스턴스에 연결 하는 경우 컴퓨터 이름, 백슬래시 및 인스턴스 이름 (예: MyServer\MyInstance.)을 차례로 입력 합니다.  
  
3.  인스턴스가 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 아닌 포트에서 연결을 허용 하도록 구성 된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **서버 포트** 상자에서 연결에 사용 되는 포트 번호를 입력 합니다. 기본 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]경우 기본 포트 번호는 1433입니다. 명명 된 인스턴스의 경우 SSMA는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스에서 포트 번호를 가져오려고 시도 합니다.  
  
4.  **데이터베이스** 상자에 대상 데이터베이스의 이름을 입력 합니다.  
  
    에 다시 연결 하는 경우에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는이 옵션을 사용할 수 없습니다.  
  
5.  **인증** 상자에서 연결에 사용할 인증 유형을 선택 합니다. 현재 Windows 계정을 사용 하려면 **Windows 인증**을 선택 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용 하려면 **SQL Server 인증**을 선택 하 고 로그인 이름 및 암호를 제공 합니다.  
  
6.  보안 연결의 경우 **연결 암호화** 및 **trustservercertificate** 확인란의 두 컨트롤이 추가 됩니다. **연결 암호화** 를 선택 하는 경우에만 **trustservercertificate** 확인란이 표시 됩니다. **연결 암호화** 가 확인 되 고 (True) **trustservercertificate** 가 선택 취소 (FALSE) 되 면 SSL 인증서 SQL Server 유효성을 검사 합니다. 서버 인증서의 유효성 검사는 SSL 핸드셰이크의 일부로 서버가 연결할 올바른 서버인지 확인합니다. 이를 위해 클라이언트 쪽 뿐만 아니라 서버 쪽에도 인증서를 설치 해야 합니다.  
  
7.  **연결**을 클릭합니다.  
  
**높은 버전 호환성**  
  
-   만든 마이그레이션 프로젝트가 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 2008 및 2012, 2014 및 2016에 연결할 수 있습니다.  
  
-   생성 되는 마이그레이션 프로젝트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 이지만 더 낮은 버전 (예: 2005)에 연결할 수 없는 경우에는 2012 및 2014 및 2016에 연결할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   프로젝트를 만들 때 2012 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016에 연결할 수는 SQL Server 2012입니다.  
  
||||||||  
|-|-|-|-|-|-|-|  
|**프로젝트 형식 Vs 대상 서버 버전**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005<br /> (버전: 4.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008<br /> (버전: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 <br />(버전: 11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 <br />(버전: 12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(버전: 13.x)|Azure SQL DB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005|yes|yes|yes|yes|yes||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008||yes|yes|yes|yes||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012|||yes|yes|yes||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||yes|yes||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||yes||
|Azure SQL DB||||||yes|
  
> [!IMPORTANT]
> 데이터베이스 개체의 변환은 프로젝트 형식에 따라 수행 되지만 연결 된의 버전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 따라 수행 되지 않습니다. 2005 프로젝트의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 더 높은 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016)에 연결 된 경우에도 2005 당 변환이 수행 됩니다.  
  
## <a name="synchronizing-sql-server-metadata"></a>SQL Server 메타 데이터 동기화  
데이터베이스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대 한 메타 데이터는 자동으로 업데이트 되지 않습니다. 메타 데이터 탐색기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 메타 데이터는 처음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결할 때 메타 데이터에 대 한 스냅숏입니다. 또는 수동으로 메타 데이터를 업데이트 한 경우에는입니다. 모든 데이터베이스 또는 단일 데이터베이스 또는 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 동기화 하려면**  
  
1.  에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결 되어 있는지 확인 합니다.  
  
2.  메타 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 탐색기에서 업데이트 하려는 데이터베이스 또는 데이터베이스 스키마 옆의 확인란을 선택 합니다.  
  
    예를 들어 모든 데이터베이스에 대 한 메타 데이터를 업데이트 하려면 **데이터베이스**옆의 상자를 선택 합니다.  
  
3.  데이터베이스를 마우스 오른쪽 **단추로 클릭 하거나**개별 데이터베이스 또는 데이터베이스 스키마를 클릭 한 다음 **데이터베이스와 동기화**를 선택 합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션의 다음 단계는 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   Oracle 스키마와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 및 스키마 간의 매핑을 사용자 지정 하려면 [oracle 스키마를 SQL Server 스키마에 매핑 &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md)을 참조 하세요.  
  
-   프로젝트에 대 한 구성 옵션을 사용자 지정 하려면 [OracleToSQL&#41;&#40;프로젝트 옵션 설정 ](../../ssma/oracle/setting-project-options-oracletosql.md)을 참조 하세요.  
  
-   원본 및 대상 데이터 형식의 매핑을 사용자 지정 하려면 [OracleToSQL&#41;&#40;Oracle 및 SQL Server 데이터 형식 매핑 ](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)을 참조 하세요.  
  
-   이러한 작업을 수행할 필요가 없는 경우 Oracle 데이터베이스 개체 정의를 개체 정의로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변환할 수 있습니다. 자세한 내용은 [Oracle 스키마 변환 &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
[Oracle 데이터베이스를 SQL Server &#40;OracleToSQL&#41;로 마이그레이션](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

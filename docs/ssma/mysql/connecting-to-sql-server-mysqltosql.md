---
title: SQL Server에 연결 (MySQLToSQL) | Microsoft Docs
description: SQL Server의 대상 인스턴스에 연결 하 여 MySQL 데이터베이스를 마이그레이션하는 방법에 대해 알아봅니다. SSMA는 SQL Server의 데이터베이스에 대 한 메타 데이터를 가져옵니다.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- connecting to SQL Server 2008, SQL Server permission
- connecting to SQL Server 2008, synchronization
ms.assetid: 08233267-693e-46e6-9ca3-3a3dfd3d2be7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: f79784b6498f080b15f1ef370e8a3f31be81a871
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823303"
---
# <a name="connecting-to-sql-server-mysqltosql"></a>SQL Server에 연결(MySQLToSQL)
MySQL 데이터베이스를 SQL Server로 마이그레이션하려면 SQL Server의 대상 인스턴스에 연결 해야 합니다. 연결할 때 SSMA는 SQL Server 인스턴스의 모든 데이터베이스에 대 한 메타 데이터를 가져오고 SQL Server 메타 데이터 탐색기에 데이터베이스 메타 데이터를 표시 합니다. SSMA는 연결 된 SQL Server의 인스턴스에 대 한 정보를 저장 하지만 암호를 저장 하지는 않습니다.  
  
SQL Server에 대 한 연결은 프로젝트를 닫을 때까지 활성 상태로 유지 됩니다. 프로젝트를 다시 열 때 서버에 대 한 활성 연결을 원하는 경우 SQL Server에 다시 연결 해야 합니다. 데이터베이스 개체를 SQL Server로 로드 하 고 데이터를 마이그레이션할 때까지 오프 라인으로 작업할 수 있습니다.  
  
SQL Server 인스턴스에 대 한 메타 데이터는 자동으로 동기화 되지 않습니다. 대신 메타 데이터 탐색기 SQL Server에서 메타 데이터를 업데이트 하려면 SQL Server 메타 데이터를 수동으로 업데이트 해야 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 "SQL Server 메타 데이터 동기화" 섹션을 참조 하십시오.  
  
## <a name="required-sql-server-permissions"></a>필요한 SQL Server 권한  
SQL Server에 연결 하는 데 사용 되는 계정에는 해당 계정에서 수행 하는 작업에 따라 다른 사용 권한이 필요 합니다.  
  
-   MySQL 개체를 구문으로 변환 [!INCLUDE[tsql](../../includes/tsql-md.md)] 하거나, SQL Server에서 메타 데이터를 업데이트 하거나, 변환 된 구문을 스크립트로 저장 하려면 계정에 SQL Server 인스턴스에 로그온 할 수 있는 권한이 있어야 합니다.  
  
-   데이터베이스 개체를 SQL Server 로드 하려면 최소 권한 요구 사항이 대상 데이터베이스에서 **db_owner** 데이터베이스 역할의 멤버 자격 이어야 합니다.  
  
## <a name="establishing-a-sql-server-connection"></a>SQL Server 연결 설정  
MySQL 데이터베이스 개체를 SQL Server 구문으로 변환 하기 전에 MySQL 데이터베이스를 마이그레이션할 SQL Server의 인스턴스에 대 한 연결을 설정 해야 합니다.  
  
연결 속성을 정의 하는 경우 개체 및 데이터가 마이그레이션되는 데이터베이스도 지정 합니다. SQL Server에 연결한 후 MySQL 스키마 수준에서이 매핑을 사용자 지정할 수 있습니다. 자세한 내용은 [SQL Server 스키마에 MySQL 데이터베이스 매핑 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md) 을 참조 하십시오.  
  
> [!IMPORTANT]  
> SQL Server에 연결 하기 전에 SQL Server 인스턴스가 실행 되 고 있는지 확인 하 고 연결을 허용할 수 있는지 확인 하십시오.  
  
**SQL Server에 연결하려면**  
  
1.  **파일** 메뉴에서 **SQL Server에 연결** 을 선택 합니다 .이 옵션은 프로젝트를 만든 후에 사용할 수 있습니다.  
  
    이전에 SQL Server에 연결한 경우 명령 이름이 **SQL Server에 다시 연결**됩니다.  
  
2.  연결 대화 상자에서 SQL Server 인스턴스의 이름을 입력 하거나 선택 합니다.  
  
    -   로컬 컴퓨터의 기본 인스턴스에 연결 하는 경우 **localhost** 또는 점 (**.**)을 입력할 수 있습니다.  
  
    -   다른 컴퓨터의 기본 인스턴스에 연결 하는 경우 컴퓨터 이름을 입력 합니다.  
  
    -   다른 컴퓨터의 명명 된 인스턴스에 연결 하는 경우 컴퓨터 이름, 백슬래시 및 인스턴스 이름 (예: MyServer\MyInstance.)을 차례로 입력 합니다.  
  
3.  SQL Server 인스턴스가 기본 포트가 아닌 포트에서 연결을 허용 하도록 구성 된 경우 **서버 포트** 상자에서 SQL Server 연결에 사용 되는 포트 번호를 입력 합니다. SQL Server 기본 인스턴스의 경우 기본 포트 번호는 1433입니다. 명명 된 인스턴스의 경우 SSMA는 SQL Server Browser 서비스에서 포트 번호를 가져오려고 시도 합니다.  
  
4.  **인증** 상자에서 연결에 사용할 인증 유형을 선택 합니다. 현재 Windows 계정을 사용 하려면 **Windows 인증**을 선택 합니다. SQL Server 로그인을 사용 하려면 SQL Server 인증을 선택 하 고 로그인 이름 및 암호를 입력 합니다.  
  
5.  보안 연결의 경우 **연결 암호화** 및 **trustservercertificate** 확인란의 두 컨트롤이 추가 됩니다. **연결 암호화** 를 선택 하는 경우에만 **trustservercertificate** 확인란이 표시 됩니다. **연결 암호화** 가 확인 되 고 (True) **trustservercertificate** 가 선택 취소 (FALSE) 되 면 SSL 인증서 SQL Server 유효성을 검사 합니다. 서버 인증서의 유효성 검사는 SSL 핸드셰이크의 일부로 서버가 연결할 올바른 서버인지 확인합니다. 이를 위해 클라이언트 쪽 뿐만 아니라 서버 쪽에도 인증서를 설치 해야 합니다.  
  
6.  연결을 클릭합니다.  
  
**높은 버전 호환성**  
  
더 높은 버전의 SQL Server에 연결 하거나 다시 연결할 수 있습니다.  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 만든 프로젝트가 2005 인 경우 2008 또는 2012 또는 2014 또는 2016에 연결할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 만든 프로젝트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 이지만 더 낮은 버전 (예: 2005)에 연결할 수 없는 경우에는 2012 또는 2014 또는 2016에 연결할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 만든 프로젝트가 2012 인 경우 2012 또는 2014 또는 2016에 연결할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 만든 프로젝트가 2014 인 경우에는 2014 또는 2016에만 연결할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
5.  "SQL Azure"에 대 한 버전 호환성이 더 이상 유효 하지 않습니다.  
  
|프로젝트 형식 및 대상 서버 버전|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (버전: 4.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (버전: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012<br />(버전: 11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014<br />(버전: 12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016<br />(버전: 13.x)|SQL Azure|  
|-|-|-|-|-|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|예|예|예|예|예||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||예|예|예|예||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||예|예|예||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||예|예||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016|||||예||  
|SQL Azure||||||예|  
  
> [!IMPORTANT]  
> 데이터베이스 개체의 변환은 프로젝트 형식에 따라 수행 되지만에 연결 된의 버전에 따라 수행 되지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 프로젝트의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 더 높은 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016)에 연결 된 경우에도 2005 당 변환이 수행 됩니다.  
  
## <a name="synchronizing-sql-server-metadata"></a>SQL Server 메타 데이터 동기화  
SQL Server 데이터베이스에 대 한 메타 데이터는 자동으로 업데이트 되지 않습니다. SQL Server 메타 데이터 탐색기의 메타 데이터는 SQL Server에 처음 연결 하거나 마지막으로 메타 데이터를 마지막으로 업데이트 한 경우 메타 데이터의 스냅숏입니다. 모든 데이터베이스 또는 단일 데이터베이스 또는 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 동기화 하려면**  
  
1.  SQL Server에 연결 되어 있는지 확인 합니다.  
  
2.  메타 데이터 탐색기 SQL Server 업데이트 하려는 데이터베이스 또는 데이터베이스 스키마 옆의 확인란을 선택 합니다.  
  
    예를 들어 모든 데이터베이스에 대 한 메타 데이터를 업데이트 하려면 데이터베이스 옆의 상자를 선택 합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭 하거나 개별 데이터베이스 또는 데이터베이스 스키마를 클릭 한 다음 **데이터베이스와 동기화**를 선택 합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션의 다음 단계는 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   MySQL 스키마와 SQL Server 데이터베이스 및 스키마 간의 매핑을 사용자 지정 하려면 [SQL Server 스키마에 Mysql 데이터베이스 매핑 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md) 을 참조 하세요.  
  
-   프로젝트에 대 한 구성 옵션을 사용자 지정 하려면 [&#40;MySQLToSQL&#41;프로젝트 옵션 설정](../../ssma/mysql/setting-project-options-mysqltosql.md) 을 참조 하세요.  
  
-   원본 및 대상 데이터 형식의 매핑을 사용자 지정 하려면 [MySQL 및 SQL Server 데이터 형식 &#40;MySQLToSQL에 매핑](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md) 을 참조 하세요&#41;  
  
-   이러한 작업을 수행할 필요가 없는 경우 MySQL 데이터베이스 개체 정의를 SQL Server 개체 정의로 변환할 수 있습니다. 자세한 내용은 [&#40;MySQLToSQL&#41;MySQL 데이터베이스 변환](../../ssma/mysql/converting-mysql-databases-mysqltosql.md) (영문)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
[MySQL 데이터베이스를 SQL Server-Azure SQL Database &#40;MySQLToSql&#41;로 마이그레이션](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

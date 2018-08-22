---
title: Sybase ASE (SybaseToSQL)에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connecting to Sybase ASE
ms.assetid: a45a2330-9175-4c9e-af38-ef920e350614
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a8411cdb507b27e69f86f0d853e1c98b4d24d29a
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40396009"
---
# <a name="connecting-to-sybase-ase-sybasetosql"></a>Sybase ASE에 연결(SybaseToSQL)
Sybase 적응형 Server Enterprise (ASE) 데이터베이스를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션하려는 데이터베이스를 포함 하는 적응형 서버에 연결 해야 SQL Azure 또는 합니다. 에 연결 하면 SSMA 적응 서버의 모든 데이터베이스에 대 한 메타 데이터를 가져오고 Sybase 메타 데이터 탐색기 창에서 데이터베이스 메타 데이터를 표시 합니다. SSMA는 데이터베이스 서버에 대 한 정보를 저장 하지만 암호를 저장 하지 않습니다.  
  
ASE에 대 한 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 열면 다시 연결 해야 ASE에 활성 서버에 연결 하려는 경우.  
  
적응 서버에 대 한 메타 데이터를 자동으로 업데이트 되지 않습니다. 대신, Sybase 메타 데이터 탐색기에서 메타 데이터를 업데이트 하려는 경우 수동으로 업데이트 해야 메타 데이터를이 항목의 뒷부분에 나오는 "Sybase ASE 메타 데이터 새로 고침" 섹션에 설명 된 대로 합니다.  
  
## <a name="required-ase-permissions"></a>필요한 ASE 사용 권한  
ASE에 연결 하는 데 사용 되는 계정을 하나 이상 있어야 합니다 **공개** 로 마이그레이션할 원본 데이터베이스 및 master 데이터베이스에 대 한 액세스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다. 또한 마이그레이션되는 테이블에 대 한 권한을 선택 하려면 사용자 SELECT 권한이 있어야 다음 시스템 테이블에서:  
  
-   [source_db].dbo.sysobjects  
  
-   [source_db].dbo.syscolumns  
  
-   [source_db].dbo.sysusers  
  
-   [source_db].dbo.systypes  
  
-   [source_db].dbo.sysconstraints  
  
-   [source_db].dbo.syscomments  
  
-   [source_db].dbo.sysindexes  
  
-   [source_db].dbo.sysreferences  
  
-   master.dbo.sysdatabases  
  
## <a name="establishing-a-connection-to-ase"></a>ASE에 연결  
적응 하는 서버에 연결할 때 SSMA는 데이터베이스 서버에서 데이터베이스 메타 데이터를 읽고 프로젝트 파일에이 메타 데이터를 추가 합니다. 개체를 변환 하는 경우이 메타 데이터 SSMA 사용한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 구문이 데이터를 마이그레이션한 경우 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다. Sybase 메타 데이터 탐색기 창에서이 메타 데이터를 찾아보고 개별 데이터베이스 개체의 속성을 검토할 수 있습니다.  
  
> [!IMPORTANT]  
> 데이터베이스 서버에 연결 하려고 하기 전에 데이터베이스 서버가 실행 되 고 연결을 허용할 수 있는지 확인 합니다.  
  
**Sybase ASE에 연결**  
  
1.  에 **파일** 메뉴에서 **Sybase에 연결**합니다.  
  
    이전에 Sybase에 연결 하는 경우 명령 이름 됩니다 **Sybase에 다시 연결**합니다.  
  
2.  에 **공급자** 상자, Sybase 서버에 연결할 컴퓨터에 설치 된 공급자 중 하나를 선택 합니다.  
  
3.  에 **모드** 상자에서 선택 하거나 **표준 모드** 또는 **고급 모드**합니다.  
  
    서버 이름, 포트, 사용자 이름 및 암호를 지정 하려면 표준 모드를 사용 합니다. 고급 모드를 사용 하 여 연결 문자열을 제공 합니다. 이 모드는 일반적으로 문제를 해결 하거나 기술 지원과 함께에 사용 됩니다.  
  
4.  선택 하는 경우 **표준 모드**, 다음 값을 제공 합니다.  
  
    1.  에 **서버 이름** 상자에 입력 하거나 이름 또는 데이터베이스 서버의 IP 주소를 선택 합니다.  
  
    2.  데이터베이스 서버에 연결을 허용 하도록 구성 되지 않은 경우 기본 포트 (5000),이 Sybase 연결에 사용 되는 포트 번호를 입력 하는 합니다 **서버 포트** 상자입니다.  
  
    3.  에 **사용자 이름** 상자에 필요한 권한이 있는 Sybase 계정을 입력 합니다.  
  
    4.  에 **암호** 상자에 지정된 된 사용자 이름에 대 한 암호를 입력 합니다.  
  
5.  선택 하는 경우 **고급 모드**에서 연결 문자열을 제공 합니다 **연결 문자열** 상자입니다.  
  
    다른 연결 문자열의 예는 다음과 같습니다.  
  
    1.  **Sybase OLE DB 공급자에 대 한 연결 문자열:**  
  
        Sybase ASE OLE DB 12.5에 대 한 연결 문자열의 예는 다음과 같습니다.  
  
        `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
        Sybase ASE OLE DB 15 일에 대 한 연결 문자열의 예는 다음과 같습니다.  
  
        `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider= ASEOLEDB;Port=5000;`  
  
    2.  **Sybase ODBC 공급자에 대 한 연결 문자열:**  
  
        `Driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
    3.  **Sybase ADO.NET 공급자에 대 한 연결 문자열:**  
  
        `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
    자세한 내용은 [Sybase에 연결 &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)합니다.  
  
## <a name="reconnecting-to-sybase-ase"></a>Sybase ASE에 다시 연결  
데이터베이스 서버에 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 열면 적응 서버로 활성 연결 하려는 경우 다시 연결 해야 합니다. 메타 데이터 업데이트를 데이터베이스 개체에 로드 될 때까지 오프 라인으로 작업할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터를 마이그레이션합니다.  
  
## <a name="refreshing-sybase-ase-metadata"></a>Sybase ASE 메타 데이터를 새로 고치는 중  
ASE 데이터베이스에 대 한 메타 데이터는 자동으로 새로 고쳐지지 않습니다. Sybase 메타 데이터 탐색기에서 메타 데이터는 적응 서버나 수동으로 메타 데이터를 새로 고칠는 마지막 시간에 처음 연결할 때 메타 데이터의 스냅숏입니다. 단일 데이터베이스를 단일 데이터베이스 스키마 또는 모든 데이터베이스에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 새로 고치려면**  
  
1.  적응 서버에 연결 되어 있는지 확인 합니다.  
  
2.  Sybase 메타 데이터 탐색기에서 데이터베이스 또는 데이터베이스 스키마를 업데이트 하려는 옆의 확인란을 선택 합니다.  
  
3.  데이터베이스 또는 개별 데이터베이스 또는 데이터베이스 스키마를 마우스 오른쪽 단추로 클릭 하 고 선택한 **데이터베이스에서 새로 고침**합니다.  
  
4.  현재 개체를 확인 하는 메시지가 누릅니다 **예**합니다.  
  
## <a name="next-step"></a>다음 단계  
  
-   마이그레이션 프로세스에서 다음 단계 [SQL Server 인스턴스에 연결할](connecting-to-sql-server-sybasetosql.md) / [SQL Azure 인스턴스에 연결 합니다.](connecting-to-azure-sql-db-sybasetosql.md)  
  
## <a name="see-also"></a>관련 항목  
[Sybase ASE 데이터베이스를 SQL Server-Azure SQL DB로 마이그레이션 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

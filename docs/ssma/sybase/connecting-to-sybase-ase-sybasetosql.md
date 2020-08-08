---
title: SAP ASE에 연결 (SybaseToSQL) | Microsoft Docs
description: 적응 서버에 연결 하 여 SAP 적응 서버 엔터프라이즈 (ASE) 데이터베이스를 SQL Server 또는 Azure SQL Database 마이그레이션하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to Sybase
ms.assetid: a45a2330-9175-4c9e-af38-ef920e350614
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 2583ef86a84158e0398265799f90633de8c76d7f
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87932364"
---
# <a name="connecting-to-sap-ase-sybasetosql"></a>SAP ASE에 연결 (SybaseToSQL)

SAP 적응 서버 엔터프라이즈 (ASE) 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 마이그레이션하려면 마이그레이션할 데이터베이스가 포함 된 적응 서버에 연결 해야 합니다. 연결할 때 SSMA는 적응 서버에 있는 모든 데이터베이스에 대 한 메타 데이터를 가져오고 Sybase 메타 데이터 탐색기 창에 데이터베이스 메타 데이터를 표시 합니다. SSMA는 데이터베이스 서버에 대 한 정보를 저장 하지만 암호를 저장 하지는 않습니다.  
  
ASE에 대 한 연결은 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 다시 열 때 서버에 대 한 활성 연결을 원하는 경우 ASE에 다시 연결 해야 합니다.  
  
적응 서버에 대 한 메타 데이터는 자동으로 업데이트 되지 않습니다. 대신, Sybase 메타 데이터 탐색기에서 메타 데이터를 업데이트 하려는 경우이 항목의 뒷부분에 나오는 "Sybase ASE 메타 데이터 새로 고침" 섹션에 설명 된 대로 메타 데이터를 수동으로 업데이트 해야 합니다.  
  
## <a name="required-ase-permissions"></a>필수 ASE 권한

ASE에 연결 하는 데 사용 되는 계정에는 적어도 master 데이터베이스 및 모든 원본 데이터베이스에 대 한 **공용** 액세스 권한 (또는 SQL Azure)이 있어야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 또한 마이그레이션되는 테이블에 대 한 사용 권한을 선택 하려면 사용자에 게 다음 시스템 테이블에 대 한 SELECT 권한이 있어야 합니다.  
  
- [source_db] .dbo.sys개체  
- [source_db] .dbo.sys열  
- [source_db] .dbo.sys사용자  
- [source_db] .dbo.sys유형  
- [source_db] .dbo.sys제약 조건  
- [source_db] .dbo.sys주석  
- [source_db] .dbo.sys인덱스  
- [source_db] .dbo.sys참조  
- master.dbo.sys데이터베이스  
  
## <a name="establishing-a-connection-to-ase"></a>ASE에 대 한 연결 설정

적응 서버에 연결할 때 SSMA는 데이터베이스 서버에서 데이터베이스 메타 데이터를 읽은 다음이 메타 데이터를 프로젝트 파일에 추가 합니다. 이 메타 데이터는 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 구문으로 변환 하 고, 데이터를 또는 SQL Azure로 마이그레이션할 때 SSMA에서 사용 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sybase 메타 데이터 탐색기 창에서이 메타 데이터를 찾아보고 개별 데이터베이스 개체의 속성을 검토할 수 있습니다.  
  
> [!IMPORTANT]  
> 데이터베이스 서버에 연결을 시도 하기 전에 데이터베이스 서버가 실행 중이 고 연결을 허용할 수 있는지 확인 합니다.  
  
**Sybase ASE에 연결 하려면**
  
1. **파일** 메뉴에서 **Sybase에 연결**을 선택 합니다.  
  
   이전에 Sybase에 연결한 경우 명령 이름이 **sybase에 다시 연결**됩니다.  
  
2. **공급자** 상자에서 Sybase 서버에 연결할 컴퓨터의 설치 된 공급자를 선택 합니다.  
  
3. **모드** 상자에서 **표준 모드** 또는 **고급 모드**를 선택 합니다.  
  
   표준 모드를 사용 하 여 서버 이름, 포트, 사용자 이름 및 암호를 지정 합니다. 고급 모드를 사용 하 여 연결 문자열을 제공 합니다. 이 모드는 일반적으로 문제 해결 또는 기술 지원 사용에만 사용 됩니다.  
  
4. **표준 모드**를 선택 하는 경우 다음 값을 제공 합니다.  
  
    1. **서버 이름** 상자에서 데이터베이스 서버의 이름 또는 IP 주소를 입력 하거나 선택 합니다.  
    2. 데이터베이스 서버가 기본 포트 (5000)의 연결을 허용 하도록 구성 되지 않은 경우 **서버 포트** 상자에서 Sybase 연결에 사용 되는 포트 번호를 입력 합니다.  
    3. **사용자 이름** 상자에 필요한 사용 권한이 있는 Sybase 계정을 입력 합니다.  
    4. **암호** 상자에 지정 된 사용자 이름의 암호를 입력 합니다.  
  
5. **고급 모드**를 선택 하는 경우 **연결 문자열** 상자에 연결 문자열을 입력 합니다.  
  
    서로 다른 연결 문자열의 예는 다음과 같습니다.  
  
    1. **Sybase OLE DB 공급자에 대 한 연결 문자열:**  
  
        Sybase ASE OLE DB 12.5의 경우 연결 문자열의 예는 다음과 같습니다.  
  
        `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
        Sybase ASE OLE DB 15의 경우 연결 문자열의 예는 다음과 같습니다.  
  
        `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider= ASEOLEDB;Port=5000;`  
  
    2. **Sybase ODBC 공급자에 대 한 연결 문자열:**  
  
       `Driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
    3. **Sybase ADO.NET Provider에 대 한 연결 문자열:**  
  
       `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
    자세한 내용은 [Sybase &#40;SybaseToSQL&#41;에 연결 ](../../ssma/sybase/connect-to-sybase-sybasetosql.md)을 참조 하세요.  
  
## <a name="reconnecting-to-sybase-ase"></a>Sybase ASE에 다시 연결

데이터베이스 서버에 대 한 연결은 프로젝트를 닫을 때까지 활성 상태로 유지 됩니다. 프로젝트를 다시 열면 적응 서버에 대 한 활성 연결을 원하는 경우 다시 연결 해야 합니다. 메타 데이터를 업데이트 하 고, 데이터베이스 개체를 또는 SQL Azure으로 로드 하 고, 데이터를 마이그레이션할 때까지 오프 라인으로 작업할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="refreshing-sybase-ase-metadata"></a>Sybase ASE 메타 데이터를 새로 고치는 중

ASE 데이터베이스에 대 한 메타 데이터는 자동으로 새로 고쳐지지 않습니다. Sybase 메타 데이터 탐색기의 메타 데이터는 적응 서버에 처음 연결할 때 또는 메타 데이터를 마지막으로 새로 고친 시간에 메타 데이터의 스냅숏입니다. 단일 데이터베이스, 단일 데이터베이스 스키마 또는 모든 데이터베이스에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 새로 고치려면**
  
1. 적응 서버에 연결 되어 있는지 확인 합니다.  
  
2. Sybase 메타 데이터 탐색기에서 업데이트 하려는 데이터베이스 또는 데이터베이스 스키마 옆의 확인란을 선택 합니다.  
  
3. 데이터베이스를 마우스 오른쪽 단추로 클릭 하거나 개별 데이터베이스 또는 데이터베이스 스키마를 클릭 한 다음 **데이터베이스에서 새로 고침**을 선택 합니다.  
  
4. 현재 개체를 확인 하는 메시지가 표시 되 면 **예**를 클릭 합니다.  
  
## <a name="next-step"></a>다음 단계  
  
- 마이그레이션 프로세스의 다음 단계는 인스턴스에 연결 하 [SQL Server 인스턴스에 연결](connecting-to-sql-server-sybasetosql.md)하는 것  /  [SQL Azure](connecting-to-azure-sql-db-sybasetosql.md)  
  
## <a name="see-also"></a>참고 항목

[Sybase ASE 데이터베이스를 SQL Server-Azure SQL Database &#40;SybaseToSQL&#41;로 마이그레이션](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  

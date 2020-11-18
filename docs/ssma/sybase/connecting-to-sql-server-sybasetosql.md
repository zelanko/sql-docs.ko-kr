---
description: SQL Server에 연결(SybaseToSQL)
title: SQL Server에 연결 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server
ms.assetid: dd368a1a-45b0-40e9-b4d3-5cdb48c26606
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 2988f57c5d0e3162c9b6dc54d8a7371efcf5da05
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870423"
---
# <a name="connecting-to-sql-server-sybasetosql"></a>SQL Server에 연결(SybaseToSQL)

Sybase 서버 ASE (적응 서버 엔터프라이즈) 데이터베이스를로 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 대상 인스턴스에 연결 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 연결할 때 SSMA는 인스턴스의 모든 데이터베이스에 대 한 메타 데이터를 가져오고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL Server 메타 데이터 탐색기** 에 데이터베이스 메타 데이터를 표시 합니다. SSMA는 연결 된 인스턴스에 대 한 정보 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 저장 하지만 암호를 저장 하지는 않습니다.

사용자의 연결은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로젝트를 닫을 때까지 활성 상태로 유지 됩니다. 프로젝트를 다시 열 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버에 대 한 활성 연결을 원하는 경우에 다시 연결 해야 합니다. 데이터베이스 개체를 로드 하 고 데이터를 마이그레이션할 때까지 오프 라인으로 작업할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

인스턴스에 대 한 메타 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 자동으로 동기화 되지 않습니다. 대신 **SQL Server Metadata Explorer** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 항목의 뒷부분에 있는 "SQL Server 메타 데이터 동기화" 단원에 설명 된 대로 메타 데이터를 SQL Server 업데이트 하 여 메타 데이터를 수동으로 업데이트 해야 합니다.

## <a name="required-sql-server-permissions"></a>필요한 SQL Server 권한

에 연결 하는 데 사용 되는 계정에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 해당 계정에서 수행 하는 작업에 따라 다른 사용 권한이 필요 합니다.

- ASE 개체를 구문으로 변환 [!INCLUDE[tsql](../../includes/tsql-md.md)] 하거나에서 메타 데이터를 업데이트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하거나 변환 된 구문을 스크립트에 저장 하려면 계정에 인스턴스에 로그온 할 수 있는 권한이 있어야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

- 데이터베이스 개체를에 로드 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정이 **db_ddladmin** 데이터베이스 역할의 멤버 여야 합니다.

- 로 데이터를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정이 다음과 같아야 합니다.
  - 클라이언트 쪽 데이터 마이그레이션 엔진을 사용 하는 경우 **db_owner** 데이터베이스 역할의 멤버입니다.
  - 서버 쪽 데이터 마이그레이션 엔진을 사용 하는 경우 **sysadmin** 서버 역할의 멤버입니다. `CmdExec` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이그레이션 중에 에이전트 작업 단계를 만들어 ssma 대량 복사 도구를 실행 하는 데 필요 합니다.
    > [!NOTE]
    > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버 쪽 데이터 마이그레이션은 에이전트 프록시 계정을 지원 하지 않습니다.

- SSMA에 의해 생성 된 코드를 실행 하려면 계정에 `EXECUTE` 대상 데이터베이스의 **ssma_syb** 스키마에 있는 모든 사용자 정의 함수에 대 한 권한이 있어야 합니다. 이러한 함수는 ASE 시스템 함수에 해당 하는 기능을 제공 하며 변환 된 개체에 사용 됩니다.

## <a name="establishing-a-sql-server-connection"></a>SQL Server 연결 설정

ASE 데이터베이스 개체를 구문으로 변환 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ase 데이터베이스를 마이그레이션하려는 인스턴스에 대 한 연결을 설정 해야 합니다.

연결 속성을 정의 하는 경우 개체 및 데이터가 마이그레이션되는 데이터베이스도 지정 합니다. 에 연결한 후 ASE 스키마 수준에서이 매핑을 사용자 지정할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 자세한 내용은 [SQL Server 스키마에 SYBASE ASE 스키마 매핑 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)을 참조 하세요.

> [!IMPORTANT]
> 에 연결을 시도 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 중이 고 연결을 허용할 수 있는지 확인 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하려면
  
1. **파일** 메뉴에서 **SQL Server에 연결** 을 선택 합니다.
   이전에에 연결한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 명령 이름이 **SQL Server에 다시 연결** 됩니다.

2. 연결 대화 상자에서 인스턴스의 이름을 입력 하거나 선택 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
   - 로컬 컴퓨터의 기본 인스턴스에 연결 하는 경우 `localhost` 또는 점 ()을 입력할 수 있습니다 `.` .
   - 다른 컴퓨터의 기본 인스턴스에 연결 하는 경우 컴퓨터 이름을 입력 합니다.
   - 다른 컴퓨터의 명명 된 인스턴스에 연결 하는 경우 컴퓨터 이름, 백슬래시 및 인스턴스 이름 (예:)을 차례로 입력 합니다 `MyServer\MyInstance` .

3. 인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본이 아닌 포트에서 연결을 허용 하도록 구성 된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **서버 포트** 상자에서 연결에 사용 되는 포트 번호를 입력 합니다. 기본 인스턴스의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 포트 번호는 1433입니다. 명명 된 인스턴스의 경우 SSMA는 Browser 서비스에서 포트 번호를 가져오려고 시도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.

4. **데이터베이스** 상자에 대상 데이터베이스의 이름을 입력 합니다.
   에 다시 연결 하는 경우에는이 옵션을 사용할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

5. **인증** 상자에서 연결에 사용할 인증 유형을 선택 합니다. 현재 Windows 계정을 사용 하려면 **Windows 인증** 을 선택 합니다. 로그인을 사용 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL Server 인증** 을 선택 하 고 로그인 이름 및 암호를 제공 합니다.

6. 보안 연결의 경우 **연결 암호화** 및 **trustservercertificate** 확인란의 두 컨트롤이 추가 됩니다. **연결 암호화** 를 선택 하는 경우에만 **trustservercertificate** 확인란이 표시 됩니다. **연결 암호화** 가 선택 되 고 (True) **trustservercertificate** 가 선택 취소 (false) 되 면 SSL 인증서의 유효성을 검사 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 서버 인증서의 유효성 검사는 SSL 핸드셰이크의 일부로 서버가 연결할 올바른 서버인지 확인합니다. 이를 위해 클라이언트 쪽 뿐만 아니라 서버 쪽에도 인증서를 설치 해야 합니다.

7. **연결** 을 클릭합니다.

> [!IMPORTANT]
> 마이그레이션 프로젝트를 만들 때 선택한 버전과 비교 하 여 더 높은 버전의에 연결할 수 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체의 변환은 연결 된의 버전이 아니라 프로젝트의 대상 버전에 의해 결정 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

## <a name="reconnecting-to-sql-server"></a>SQL Server에 다시 연결

사용자의 연결은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로젝트를 닫을 때까지 활성 상태로 유지 됩니다. 프로젝트를 다시 열 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버에 대 한 활성 연결을 원하는 경우에 다시 연결 해야 합니다. 메타 데이터를 업데이트 하 고, 데이터베이스 개체를에 로드 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고, 데이터를 마이그레이션할 때까지 오프 라인으로 작업할 수 있습니다.

에 다시 연결 하는 절차는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결을 설정 하는 절차와 같습니다.

## <a name="synchronizing-sql-server-metadata"></a>SQL Server 메타 데이터 동기화

데이터베이스에 대 한 메타 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 자동으로 업데이트 되지 않습니다. 메타 데이터 **탐색기 SQL Server** 의 메타 데이터는 처음 연결 될 때 메타 데이터의 스냅숏입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 또는 메타 데이터를 마지막으로 업데이트 한 시간입니다. 모든 데이터베이스 또는 단일 데이터베이스 또는 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다. 메타 데이터를 동기화 하려면:

1. 에 연결 되어 있는지 확인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.

2. **메타 데이터 탐색기 SQL Server** 업데이트 하려는 데이터베이스 또는 데이터베이스 스키마 옆의 확인란을 선택 합니다.
   예를 들어 모든 데이터베이스에 대 한 메타 데이터를 업데이트 하려면 **데이터베이스** 옆의 상자를 선택 합니다.

3. 데이터베이스를 마우스 오른쪽 **단추로 클릭 하거나** 개별 데이터베이스 또는 데이터베이스 스키마를 클릭 한 다음 **데이터베이스와 동기화** 를 선택 합니다.

## <a name="next-step"></a>다음 단계

마이그레이션의 다음 단계는 프로젝트 요구 사항에 따라 달라 집니다.

- ASE 데이터베이스와 스키마 및 데이터베이스와 스키마 간의 매핑을 사용자 지정 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQL Server 스키마에 Sybase ASE 스키마 매핑 &#40;SybaseToSQL&#41;을 ](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)참조 하세요.
- 프로젝트에 대 한 구성 옵션을 사용자 지정 하려면 [프로젝트 옵션 설정 &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)을 참조 하세요.
- 원본 및 대상 데이터 형식의 매핑을 사용자 지정 하려면 [SYBASE ASE 및 SQL Server 데이터 형식 매핑 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)을 참조 하세요.
- 이러한 작업을 수행할 필요가 없는 경우 Sybase ASE 데이터베이스 개체 정의를 개체 정의로 변환할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 자세한 내용은 [SYBASE ASE 데이터베이스 개체 변환 &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)을 참조 하세요.

## <a name="see-also"></a>참고 항목

[Sybase ASE 데이터베이스를 SQL Server-Azure SQL Database &#40;SybaseToSQL&#41;로 마이그레이션 ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)

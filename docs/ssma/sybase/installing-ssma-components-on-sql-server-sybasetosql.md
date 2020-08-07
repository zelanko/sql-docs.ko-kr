---
title: SQL Server에 SSMA 구성 요소 설치 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1c66255f57a69db0807ab1620cafd60444f296c8
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87865391"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>SQL Server에 SSMA 구성 요소 설치 (SybaseToSQL)

SSMA를 설치 하는 것 외에도 서버 쪽 데이터 마이그레이션을 사용 하기 위해를 실행 하는 컴퓨터에 구성 요소를 설치 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이러한 구성 요소에는 데이터 마이그레이션을 지 원하는 SSMA 확장 팩과 서버 간 연결을 설정 하는 Sybase 공급자가 포함 됩니다.

## <a name="ssma-for-sybase-extension-pack"></a>Sybase 확장 팩용 SSMA

SSMA 확장 팩은 지정 된 인스턴스에 **sysdb** 및 **ssmatesterdb_syb**데이터베이스를 추가 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **Sysdb** 데이터베이스에는 데이터를 마이그레이션하는 데 필요한 테이블과 저장 프로시저가 포함 되어 있습니다. **Ssmatester_syb** 데이터베이스에는 ssma 테스터 구성 요소에서 사용 하는 개체 (테이블, 트리거, 뷰)가 생성 되는 스키마 **ssma_sybase_utilities**포함 되어 있습니다.

또한 데이터를로 마이그레이션하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ssma는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이그레이션에 서버 쪽 데이터 마이그레이션 엔진을 사용 하는 경우 에이전트 작업을 만듭니다.

### <a name="prerequisites"></a>필수 구성 요소

Sybase 용 SSMA 서버 구성 요소를 설치 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템이 다음과 같은 요구 사항을 충족 하는지 확인 합니다.

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스가 설치 되었습니다.
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 이상 버전
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.7.2 이상 버전입니다. [.NET Framework 개발자 센터](https://go.microsoft.com/fwlink/?LinkId=48882)에서 가져올 수 있습니다.
- Sybase OLE DB/ADO.Net/ODBC 공급자 및 마이그레이션할 데이터베이스가 포함 된 SAP ASE 데이터베이스 서버에 대 한 연결입니다. SAP ASE 제품 미디어에서 공급자를 설치할 수 있습니다. 연결에 대 한 자세한 내용은 [SYBASE ASE &#40;SybaseToSQL&#41;에 연결을 ](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)참조 하세요.
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치 하는 동안 Browser 서비스를 실행 해야 합니다. 이는 설치 마법사에서 인스턴스 목록을 채우는 데 사용 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 설치 후 Browser 서비스를 사용 하지 않도록 설정할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

  > [!NOTE]
  > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser 서비스가 실행 되 고 있지만 설치 프로그램에 인스턴스 목록이 표시 되지 않는 경우 UDP 포트 1434을 차단 해제 해야 합니다. Windows 방화벽을 사용 하 여 일시적으로 포트 차단을 해제 하거나 Windows 방화벽을 일시적으로 사용 하지 않도록 설정할 수 있습니다. 바이러스 백신 소프트웨어를 일시적으로 사용 하지 않도록 설정 해야 할 수도 있습니다. 설치 후 방화벽 및 바이러스 백신 소프트웨어를 사용 하도록 설정 해야 합니다.

### <a name="installing-the-extension-pack"></a>확장 팩 설치

에 데이터를 마이그레이션하기 전에 언제 든 지 확장 팩을 설치할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

> [!IMPORTANT]
> 확장 팩을 설치 하려면 인스턴스에서 sysadmin 서버 역할의 멤버 여야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

확장 팩을 설치 하려면:

1. **SSMAforSybaseExtensionPack_*n*.msi**를 복사 합니다. 여기서 *n* 은 빌드 번호 이며를 실행 하는 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 있습니다.
2. **SSMAforSybaseExtensionPack_*n*.msi**를 두 번 클릭 합니다.
3. **Welcome** 페이지에서 **다음**을 클릭합니다.
4. **최종 사용자 사용권 계약** 페이지에서 사용권 계약을 읽습니다. 동의 **하면 동의 함 옵션을** 선택 하 고 **다음**을 클릭 합니다.
5. **설치 유형 선택** 페이지에서 **일반**을 클릭 합니다.
6. **설치할 준비가 되었습니다** 페이지에서 **설치**를 클릭합니다.
7. **설치의 첫 번째 단계를 완료 했습니다** . 페이지에서 **다음**을 클릭 합니다.

   새 대화 상자가 표시 되 고 확장 팩을 설치할 인스턴스를 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.

8. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SAP ASE 데이터베이스를 마이그레이션하려는 인스턴스를 선택 하 고 **다음**을 클릭 합니다.

   기본 인스턴스의 이름은 컴퓨터와 동일 합니다. 명명 된 인스턴스에는 백슬래시와 인스턴스 이름이 나옵니다.

9. 연결 페이지에서 인증 방법을 선택 하 고 **다음**을 클릭 합니다.

   Windows 인증에서는 Windows 자격 증명을 사용 하 여 인스턴스에 로그온을 시도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 서버 인증을 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 이름 및 암호를 입력 해야 합니다.

10. 다음 단계에서는 서버 쪽 데이터를 마이그레이션하는 동안 확장 팩 데이터베이스에 저장 된 중요 한 데이터를 암호화 하는 데 사용 되는 마스터 키에 대 한 암호를 설정 해야 합니다. 강력한 암호를 입력 하 고 **다음**을 클릭 합니다.

11. 다음 페이지에서 **유틸리티 데이터베이스 *n* 설치를 선택 하 고 확장 팩 라이브러리를 설치**합니다. 여기서 *n* 은 버전 번호입니다. 테스터 기능을 사용 하려는 경우 **테스터 데이터베이스 설치** 확인란을 선택 하 고 **다음**을 선택 합니다.

    이 데이터베이스에는 데이터 마이그레이션에 필요한 테이블 및 저장 프로시저 (서버 쪽 데이터 마이그레이션 엔진 사용)를 사용 하 여 **sysdb** 데이터베이스가 만들어집니다.

    **테스터 데이터베이스 설치** 옵션을 선택 하면 **ssmatesterdb_syb** 데이터베이스가 생성 됩니다.

12. 설치가 완료 되 면 다른 인스턴스에 유틸리티 데이터베이스를 설치할지 묻는 메시지가 표시 되 면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **예**를 선택 하 고 **다음**을 선택 하거나 마법사를 종료 하려면 **아니요** 를 선택한 다음 **끝내기**를 선택 합니다.

### <a name="sql-server-database-objects"></a>데이터베이스 개체 SQL Server

확장 팩을 설치한 후에는 **sysdb** 데이터베이스의 **ssma_syb bcp_migration_packages** 테이블이 표시 됩니다. 다음 저장 프로시저도 표시 됩니다.

- `bcp_clean_migration_data`
- `bcp_ensure_message_table`
- `bcp_insert_new_message`
- `bcp_post_process`
- `bcp_read_new_migration_messages`
- `bcp_save_migration_package`
- `bcp_smart_truncate`
- `bcp_start_migration_process`
- `get_jobstep_info`
- `stop_agent_process`

데이터를로 마이그레이션할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ssma는 에이전트 작업을 만듭니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이러한 작업에는 **데이터 마이그레이션 패키지 {GUID} ssma_syb**이름이 지정 되 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업 폴더의 에이전트 노드에 표시 됩니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  

## <a name="sybase-providers"></a>Sybase 공급자

서버 쪽 데이터 마이그레이션을 사용 하 여 SAP ASE에서로 데이터를 이동 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 경우 SAP ase와 간에 데이터가 직접 마이그레이션됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이는 데이터 마이그레이션의 속도가 느려지므로 SSMA를 통해 이동 하지 않습니다.

### <a name="installing-the-sybase-providers"></a>Sybase 공급자 설치

다음 지침은 Sybase 공급자를 설치 하는 기본 설치 단계를 제공 합니다. 정확한 지침은 Sybase 설치 프로그램의 버전에 따라 달라 집니다.

> [!IMPORTANT]
> 설치 프로그램을 실행 하기 전에 사용권 계약을 위반 하지 않는지 확인 합니다.

1. Sybase ASE 설치 프로그램을 실행 합니다.
2. 사용자 지정 설치를 선택 합니다.
3. 기능 선택 페이지에서 ODBC, OLE DB 및 ADO.NET 데이터 공급자를 선택 합니다.
4. 선택한 기능을 확인 한 다음 **마침** 을 클릭 하 여 데이터 공급자를 설치 합니다.

## <a name="see-also"></a>참고 항목

- [Sybase 클라이언트용 SSMA 설치](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)
- [Sybase ASE 데이터베이스를 SQL Server-Azure SQL Database로 마이그레이션](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)

---
title: 데이터베이스 즉시 파일 초기화
description: 인스턴트 파일 초기화 및 SQL Server 데이터베이스에서 이를 사용하도록 설정하는 방법을 알아봅니다.
ms.custom: contperfq4
ms.date: 05/30/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initialization [SQL Server]
- fast file initialization [SQL Server]
- file initialization [SQL Server]
- IFI [SQL Server]
- database instant file initialization [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
author: stevestein
ms.author: sstein
ms.openlocfilehash: a10e6f9cff886b18b8bc344270516aaf2b5577db
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756258"
---
# <a name="database-instant-file-initialization"></a>데이터베이스 즉시 파일 초기화
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
이 문서에서는 인스턴트 파일 초기화에 대해 살펴보고 이를 사용하도록 설정하여 SQL Server 데이터베이스 파일 증가를 가속화하는 방법을 알아봅니다.  

기본적으로 데이터 및 로그 파일이 초기화되어 이전에 삭제한 파일의 디스크에 남아 있는 기존 데이터를 덮어씁니다. 데이터 및 로그 파일은 사용자가 다음 작업을 수행하면 파일을 비워(0으로 채워져) 초기화됩니다.  
  
- 데이터베이스 만들기  
- 기존 데이터베이스에 데이터 또는 로그 파일을 추가합니다.  
- 기존 파일의 크기를 늘립니다(자동 증가 작업 포함).  
- 데이터베이스 또는 파일 그룹을 복원합니다.  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 IFI(인스턴트 파일 초기화)를 사용하여 앞서 언급한 파일 작업을 더 빠르게 실행할 수 있습니다. 이는 해당 공간을 0으로 채우지 않고 사용된 디스크 공간을 회수하기 때문입니다. 대신, 새 데이터를 파일에 기록할 때 디스크 내용을 덮어씁니다. 로그 파일은 즉시 초기화할 수 없습니다.

## <a name="enable-instant-file-initialization"></a>인스턴트 파일 초기화 사용

즉시 파일 초기화는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에 *SE_MANAGE_VOLUME_NAME*을 부여받은 경우에만 사용할 수 있습니다. Windows Administrator 그룹의 구성원은 이 권한을 가지고 있으며 다른 사용자에게 **볼륨 유지 관리 작업 수행** 보안 정책을 추가하여 이 권한을 부여할 수 있습니다.  
> [!IMPORTANT]
> [TDE(투명한 데이터 암호화)](../../relational-databases/security/encryption/transparent-data-encryption.md)와 같은 일부 기능을 사용하면 즉시 파일 초기화를 막을 수 있습니다.  

> [!NOTE]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터는 설치하는 동안 이 권한을 서비스 계정에 부여할 수 있습니다. <br><br>[명령 프롬프트 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)를 사용하는 경우 /SQLSVCINSTANTFILEINIT 인수를 추가하거나 [설치 마법사](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)의 *SQL Server 데이터베이스 엔진 서비스에 볼륨 유지 관리 작업 권한 부여* 확인란을 선택합니다.
  
계정에 `Perform volume maintenance tasks` 권한을 부여하려면  
  
1.  데이터 파일을 생성할 컴퓨터에서 **로컬 보안 정책** 애플리케이션(`secpol.msc`)을 엽니다.  
  
1.  왼쪽 창에서 **로컬 정책**을 확장한 다음 **사용자 권한 할당**을 클릭합니다.  
  
1.  오른쪽 창에서 **볼륨 유지 관리 작업 수행**을 두 번 클릭합니다.  
  
1.  **사용자 또는 그룹 추가**를 클릭하고 SQL Server 서비스를 실행하는 계정을 추가합니다.  
  
1.  **적용**을 클릭한 다음 모든 **로컬 보안 정책** 대화 상자를 닫습니다.  

1. SQL Server 서비스를 다시 시작합니다.

1. 시작 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그를 확인합니다.
   
  
    **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4, [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 및 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상부터).
    1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 계정에 *SE_MANAGE_VOLUME_NAME*이 부여되면 다음과 같은 정보 메시지가 기록됩니다.

        `Database Instant File Initialization: enabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`

    1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 계정에 *SE_MANAGE_VOLUME_NAME*이 부여되지 **않으면** 다음과 같은 정보 메시지가 기록됩니다.

        `Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`
    > [!NOTE]
    > [sys.dm_server_services](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md) DMV에서 *instant_file_initialization_enabled* 열을 사용하여 인스턴트 파일 초기화가 사용하도록 설정되었는지 확인할 수도 있습니다.

## <a name="security-considerations"></a>보안 고려 사항

이점이 보안 위험을 능가할 수 있으므로 인스턴트 파일 초기화를 사용하는 것이 좋습니다.

인스턴트 파일 초기화를 사용하는 경우 파일에 새 데이터가 기록될 때만 삭제된 디스크 내용을 덮어씁니다. 그러므로 데이터 파일의 특정 영역에 다른 데이터가 기록될 때까지는 권한 없는 보안 주체가 삭제된 내용에 액세스할 수 있습니다.

데이터베이스 파일이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 연결되어 있는 동안 파일의 DACL(임의 액세스 제어 목록)에 의해 이러한 정보 공개 위협이 줄어듭니다. 이 DACL은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정 및 로컬 관리자에게만 파일 액세스를 허용합니다. 그러나 파일이 분리되면 *SE_MANAGE_VOLUME_NAME*이 없는 사용자 또는 서비스가 액세스할 수 있습니다.

다음과 같은 경우에도 비슷한 고려 사항이 있습니다.

* 데이터베이스가 백업됩니다. 백업 파일이 적절한 DACL로 보호되지 않는 경우 권한이 없는 사용자 또는 서비스가 삭제된 내용을 사용할 수 있게 됩니다.  

* 파일이 IFI를 사용하여 증가합니다. SQL Server 관리자가 잠재적으로 원시 페이지 내용에 액세스하고 이전에 삭제된 내용을 볼 수 있습니다.

* 데이터베이스 파일이 저장 영역 네트워크에서 호스트됩니다. 저장 영역 네트워크가 항상 미리 초기화된 새 페이지를 표시하고 운영 체제에서 페이지를 다시 초기화하도록 하여 불필요한 오버헤드가 발생할 수 있습니다.

삭제된 내용의 공개 가능성이 우려된다면 다음 작업 중 하나 또는 둘 다를 수행해야 합니다.  
  
- 분리된 데이터 파일 및 백업 파일에 제한적인 DACL이 있는지 항상 확인합니다.  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 인스턴트 파일 초기화를 사용하지 않도록 설정합니다.    이렇게 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 계정에서 *SE_MANAGE_VOLUME_NAME*을 취소합니다.
    
    > [!NOTE]
    > 사용하지 않도록 설정하면 데이터 파일에 대한 할당 시간이 늘어나고 사용자 권한이 취소된 후 생성되거나 크기가 증가한 파일에만 영향을 줍니다.
  
## <a name="see-also"></a>참고 항목  
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)

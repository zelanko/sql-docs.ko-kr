---
title: 데이터베이스 즉시 파일 초기화 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2019
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
manager: craigg
ms.openlocfilehash: 9b75512b0b0e4f4975074bd35f797f526d25ffc2
ms.sourcegitcommit: 3c4bb35163286da70c2d669a3f84fb6a8145022c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2019
ms.locfileid: "57683603"
---
# <a name="database-file-initialization"></a>데이터베이스 파일 초기화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
데이터 및 로그 파일이 초기화되어 이전에 삭제한 파일의 디스크에 남아 있는 기존 데이터를 덮어씁니다. 데이터 및 로그 파일은 사용자가 다음 작업 중 하나를 수행할 때 파일을 비워(0으로 채워져) 초기화됩니다.  
  
- 데이터베이스를 만듭니다.  
- 기존 데이터베이스에 데이터 또는 로그 파일을 추가합니다.  
- 기존 파일의 크기를 늘립니다(자동 증가 작업 포함).  
- 데이터베이스 또는 파일 그룹을 복원합니다.  
  
파일 초기화는 이러한 작업의 수행 시간을 더 오래 만듭니다. 그러나 데이터를 처음으로 파일에 기록할 때 운영 체제는 0으로 파일을 채울 수 없습니다.  
  
## <a name="instant-file-initialization-ifi"></a>IFI(즉시 파일 초기화)  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 데이터 파일을 즉시 초기화하여 비우기 작업을 방지할 수 있습니다. 인스턴트 파일 초기화를 통해 이전에 언급한 파일 작업을 빠르게 실행할 수 있습니다. 즉시 파일 초기화는 디스크 공간을 0으로 채우지 않고 디스크 공간을 회수합니다. 대신, 새 데이터를 파일에 기록할 때 디스크 내용을 덮어씁니다. 로그 파일은 즉시 초기화할 수 없습니다.  
  
> [!NOTE]
> 인스턴트 파일 초기화는 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] 또는 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 이상 버전에서만 사용할 수 있습니다.  
> 
> [!IMPORTANT]
> 즉시 파일 초기화는 데이터 파일에만 사용할 수 있습니다. 로그 파일은 만들어질 때나 크기가 증가할 때 항상 비워집니다.
  
즉시 파일 초기화는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에 *SE_MANAGE_VOLUME_NAME*을 부여받은 경우에만 사용할 수 있습니다. Windows Administrator 그룹의 구성원은 이 권한을 가지고 있으며 다른 사용자에게 **볼륨 유지 관리 작업 수행** 보안 정책을 추가하여 이 권한을 부여할 수 있습니다.  
  
> [!IMPORTANT]
> [TDE(투명한 데이터 암호화)](../../relational-databases/security/encryption/transparent-data-encryption.md)와 같은 일부 기능을 사용하면 즉시 파일 초기화를 막을 수 있습니다.  
  
계정에 `Perform volume maintenance tasks` 권한을 부여하려면  
  
1.  데이터 파일을 생성할 컴퓨터에서 **로컬 보안 정책** 애플리케이션(`secpol.msc`)을 엽니다.  
  
2.  왼쪽 창에서 **로컬 정책**을 확장한 다음 **사용자 권한 할당**을 클릭합니다.  
  
3.  오른쪽 창에서 **볼륨 유지 관리 작업 수행**을 두 번 클릭합니다.  
  
4.  **사용자 또는 그룹 추가**를 클릭하고 SQL Server 서비스를 실행하는 계정을 추가합니다.  
  
5.  **적용**을 클릭한 다음 모든 **로컬 보안 정책** 대화 상자를 닫습니다.  

1. SQL Server 서비스를 다시 시작합니다.

> [!NOTE]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터는 설치하는 동안 이 권한을 서비스 계정에 부여할 수 있습니다. [명령 프롬프트 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)를 사용하는 경우 /SQLSVCINSTANTFILEINIT 인수를 추가하거나 [설치 마법사](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)의 *SQL Server 데이터베이스 엔진 서비스에 볼륨 유지 관리 작업 권한 부여* 확인란을 선택합니다.

> [!NOTE]
> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4부터 그리고 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지는 [sys.dm_server_services](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md) DMV의 *instant_file_initialization_enabled* 열을 사용하여 인스턴트 파일 초기화가 사용되는지 확인할 수 있습니다.

## <a name="remarks"></a>Remarks
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 계정에 *SE_MANAGE_VOLUME_NAME*이 부여되면 시작 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 다음과 유사한 정보 메시지가 기록됩니다. 

`Database Instant File Initialization: enabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 계정에 *SE_MANAGE_VOLUME_NAME*이 부여되지 **않으면** 시작 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 다음과 유사한 정보 메시지가 기록됩니다. 

`Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`

**적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4부터, [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 및 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

## <a name="security-considerations"></a>보안 고려 사항  
삭제된 디스크 내용은 새 데이터가 파일에 기록될 때만 덮어쓰기 때문에 인스턴트 파일 초기화(IFI)를 사용하는 경우 데이터 파일의 해당하는 특정 영역에 다른 데이터를 쓸 때까지 권한 없는 사용자가 삭제된 내용에 액세스할 수 있습니다. 데이터베이스 파일이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 연결되어 있는 동안 파일의 DACL(임의 액세스 제어 목록)에 의해 이러한 정보 공개 위협이 줄어듭니다. 이 DACL은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정 및 로컬 관리자에게만 파일 액세스를 허용합니다. 그러나 파일이 분리되면 *SE_MANAGE_VOLUME_NAME*이 없는 사용자 또는 서비스가 액세스할 수 있습니다. 데이터베이스를 백업할 때도 유사한 사항을 고려해야 합니다. 즉, 백업 파일이 적절한 DACL로 보호되지 않는 경우 권한이 없는 사용자 또는 서비스가 삭제된 내용을 사용할 수 있게 됩니다.  

또 다른 고려 사항은 파일이 IFI를 사용하여 증가하는 경우입니다. SQL Server 관리자는 잠재적으로 원시 페이지 콘텐츠에 엑세스하고 이전에 삭제된 내용을 확인할 수 있습니다.

데이터베이스 파일을 스토리지 영역 네트워크에서 호스트하는 경우 저장 영역 네트워크는 항상 미리 초기화된 새 페이지를 표시하고 운영 체제에서 페이지를 다시 초기화하는 경우 불필요한 오버헤드가 발생할 수 있습니다.
 
> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 보안 물리적 환경에 설치되어 있는 경우 인스턴스 파일 초기화를 사용할 때 성능 이점이 보안 위험을 능가하므로 이렇게 하는 것이 좋습니다.
  
삭제된 내용의 공개 가능성이 우려된다면 다음 작업 중 하나 또는 둘 다를 수행해야 합니다.  
  
- 분리된 데이터 파일 및 백업 파일에 제한적인 DACL이 있는지 항상 확인합니다.  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 계정에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SE_MANAGE_VOLUME_NAME*을 취소하여* 의 인스턴스에 대한 즉시 파일 초기화를 해제합니다. 

> [!IMPORTANT]
> 인스턴트 파일 초기화를 해제하면 데이터 파일의 할당 시간이 늘어납니다.  
  
> [!NOTE]  
> 즉시 파일 초기화 해제는 사용자 권한이 취소된 후 생성되거나 크기를 늘린 파일에만 영향을 미칩니다.  
  
## <a name="see-also"></a>참고 항목  
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  

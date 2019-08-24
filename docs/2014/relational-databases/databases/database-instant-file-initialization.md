---
title: 데이터베이스 즉시 파일 초기화 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initializations [SQL Server]
- fast file initialization (SQL Server)
- file initialization [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 491c8a63c7ee3ed06c90356c58820f34ed3c0bf9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62872098"
---
# <a name="database-instant-file-initialization"></a>데이터베이스 즉시 파일 초기화
  데이터 및 로그 파일이 초기화되어 이전에 삭제한 파일의 디스크에 남아 있는 기존 데이터를 덮어씁니다. 데이터 및 로그 파일은 사용자가 다음 작업 중 하나를 수행할 때 0으로 채워져 초기화됩니다.  
  
-   데이터베이스를 만듭니다.  
  
-   기존 데이터베이스에 파일, 로그 또는 데이터를 추가합니다.  
  
-   기존 파일의 크기를 늘립니다(자동 증가 작업 포함).  
  
-   데이터베이스 또는 파일 그룹을 복원합니다.  
  
 파일 초기화는 이러한 작업의 수행 시간을 더 오래 만듭니다. 그러나 데이터를 처음으로 파일에 기록할 때 운영 체제는 0으로 파일을 채울 수 없습니다.  
  
## <a name="instant-file-initialization"></a>즉시 파일 초기화  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터 파일을 즉시 초기화할 수 있습니다. 이를 통해 이전에 언급한 파일 작업을 신속히 실행할 수 있습니다. 즉시 파일 초기화는 디스크 공간을 0으로 채우지 않고 디스크 공간을 회수합니다. 대신, 새 데이터를 파일에 기록할 때 디스크 내용을 덮어씁니다. 로그 파일은 즉시 초기화할 수 없습니다.  
  
> [!NOTE]  
>  인스턴트 파일 초기화는 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] 또는 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 이상 버전에서만 사용할 수 있습니다.  
  
 즉시 파일 초기화는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) 서비스 계정에 SE_MANAGE_VOLUME_NAME을 부여받은 경우에만 사용할 수 있습니다. Windows Administrator 그룹의 구성원은 이 권한을 가지고 있으며 다른 사용자에게 **볼륨 유지 관리 작업 수행** 보안 정책을 추가하여 이 권한을 부여할 수 있습니다. 사용자 권한 할당에 대한 자세한 내용은 Windows 설명서를 참조하세요.  
  
 TDE를 사용하도록 설정되어 있으면 즉시 파일 초기화를 사용할 수 없습니다.  
  
 계정에 `Perform volume maintenance tasks` 권한을 부여하려면  
  
1.  백업 파일을 생성할 컴퓨터에서 `Local Security Policy` 애플리케이션(`secpol.msc`)을 엽니다.  
  
2.  왼쪽 창에서 **로컬 정책**을 확장한 다음 **사용자 권한 할당**을 클릭합니다.  
  
3.  오른쪽 창에서 **볼륨 유지 관리 작업 수행**을 두 번 클릭합니다.  
  
4.  **사용자 또는 그룹 추가** 를 클릭하고 백업에 사용되는 사용자 계정을 추가합니다.  
  
5.  클릭 **Apply**를 모두 닫고 `Local Security Policy` 대화 상자.  
  
### <a name="security-considerations"></a>보안 고려 사항  
 삭제된 디스크 내용은 새 데이터가 파일에 기록될 때만 덮어쓰기 때문에 권한 없는 사용자가 삭제된 내용에 액세스할 수 있습니다. 데이터베이스 파일이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 연결되어 있는 동안 파일의 DACL(임의 액세스 제어 목록)에 의해 이러한 정보 공개 위협이 줄어듭니다. 이 DACL은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정 및 로컬 관리자에게만 파일 액세스를 허용합니다. 그러나 파일이 분리되면 SE_MANAGE_VOLUME_NAME이 없는 사용자 또는 서비스가 액세스할 수 있습니다. 데이터베이스가 백업될 때에도 유사한 위협이 존재합니다. 백업 파일이 적절한 DACL로 보호되지 않는 경우 권한이 없는 사용자 또는 서비스가 삭제된 내용을 사용할 수 있게 됩니다.  
  
 삭제된 내용의 공개 가능성이 우려된다면 다음 중 하나 또는 둘 다를 수행해야 합니다.  
  
-   분리된 데이터 파일 및 백업 파일에 제한적인 DACL이 있는지 항상 확인합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에서 SE_MANAGE_VOLUME_NAME을 취소하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스에 대한 즉시 파일 초기화를 해제합니다.  
  
> [!NOTE]  
>  즉시 파일 초기화 해제는 사용자 권한이 취소된 후 생성되거나 크기를 늘린 파일에만 영향을 미칩니다.  
  
## <a name="see-also"></a>관련 항목  
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  

---
title: 스냅샷 폴더 보안 설정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], security
ms.assetid: 3cd877d1-ffb8-48fd-a72b-98eb948aad27
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 30e0f800477af8305f64b617aa3af543e789bdc1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051888"
---
# <a name="secure-the-snapshot-folder"></a>스냅샷 폴더 보안 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  스냅샷 폴더는 스냅샷 파일을 저장하는 디렉터리입니다. 스냅샷 스토리지 전용 디렉터리를 지정하는 것이 좋습니다. 스냅샷 에이전트에 폴더에 대한 쓰기 권한을 부여하고 병합 에이전트 또는 배포 에이전트가 폴더에 액세스할 때 사용하는 Windows 계정에만 읽기 권한을 부여합니다. 에이전트에 연결된 Windows 계정은 원격 컴퓨터에 있는 스냅샷 폴더에 액세스할 수 있는 도메인 계정이어야 합니다.  
  
> [!NOTE]  
>  UAC(사용자 계정 컨트롤)는 관리자가 승격된 사용자 권한( *권한*이라고도 함)을 관리하는 데 유용합니다. UAC를 사용하도록 설정된 운영 체제에서 실행할 때는 관리자가 해당 관리자 권한을 사용하지 않습니다. 대신 대부분의 동작을 관리 권한이 없는 일반 사용자로 수행하며 필요한 경우에만 임시로 해당 관리자 권한을 사용합니다. UAC에서는 스냅샷 공유에 대한 관리 액세스를 거부할 수 있습니다. 따라서 스냅샷 에이전트, 배포 에이전트 및 병합 에이전트에서 사용하는 Windows 계정에 스냅샷 공유 권한을 명시적으로 부여해야 합니다. Windows 계정이 Administrators 그룹의 멤버인 경우에도 이 작업을 수행해야 합니다.  
  
 배포 구성 마법사나 새 게시 마법사를 사용하여 배포자를 구성할 때 스냅샷 폴더의 기본값은 로컬 경로인 X:\Program Files\Microsoft SQL Server\\ *\<instance>* \MSSQL\ReplData입니다. 원격 배포자나 끌어오기 구독을 사용하는 경우에는 로컬 경로 대신 UNC 네트워크 공유(예: \\\\<*computername>* \snapshot)를 지정해야 합니다.  
  
 스냅샷 폴더에 대한 액세스 권한을 부여할 때는 폴더가 액세스되는 방법에 따라 권한을 부여해야 합니다. 다음 대화 상자 탭은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2003에서 사용됩니다.  
  
-   로컬 경로를 지정하는 경우 해당 폴더에 대한 **속성** 대화 상자의 **보안** 탭을 통해 사용 권한을 부여합니다.  
  
-   네트워크 공유를 지정하는 경우 해당 폴더에 대한 **속성** 대화 상자의 **공유** 탭을 통해 사용 권한을 부여합니다.  
  
    > [!NOTE]  
    >  배포자에서 복제 에이전트를 실행하는 경우 폴더에 대한 **속성** 대화 상자의 **보안** 탭을 사용하여 에이전트를 실행하는 데 사용되는 Windows 계정에 사용 권한을 부여합니다. 네트워크 공유가 사용되는 경우에도 이 작업을 수행하십시오. 이 내용은 밀어넣기 구독의 경우 병합 에이전트와 배포 에이전트에 적용되며 게시자와 배포자가 같은 컴퓨터에 있는 경우 스냅샷 에이전트에도 적용됩니다.  
  
 로컬 경로 및 네트워크 공유에 대해 사용 권한을 설정하는 방법은 Windows 설명서를 참조하십시오.  
  
> [!NOTE]  
>  게시를 삭제하면 복제는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정의 보안 컨텍스트에서 스냅샷 폴더를 제거합니다. 이 계정에 충분한 권한이 없는 경우에는 적절한 권한이 있는 계정으로 로그인하여 해당 폴더를 수동으로 삭제해야 합니다. 폴더를 삭제하려면 폴더가 로컬 경로인 경우 **수정** 권한이 필요하고 네트워크 경로인 경우 **모든 권한** 이 필요합니다.  
  
## <a name="delivering-snapshots-through-ftp"></a>FTP를 통해 스냅샷 배달  
 보안상 스냅샷을 UNC 공유에 저장하는 것이 가장 좋지만 스냅샷을 FTP 공유에 저장한 다음 FTP를 통해 구독자로 배달할 수도 있습니다. FTP 서버를 구성할 때는 스냅샷 에이전트가 게시에 대한 쓰기 권한을 가지도록 허용하는 기본 UNC 공유가 가상 디렉터리에 표시되도록 합니다.  
  
 구독자를 구성하여 FTP를 통해 스냅샷을 검색하려면 먼저 FTP 서버에 FTP 로그인과 암호를 설정합니다. 이 로그인과 암호는 스냅샷 파일을 다운로드할 수 있도록 구독자에게 읽기(또는 "가져오기") 액세스 권한을 허용합니다.  
  
 FTP를 통해 스냅샷을 배달하려면 [FTP를 통해 스냅샷 배달](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)을 참조하세요.  
  
 FTP를 통해 스냅샷에 액세스하는 데 필요한 암호를 설정하고 변경하는 방법은 [Secure the Publisher](../../../relational-databases/replication/security/secure-the-publisher.md)항목의 "FTP 스냅샷 배달" 섹션을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [스냅샷 옵션 수정](../../../relational-databases/replication/snapshot-options.md)   
 [스냅샷으로 구독 초기화](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [복제 보안 설정 보기 및 수정](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [FTP를 통해 스냅샷 전송](../../../relational-databases/replication//publish/deliver-a-snapshot-through-ftp.md)  
  
  

---
title: "데이터베이스 백업 태스크(유지 관리 계획) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.maint.maintplanproperties.logbackup.f1
- sql13.swb.maint.backup.f1
helpviewer_keywords: Back Up Database Task dialog box
ms.assetid: ed1ef012-fa14-4ba5-bafe-d1527ba065b3
caps.latest.revision: "52"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5cd325a83874a12581143e7bf634c3b7348c28ce
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="options-in-the-back-up-database-task-for-maintenance-plan"></a>유지 관리 계획을 위한 데이터베이스 백업 태스크의 옵션
  **데이터베이스 백업 태스크** 대화 상자를 사용하여 유지 관리 계획에 백업 작업을 추가할 수 있습니다. 데이터베이스 백업은 시스템이나 하드웨어 상의 장애 또는 사용자의 오류로 인해 데이터베이스가 손상되어 백업 복사본을 복원해야 하는 경우를 대비하기 위한 중요한 작업입니다. 이 태스크를 통해 전체 백업, 차등 백업, 파일 및 파일 그룹 백업, 트랜잭션 로그 백업을 수행할 수 있습니다.  
  
 **데이터베이스 백업 태스크를 만들려면**  
  
-   [유지 관리 계획 만들기](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)  
  
## <a name="options"></a>옵션  
 **연결**  
 이 태스크를 수행할 때 사용할 서버 연결을 선택합니다.  
  
 **새로 만들기**  
 이 태스크를 수행할 때 사용할 새 서버 연결을 만듭니다. 아래에서는 **새 연결** 대화 상자에 대해 설명합니다.  
  
 **데이터베이스**  
 이 태스크의 영향을 받는 데이터베이스를 지정합니다. 이 옵션을 선택하면 **모든 데이터베이스**, **모든 시스템 데이터베이스**, **모든 사용자 데이터베이스**, **다음 데이터베이스**옵션을 제공하는 드롭다운 목록이 표시됩니다.  
  
 **모든 데이터베이스**  
 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대해 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다.  
  
 **모든 시스템 데이터베이스(master, msdb, model)**  
 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터베이스에 대해 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다. 사용자가 만든 데이터베이스에 대해서는 유지 관리 태스크가 실행되지 않습니다.  
  
 **모든 사용자 데이터베이스(master, model, msdb, tempdb 제외)**  
 사용자가 만든 모든 데이터베이스에 대해 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터베이스에 대해서는 유지 관리 태스크가 실행되지 않습니다.  
  
 **다음 데이터베이스**  
 선택한 데이터베이스에 대해서만 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다. 이 옵션을 선택한 경우에는 목록에서 하나 이상의 데이터베이스를 선택해야 합니다.  
  
 **백업 유형**  
 수행할 백업 유형을 표시합니다.  
  
 **백업 구성 요소**  
 전체 데이터베이스를 백업하려면 **데이터베이스** 를 선택합니다. 데이터베이스 일부만 백업하려면 **파일 및 파일 그룹** 을 선택합니다. 이 옵션을 선택한 경우 파일 또는 파일 그룹 이름을 제공합니다. **데이터베이스** 상자에서 여러 데이터베이스를 선택한 경우에는 **백업 구성 요소** 에 대해 **데이터베이스**만 지정합니다. 파일 또는 파일 그룹 백업을 수행하려면 각 데이터베이스에 대해 태스크를 만듭니다.  
  
 **백업 세트 만료 기한**  
 백업 세트를 다른 백업 세트로 덮어쓸 수 있는 날짜를 지정합니다.  
  
 **백업할 위치**  
 파일 또는 테이프에 데이터베이스를 백업합니다. 데이터베이스를 포함하는 컴퓨터에 연결된 테이프 장치만 사용할 수 있습니다.  
  
 **하나 이상의 파일에 데이터베이스 백업**  
 **추가** 를 클릭하여 **백업 대상 선택** 대화 상자를 연 다음 하나 이상의 디스크 위치나 테이프 장치를 지정합니다.  
  
 **백업 파일이 있는 경우**  
 파일의 끝에 이 백업을 추가하려면 **추가** 를 선택합니다. 파일의 이전 백업을 모두 제거하고 새 백업으로 바꾸려면 **덮어쓰기**를 선택합니다.  
  
 **모든 데이터베이스에 대한 백업 파일 만들기**  
 폴더 상자에서 지정한 위치에 백업 파일을 만듭니다. 선택한 데이터베이스당 하나의 파일이 생성됩니다.  
  
 **각 데이터베이스에 대한 하위 디렉터리 만들기**  
 각 데이터베이스를 하위 폴더에 저장하려면 선택합니다.  
  
> [!IMPORTANT]  
>  유지 관리 계획으로 하위 디렉터리를 만들 수는 있지만 의 유지 관리 태스크로 하위 디렉터리를 삭제할 수는 없습니다. 이 기능은 유지 관리 정리 태스크를 사용하여 파일을 삭제하는 악의적 공격의 가능성을 줄여 줍니다.  
  
> [!IMPORTANT]  
>  하위 디렉터리는 부모 디렉터리에서 사용 권한을 상속받습니다. 무단으로 액세스하지 못하도록 하려면 사용 권한을 제한하세요.  
  
 **Folder**  
 자동으로 생성된 데이터베이스 파일을 포함할 폴더를 지정합니다.  
  
 **백업 파일 확장명**  
 백업 파일에 사용할 확장명을 지정합니다. 기본값은 **.bak**입니다.  
  
 **백업 무결성 확인**  
 백업 세트가 올바른지 확인하고 모든 볼륨을 읽을 수 있는지 확인합니다.  
  
 **비상 로그 백업을 수행하고 복원 중인 상태로 데이터베이스 유지**  
 데이터베이스를 복원하기 전의 마지막 단계로 로그 백업을 수행합니다. 자세한 내용은 [비상 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)을 참조하세요.  
  
 **백업 압축 설정**  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (이상 버전)에서 다음 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md) 값 중 하나를 선택합니다.  
  
|||  
|-|-|  
|**기본 서버 설정 사용**|서버 수준 기본값을 사용하려면 클릭합니다.<br /><br /> 이 기본값은 **백업 압축 기본값** 서버 구성 옵션으로 설정됩니다. 이 옵션의 현재 설정을 확인하는 방법은 [backup compression default 서버 구성 옵션 보기 또는 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)을 참조하세요.|  
|**백업 압축**|서버 수준 기본값에 관계없이 백업을 압축하려면 클릭합니다.<br /><br /> **\*\* 중요 \*\*** 압축 시에는 기본적으로 CPU 사용량이 크게 증가하며, 압축 프로세스에서 CPU를 추가로 사용하므로 동시 작업 성능이 저하될 수 있습니다. 따라서 CPU 사용량이 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)에 의해 제한되는 세션에서 우선 순위가 낮은 압축 백업을 만들 수 있습니다. 자세한 내용은 이 항목 뒷부분의 [Resource GovernoR을 사용하여 백업 압축을 통해 CPU 사용량 제한&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)에 의해 제한되는 세션에서 우선 순위가 낮은 압축 백업을 만들 수 있습니다.|  
|**백업 압축 안 함**|서버 수준 기본값에 관계없이 압축되지 않은 백업을 만들려면 클릭합니다.|  
  
 **T-SQL 보기**  
 선택한 옵션을 기반으로 서버에 대해 수행한 이 태스크의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 표시합니다.  
  
> [!NOTE]  
>  영향을 받은 개체 수가 많은 경우에는 표시하는 데 시간이 오래 걸릴 수 있습니다.  
  
## <a name="new-connection-dialog-box"></a>새 연결 대화 상자  
 **연결 이름**  
 새 연결의 이름을 입력합니다.  
  
 **서버 이름 선택 또는 입력**  
 이 태스크를 수행할 때 연결할 서버를 선택합니다.  
  
 **새로 고침**  
 사용할 수 있는 서버 목록을 새로 고칩니다.  
  
 **서버 로그온 정보 입력**  
 서버에 대한 인증 방법을 지정합니다.  
  
 **Windows NT 통합 보안 사용**  
 Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결합니다.  
  
 **특정 사용자 이름 및 암호 사용**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다. 이 옵션은 사용할 수 없습니다.  
  
 **사용자 이름**  
 인증 시 사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 입력합니다. 이 옵션은 사용할 수 없습니다.  
  
 **암호**  
 인증 시 사용할 암호를 입력합니다. 이 옵션은 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)  
  
  

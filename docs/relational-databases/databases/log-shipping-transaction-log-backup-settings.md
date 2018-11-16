---
title: 로그 전달 트랜잭션 로그 백업 설정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.logshipping.settings.tlogback.f1
ms.assetid: 9a6e6c16-7f71-412b-bba6-7bffac001277
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 98fde530e6d6d15d4abfdd97d53d6beff354a394
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558680"
---
# <a name="log-shipping-transaction-log-backup-settings"></a>로그 전달 트랜잭션 로그 백업 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 대화 상자를 사용하여 로그 전달 구성에 대한 트랜잭션 로그 백업 설정을 구성하고 수정할 수 있습니다.  
  
 로그 전달 개념에 대한 설명은 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)를 참조하세요.  
  
## <a name="options"></a>Options  
 **백업 폴더의 네트워크 경로**  
 이 상자에 백업 폴더의 네트워크 공유를 입력합니다. 트랜잭션 로그 백업을 저장하는 로컬 폴더를 공유해야 로그 전달 복사 작업을 통해 해당 파일을 보조 서버에 복사할 수 있습니다. 보조 서버 인스턴스에서 복사 작업을 실행하는 데 사용할 프록시 계정에 이 네트워크 공유를 읽을 수 있는 권한을 부여해야 합니다. 기본적으로 이 계정은 보조 서버 인스턴스의 SQLServerAgent 서비스 계정이지만 관리자가 다른 프록시 계정을 선택하여 작업에 사용할 수 있습니다.  
  
 **백업 폴더가 주 서버에 있는 경우 폴더의 로컬 경로를 입력하십시오.**  
 백업 폴더가 주 서버에 있는 경우 백업 폴더의 로컬 드라이브 문자와 경로를 입력합니다. 백업 폴더가 주 서버에 없는 경우에는 이 상자를 비워 둘 수 있습니다.  
  
 여기에서 로컬 경로를 지정하면 BACKUP 명령에서 이 경로를 사용하여 트랜잭션 로그 백업을 만듭니다. 그러나 로컬 경로를 지정하지 않으면 BACKUP 명령에서 **백업 폴더의 네트워크 경로** 상자에 지정된 네트워크 경로를 사용합니다.  
  
> [!NOTE]  
>  주 서버의 로컬 시스템 계정에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정이 실행되고 있으면 주 서버에 백업 폴더를 만들고 여기에서 이 폴더의 로컬 경로를 지정해야 합니다. 주 서버 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에는 이 폴더에 대한 읽기 및 쓰기 권한이 있어야 합니다.  
  
 **다음보다 오래된 파일 삭제**  
 트랜잭션 로그 백업을 삭제하기 전에 백업 디렉터리에 보관하는 기간을 지정합니다.  
  
 **다음 기간 내에 백업이 발생하지 않으면 경고**  
 트랜잭션 로그 백업이 수행되지 않았다는 경고를 발생시키기 전까지 로그 전달에서 기다리는 기간을 지정합니다.  
  
 **작업 이름**  
 로그 전달에 사용할 트랜잭션 로그 백업을 만드는 데 사용되는 SQL Server 에이전트 작업의 이름을 표시합니다. 처음 작업을 만들 때 상자에 이름을 입력하여 수정할 수 있습니다.  
  
 **일정**  
 주 데이터베이스의 트랜잭션 로그를 백업하기 위한 현재 일정을 표시합니다. 백업 작업이 생성되기 전에는 **일정...** 을 클릭하여 이 일정을 수정할 수 있고 작업이 생성된 후에는 **작업 편집...** 을 클릭하여 이 일정을 수정할 수 있습니다.  
  
### <a name="backup-job"></a>백업 작업  
 **일정...**  
 SQL Server 에이전트 작업을 만들 때 생성되는 일정을 수정합니다.  
  
 **작업 편집...**  
 주 데이터베이스에 대해 트랜잭션 로그 백업을 수행하는 작업의 SQL Server 에이전트 작업 매개 변수를 수정합니다.  
  
 **이 작업 비활성화**  
 트랜잭션 로그 백업을 만들지 않도록 SQL Server 에이전트 작업을 비활성화합니다.  
  
### <a name="compression"></a>압축  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (이상 버전)에서는 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md)을 지원합니다.  
  
 **백업 압축 설정**  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상 버전에서 이 로그 전달 구성의 로그 백업에 대해 다음 백업 압축 값 중 하나를 선택합니다.  
  
|||  
|-|-|  
|**기본 서버 설정 사용**|서버 수준 기본값을 사용하려면 클릭합니다.<br /><br /> 이 기본값은 **백업 압축 기본값** 서버 구성 옵션으로 설정됩니다. 이 옵션의 현재 설정을 확인하는 방법에 대한 자세한 내용은 [백업 압축 기본값 서버 구성 옵션 보기 또는 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)을 참조하세요.|  
|**백업 압축**|서버 수준 기본값에 관계없이 백업을 압축하려면 클릭합니다.<br /><br /> **\*\* 중요 \*\*** 기본적으로 압축하면 CPU 사용량이 크게 늘어나고 압축 프로세스로 사용되는 추가 CPU는 동시 작업에 악영향을 줄 수 있습니다. 따라서 CPU 사용량이 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)에 의해 제한되는 세션에서 우선 순위가 낮은 압축 백업을 만들 수 있습니다. 자세한 내용은 이 항목 뒷부분의 [Resource Governor를 사용하여 백업 압축을 통해 CPU 사용량 제한&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)에 의해 제한되는 세션에서 우선 순위가 낮은 압축 백업을 만들 수 있습니다.|  
|**백업 압축 안 함**|서버 수준 기본값에 관계없이 압축되지 않은 백업을 만들려면 클릭합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 에이전트 작업을 만들고 관리하도록 사용자 구성](../../ssms/agent/configure-a-user-to-create-and-manage-sql-server-agent-jobs.md)   
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
  

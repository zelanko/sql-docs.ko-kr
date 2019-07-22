---
title: 데이터베이스 백업(일반 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 07/01/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.backupdatabase.general.f1
ms.assetid: 5c344dfd-1ad3-41cc-98cd-732973b4a162
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e3bbac9bbdc12e5f2c1a0fb318a91860e44131d0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67940921"
---
# <a name="back-up-database-general-page"></a>데이터베이스 백업(일반 페이지)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **데이터베이스 백업** 대화 상자의 **일반** 페이지를 사용하여 데이터베이스 백업 작업에 대한 설정을 확인하거나 수정할 수 있습니다.  
  
 기본 백업 개념에 대한 자세한 내용은 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 백업 태스크를 지정할 때 **스크립트** 단추를 클릭한 다음 스크립트에 대한 대상을 선택하여 해당되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) 스크립트를 생성할 수 있습니다.  
  
 **SQL Server Management Studio를 사용하여 백업을 만들려면**  
  
-   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
    > [!IMPORTANT]  
    >  데이터베이스 유지 관리 계획을 정의하여 데이터베이스 백업을 만들 수 있습니다. 자세한 내용은 [온라인 설명서의](../maintenance-plans/maintenance-plans.md) 데이터베이스 유지 관리 계획 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 을 참조하세요.  
  
 **부분 백업을 만들려면**  
  
-   부분 백업의 경우 PARTIAL 옵션과 함께 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) 문을 사용해야 합니다.  
  
## <a name="options"></a>옵션  
  
### <a name="source"></a>원본  
 **원본** 패널의 옵션은 데이터베이스를 식별하고 백업 작업에 대한 구성 요소 및 백업 유형을 지정합니다.  
  
 **데이터베이스 백업**  
 백업할 데이터베이스를 선택합니다.  
  
 **복구 모델**  
 선택한 데이터베이스에 대해 표시되는 복구 모델(SIMPLE, FULL 또는 BULK_LOGGED)을 검토합니다.  
  
 **백업 유형**  
 지정한 데이터베이스에서 수행할 백업 유형을 선택합니다.  
  
|백업 유형|사용 가능한 대상|Restrictions|  
|-----------------|-------------------|------------------|  
|전체|데이터베이스, 파일 및 파일 그룹|**master** 데이터베이스에서는 전체 백업만 가능합니다.<br /><br /> 단순 복구 모델에서는 읽기 전용 파일 그룹에 대해서만 파일 및 파일 그룹 백업을 사용할 수 있습니다.|  
|차등|데이터베이스, 파일 및 파일 그룹|단순 복구 모델에서는 읽기 전용 파일 그룹에 대해서만 파일 및 파일 그룹 백업을 사용할 수 있습니다.|  
|트랜잭션 로그|트랜잭션 로그|단순 복구 모델에는 트랜잭션 로그 백업을 사용할 수 없습니다.|  
  
 **복사 전용 백업**  
 복사 전용 백업을 만들려면 선택합니다. *복사 전용 백업*은 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 시퀀스와 독립적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업입니다. 자세한 내용은 [복사 전용 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)를 참조하세요.  
  
> [!NOTE]  
>  **차등** 옵션을 선택하는 경우 복사 전용 백업을 만들 수 없습니다.  
  
 **백업 구성 요소**  
 백업할 데이터베이스 구성 요소를 선택합니다. **백업 유형** 목록에서 **트랜잭션 로그** 를 선택한 경우에는 이 옵션을 사용할 수 없습니다.  
  
 다음 옵션 단추 중 하나를 선택합니다.  
  
|||  
|-|-|  
|**데이터베이스 백업**|전체 데이터베이스를 백업할지를 지정합니다.|  
|**파일 및 파일 그룹**|선택한 파일 및/또는 파일 그룹을 백업할지를 지정합니다.<br /><br /> 이 옵션을 선택하면 **파일 및 파일 그룹 선택** 대화 상자가 열립니다. 백업하려는 파일 그룹이나 파일을 선택하고 **확인**을 클릭하면 **파일 그룹 및 파일** 상자에 선택한 내용이 나타납니다.|  
  
### <a name="destination"></a>Destination  
 **대상** 패널의 옵션을 사용하면 백업 작업에 대한 백업 디바이스 유형을 지정하고 기존 논리적 또는 물리적 백업 디바이스를 찾을 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 디바이스에 대한 자세한 내용은 [백업 디바이스&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)를 참조하세요.  
  
 **백업할 위치**  
 다음 중 백업할 미디어 유형 하나를 선택합니다. **백업할 위치** 목록에 선택한 대상이 나타납니다.  
  
|||  
|-|-|  
|**디스크**|디스크에 백업합니다. 데이터베이스에 대해 만든 시스템 파일이나 디스크 기반의 논리적 백업 디바이스일 수 있습니다. **백업할 위치** 목록에 현재 선택한 디스크가 나타납니다. 백업 작업에 대해 최대 64개의 디스크 디바이스를 선택할 수 있습니다.|  
|**Tape**|테이프에 백업합니다. 데이터베이스에 대해 만든 로컬 테이프 드라이브나 테이프 기반의 논리적 백업 디바이스일 수 있습니다. **백업할 위치** 목록에 현재 선택한 테이프가 나타납니다. 최대 개수는 64개입니다. 서버에 연결된 테이프 디바이스가 없으면 이 옵션이 비활성화됩니다. **백업할 위치** 목록에 선택한 테이프가 나열됩니다.<br /><br /> 참고: 테이프 백업 디바이스에 대한 지원은 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.|  
|**URL**|Microsoft Azure Blob Storage에 백업합니다.|  
  
 아래 표시된 다음 옵션 집합은 선택한 대상 유형에 따라 달라집니다. 디스크 또는 테이프를 선택하면 다음 옵션이 표시됩니다.  
  
 **추가**  
 **백업할 위치** 목록에 파일이나 디바이스를 추가합니다. 로컬 디스크 또는 원격 디스크의 최대 64개의 디바이스로 동시에 백업할 수 있습니다. 원격 디스크에서 파일을 지정하려면 정규화된 UNC(Universal Naming Convention) 이름을 사용합니다. 자세한 내용은 [백업 디바이스&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)를 참조하세요.  
 
 
  
 **제거**  
 **백업할 위치** 목록에서 현재 선택한 디바이스를 하나 이상 제거합니다.  
  
 **내용**  
선택한 디바이스가 있으면 미디어 내용을 표시합니다.  단추는 **URL** 이 지정된 경우 함수를 수행하지 않습니다. 
   
**백업 대상 선택** 대화 상자: **추가** 를 선택하면 **백업 대상 선택**대화 상자가 나타납니다.   아래 표시된 옵션 집합은 선택한 대상 유형에 따라 달라집니다. 

**디스크** 또는 **테이프** 를 백업 대상으로 선택하면 다음 옵션이 표시됩니다.  

*
  **파일 이름**  
    백업 파일의 이름을 지정합니다.

**URL** 을 백업 대상으로 선택하면 다음 옵션이 표시됩니다.
*
  **Azure Storage 컨테이너**  
  백업 파일을 저장할 Microsoft Azure Storage 컨테이너의 이름입니다. 
   
*
  **공유 액세스 정책:**  
  수동으로 입력한 컨테이너에 대한 공유 액세스 서명을 입력합니다.  기존 컨테이너를 선택한 경우에는 이 필드를 사용할 수 없습니다.
  
*
  **백업 파일:**  
  백업 파일의 이름입니다.

*
  **새 컨테이너:**  
공유 액세스 서명이 없는 기존 컨테이너를 등록하는 데 사용됩니다.  [Microsoft Azure 구독에 연결](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md)을 참조하세요.
  
## <a name="see-also"></a>참고 항목  
 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [파일 및 파일 그룹 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [디스크 파일에 대한 논리적 백업 디바이스 정의&#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [테이프 드라이브에 대한 논리적 백업 디바이스 정의&#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [복구 모델&#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  

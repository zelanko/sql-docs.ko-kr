---
title: 데이터베이스 백업(일반 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.backupdatabase.general.f1
ms.assetid: 5c344dfd-1ad3-41cc-98cd-732973b4a162
caps.latest.revision: 59
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7300b9be81e07a922079bc8e1b56aa02266d9b99
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093779"
---
# <a name="back-up-database-general-page"></a>데이터베이스 백업(일반 페이지)
  **데이터베이스 백업** 대화 상자의 **일반** 페이지를 사용하여 데이터베이스 백업 작업에 대한 설정을 확인하거나 수정할 수 있습니다.  
  
 기본 백업 개념에 대한 자세한 내용은 [백업 개요&#40;SQL Server&#41;](backup-overview-sql-server.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 백업 태스크를 지정할 때 [!INCLUDE[tsql](../../includes/tsql-md.md)][스크립트](/sql/t-sql/statements/backup-transact-sql) 단추를 클릭한 다음 스크립트에 대한 대상을 선택하여 해당되는 **BACKUP** 스크립트를 생성할 수 있습니다.  
  
 **SQL Server Management Studio를 사용하여 백업을 만들려면**  
  
-   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
    > [!IMPORTANT]  
    >  데이터베이스 유지 관리 계획을 정의하여 데이터베이스 백업을 만들 수 있습니다. 자세한 내용은 [온라인 설명서의](http://msdn.microsoft.com/library/ms187658.aspx) 데이터베이스 유지 관리 계획 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 을 참조하세요.  
  
 **부분 백업을 만들려면**  
  
-   부분 백업의 경우 PARTIAL 옵션과 함께 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](/sql/t-sql/statements/backup-transact-sql) 문을 사용해야 합니다.  
  
## <a name="options"></a>변수  
  
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
 복사 전용 백업을 만들려면 선택합니다. *복사 전용 백업*은 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 시퀀스와 독립적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업입니다. 자세한 내용은 [복사 전용 백업&#40;SQL Server&#41;](copy-only-backups-sql-server.md)를 참조하세요.  
  
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
 **대상** 패널의 옵션을 사용하면 백업 작업에 대한 백업 장치 유형을 지정하고 기존 논리적 또는 물리적 백업 장치를 찾을 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 장치에 대한 자세한 내용은 [백업 장치&#40;SQL Server&#41;](backup-devices-sql-server.md)를 참조하세요.  
  
 **백업할 위치**  
 다음 중 백업할 미디어 유형 하나를 선택합니다. **백업할 위치** 목록에 선택한 대상이 나타납니다.  
  
|||  
|-|-|  
|**디스크**|디스크에 백업합니다. 데이터베이스에 대해 만든 시스템 파일이나 디스크 기반의 논리적 백업 장치일 수 있습니다. **백업할 위치** 목록에 현재 선택한 디스크가 나타납니다. 백업 작업에 대해 최대 64개의 디스크 장치를 선택할 수 있습니다.|  
|**Tape**|테이프에 백업합니다. 데이터베이스에 대해 만든 로컬 테이프 드라이브나 테이프 기반의 논리적 백업 장치일 수 있습니다. **백업할 위치** 목록에 현재 선택한 테이프가 나타납니다. 최대 개수는 64개입니다. 서버에 연결된 테이프 장치가 없으면 이 옵션이 비활성화됩니다. **백업할 위치** 목록에 선택한 테이프가 나열됩니다.<br /><br /> 참고: 테이프 백업 장치에 대한 지원은 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요.|  
|**URL**|Windows Azure Blob 저장소에 백업합니다.|  
  
 아래 표시된 다음 옵션 집합은 선택한 대상 유형에 따라 달라집니다. 디스크 또는 테이프를 선택하면 다음 옵션이 표시됩니다.  
  
 **추가**  
 **백업할 위치** 목록에 파일이나 장치를 추가합니다. 로컬 디스크 또는 원격 디스크의 최대 64개의 장치로 동시에 백업할 수 있습니다. 원격 디스크에서 파일을 지정하려면 정규화된 UNC(Universal Naming Convention) 이름을 사용합니다. 자세한 내용은 [백업 장치&#40;SQL Server&#41;](backup-devices-sql-server.md)).  
  
 **제거**  
 **백업할 위치** 목록에서 현재 선택한 장치를 하나 이상 제거합니다.  
  
 **내용**  
 선택한 장치의 미디어 내용을 표시합니다.  
  
 URL을 백업 대상으로 선택하면 다음 옵션이 표시됩니다.  
  
 **파일 이름**  
 백업 파일의 이름을 지정합니다.  
  
 **SQL 자격 증명**  
 Windows Azure 저장소에 인증하는 데 사용되는 SQL 자격 증명을 선택합니다. 사용할 수 있는 기존 SQL 자격 증명이 없는 경우 **만들기** 단추를 클릭하여 새 SQL 자격 증명을 만듭니다.  
  
> [!IMPORTANT]  
>  **만들기** 를 클릭하면 열리는 대화 상자에서는 관리 인증서나 구독용 게시 프로필이 필요합니다. 관리 인증서나 게시 프로필에 액세스할 수 없는 경우 Transact-SQL이나 SQL Server Management Studio를 사용하여 저장소 계정 이름을 지정하고 키 정보에 액세스하여 SQL 자격 증명을 만들 수 있습니다. 샘플 코드를 참조는에 [자격 증명을 만들려면](../security/authentication-access/create-a-credential.md#Credential) TRANSACT-SQL을 사용 하 여 자격 증명을 만들려면 항목입니다. 또는 SQL Server Management Studio를 사용하여 데이터베이스 엔진 인스턴스에서 **보안**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**, **자격 증명**을 차례로 선택합니다. **ID** 에 대한 저장소 계정 이름을 지정하고 **암호** 필드에 액세스 키를 지정합니다.  
  
 **Azure 저장소 컨테이너**  
 Windows Azure 저장소 컨테이너의 이름을 지정합니다.  
  
 **URL 접두사:**  
 이는 지정된 Azure 저장소 컨테이너 이름 및 SQL 자격 증명에 저장된 저장소 계정 정보를 기반으로 자동 생성됩니다. **\<storage account>.blob.core.windows.net** 이외의 형식을 사용하는 도메인을 사용하지 않는 경우 이 필드의 정보를 편집하지 않는 것이 좋습니다.  
  
## <a name="see-also"></a>관련 항목  
 [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)   
 [파일 및 파일 그룹 백업&#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)   
 [디스크 파일에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [테이프 드라이브에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [복구 모델&#40;SQL Server&#41;](recovery-models-sql-server.md)  
  
  

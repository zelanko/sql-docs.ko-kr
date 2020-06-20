---
title: 백업 대상 선택 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.selectbackupdest.f1
ms.assetid: f79e824b-1525-45de-8ede-513563af41b6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5ffd1d2529dd13e42689bcf168c972d757fb5499
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84956543"
---
# <a name="select-backup-destination"></a>백업 대상 선택
  **백업 대상 선택** 대화 상자를 사용하여 디바이스를 백업 대상으로 선택할 수 있습니다. 디스크 또는 논리적 백업 디바이스를 백업 대상으로 사용할 수 있습니다.  
  
 **SQL Server Management Studio를 사용하여 데이터베이스를 백업하려면**  
  
-   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [파일 및 파일 그룹 백업&#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
## <a name="options"></a>옵션  
 이 대화 상자의 옵션은 대상을 디스크에서 선택하는지 또는 테이프에서 선택하는지에 따라 달라집니다.  
  
 **디스크의 대상**  
 백업 대상을 지정하려면 다음 옵션 중 하나를 선택합니다.  
  
|||  
|-|-|  
|**파일 이름**|입력란에 로컬 파일 또는 원격 파일을 백업 대상으로 입력하려면 이 옵션을 선택합니다.<br /><br /> 로컬 파일을 지정하려면 입력란 오른쪽의 찾아보기 단추를 클릭하고 서버를 실행하는 컴퓨터의 고정 드라이브에서 파일을 검색하거나 전체 경로 및 파일 이름을 직접 입력합니다(예: `C:\Program Files\Microsoft SQL Server\MSSQL\Backup\AdventureWorksBackup.bak`).<br /><br /> 원격 파일을 백업 대상으로 지정하려면 해당 파일의 정규화된 UNC(Universal Naming Convention) 이름을 입력합니다. 자세한 내용은 [백업 디바이스&#40;SQL Server&#41;](backup-devices-sql-server.md)를 참조하세요.<br /><br /> **\*\* 중요 \*\*** 네트워크를 통해 데이터를 백업할 경우에는 네트워크 오류가 발생할 수 있으므로 완료된 후에 백업 작업을 확인하는 것이 좋습니다. 자세한 내용은 [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)를 참조하세요.|  
|**백업 디바이스**|논리적 백업 디바이스를 선택하려면 이 옵션을 선택합니다.<br /><br /> 참고: 디스크 백업 디바이스를 만드는 방법에 대한 자세한 내용은 [디스크 파일에 대한 논리적 백업 디바이스 정의&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)를 참조하세요.|  
  
 **테이프의 대상**  
 서버를 실행하는 컴퓨터( [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스)에 물리적으로 연결된 테이프 드라이브에서 백업 대상을 지정합니다. 다음 옵션 중 하나를 선택합니다.  
  
|||  
|-|-|  
|**테이프 드라이브**|서버 인스턴스를 실행하는 컴퓨터에 물리적으로 연결된 테이프 드라이브의 목록에서 테이프 드라이브를 백업 대상으로 선택하려면 이 옵션을 선택합니다.<br /><br /> 참고: 원격 컴퓨터의 테이프 백업 디바이스는 올바른 백업 대상이 아닙니다.|  
|**백업 디바이스**|기존의 논리적 백업 디바이스를 선택하려면 이 옵션을 선택합니다. 이러한 논리적 백업 디바이스는 서버 인스턴스를 실행하는 컴퓨터에 물리적으로 연결된 테이프 드라이브입니다.<br /><br /> 참고: 테이프 백업 디바이스를 만드는 방법에 대한 자세한 내용은 [테이프 드라이브에 대한 논리적 백업 디바이스 정의&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)를 참조하세요.|  
  
## <a name="see-also"></a>참고 항목  
 [백업 디바이스&#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  

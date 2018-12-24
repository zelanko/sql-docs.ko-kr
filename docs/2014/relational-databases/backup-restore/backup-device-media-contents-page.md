---
title: 백업 디바이스(미디어 내용 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backupdevice.contents.f1
ms.assetid: 5fc7bd22-b6d8-4af1-8a58-2e7d0b994d08
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 524e6d8e5ec987a20d693cb1f7e06b30bc27c0b5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48130506"
---
# <a name="backup-device-media-contents-page"></a>백업 디바이스(미디어 내용 페이지)
  **백업 장치** 대화 상자를 사용하여 백업 정보를 볼 수 있습니다. 이 정보에는 디바이스, 미디어, 미디어 세트 및 백업 세트에 대한 설명이 포함됩니다.  
  
 **SQL Server Management Studio를 사용하여 백업 장치의 내용을 보려면**  
  
-   [백업 테이프 또는 파일의 내용 보기&#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [논리적 백업 장치의 속성 및 내용 보기&#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>변수  
 개별 미디어, 미디어 세트 및 백업 세트에 대한 정보를 봅니다.  
  
 **미디어**  
 백업 정보가 저장되는 디스크 또는 테이프 세트입니다.  
  
 **미디어 시퀀스**  
 미디어 시퀀스 번호, 패밀리 시퀀스 번호 및 미러 ID를 나열합니다(있는 경우). 각 물리적 백업 미디어에는 미디어가 사용된 순서를 나타내는 미디어 시퀀스 번호가 표시됩니다. 초기 백업 미디어에는 1번이, 두 번째 미디어(첫 번째 연속 테이프)에는 2번이, 나머지 미디어에도 순서에 따라 태그가 붙습니다. 미디어 시퀀스 번호는 백업 세트를 복원할 때 백업을 복원하는 운영자가 올바른 순서대로 정확하게 미디어를 탑재하도록 합니다.  
  
 **만든 날짜**  
 미디어 세트를 만든 날짜와 시간을 표시합니다.  
  
 **미디어 세트**  
 미디어 세트는 일정한 개수의 백업 디바이스를 사용하여 하나 이상의 백업 작업을 기록한 백업 미디어의 모음입니다.  
  
 **이름**  
 미디어 세트의 이름을 표시합니다(있는 경우).  
  
 **설명**  
 미디어 세트에 대한 설명을 표시합니다(있는 경우).  
  
 **미디어 패밀리 개수**  
 미디어 세트에 있는 패밀리 수를 표시합니다. 각 미디어 세트는 하나 이상의 미디어 패밀리의 모음입니다. 단일 미디어 패밀리는 지정된 단일 백업 디바이스 또는 미러된 백업 디바이스 그룹에 대한 모든 출력으로 구성됩니다. 각 미디어 세트에는 각각의 디바이스 또는 미러된 디바이스 그룹마다 하나의 미디어 패밀리가 포함됩니다. 예를 들어 한 미디어 세트에서 미러되지 않은 두 백업 디바이스를 사용하면 해당 미디어 세트에 두 개의 미디어 패밀리가 포함됩니다.  
  
 **백업 세트**  
 미디어에 포함된 백업 세트에 대한 정보를 표시합니다. 백업 세트는 성공적인 백업 작업의 결과이며 백업 디바이스 집합의 미디어 간에 해당 내용이 분산됩니다.  
  
|머리글|값|  
|------------|------------|  
|**이름**|백업 세트의 이름입니다.|  
|**형식**|백업된 개체입니다. 데이터베이스, 파일 또는 *\<비어 있음>*(트랜잭션 로그의 경우)이 될 수 있습니다.|  
|**구성 요소**|수행된 백업 유형입니다. 전체, 차등 또는 트랜잭션 로그일 수 있습니다.|  
|**Server**|백업 작업을 수행한 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스의 이름입니다.|  
|**데이터베이스 백업**|백업한 데이터베이스 이름입니다.|  
|**위치**|볼륨에 있는 백업 세트의 위치입니다.|  
|**날짜**|클라이언트의 국가별 설정으로 표시되는 백업 작업 완료 날짜 및 시간입니다.|  
|**크기**|백업 세트의 크기를 바이트 단위로 표시한 것입니다.|  
|**사용자 이름**|백업 작업을 수행한 사용자의 이름입니다.|  
|**만료**|백업 세트가 만료되는 날짜 및 시간입니다.|  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [디스크 파일에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [테이프 드라이브에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [디스크 또는 테이프를 백업 대상으로 지정&#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [백업 장치 삭제&#40;SQL Server&#41;](delete-a-backup-device-sql-server.md)  
  
-   [백업의 만료 날짜 설정&#40;SQL Server&#41;](set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [백업 테이프 또는 파일의 내용 보기&#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [백업 세트의 데이터와 로그 파일 보기&#40;SQL Server&#41;](view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [논리적 백업 장치의 속성 및 내용 보기&#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [장치에서 백업 복원&#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [백업 장치&#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  

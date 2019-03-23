---
title: 기록 정리 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.historycleanuptask.f1
helpviewer_keywords:
- history tables [SQL Server]
- History Cleanup task [Integration Services]
ms.assetid: 5defc5b9-dfd3-4859-a7fe-ac8c2b5480f8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1a7664fb91c6e60789cd59aeef1d25c33409477a
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381941"
---
# <a name="history-cleanup-task"></a>기록 정리 태스크
  기록 정리 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 데이터베이스의 다음 기록 테이블에서 항목을 삭제합니다.  
  
-   backupfile  
  
-   backupfilegroup  
  
-   backupmediafamily  
  
-   backupmediaset  
  
-   backupset  
  
-   restorefile  
  
-   restorefilegroup  
  
-   restorehistory  
  
 기록 정리 태스크를 사용하면 패키지가 백업 및 복원 작업, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 및 데이터베이스 유지 관리 계획과 관련된 기록 데이터를 삭제할 수 있습니다.  
  
 이 태스크는 sp_delete_backuphistory 시스템 저장 프로시저를 캡슐화하고 지정한 날짜를 프로시저에 인수로 전달합니다. 자세한 내용은 [sp_delete_backuphistory&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql)를 참조하세요.  
  
## <a name="configuration-of-the-history-cleanup-task"></a>기록 정리 태스크 구성  
 이 태스크에는 기록 테이블에 보관되는 데이터의 가장 오래된 날짜를 지정하는 속성이 있습니다. 현재 날짜로부터의 일, 주, 월 또는 연 수로 날짜를 지정하면 태스크에서 자동으로 이 간격이 특정 날짜로 변환됩니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 속성을 설정할 수 있습니다. 이 태스크는 **디자이너의** 도구 상자 **에 있는** 유지 관리 계획 태스크 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 섹션에서 수행할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [기록 정리 태스크&#40;유지 관리 계획&#41;](../../relational-databases/maintenance-plans/history-cleanup-task-maintenance-plan.md)  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 태스크](integration-services-tasks.md)   
 [제어 흐름](control-flow.md)  
  
  

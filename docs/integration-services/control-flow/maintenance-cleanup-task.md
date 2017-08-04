---
title: "유지 관리 정리 태스크 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.maintenancecleanuptask.f1
helpviewer_keywords:
- deleting files
- removing files
- Maintenance Cleanup task
ms.assetid: 73ad3cd6-9a6d-44cf-905f-c56aa658bf42
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 19ea8533605a0507db4ba6ac566c585d3746cc37
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="maintenance-cleanup-task"></a>유지 관리 정리 태스크
  유지 관리 정리 태스크는 유지 관리 계획에서 만든 데이터베이스 백업 파일 및 보고서를 비롯하여 유지 관리 계획과 관련된 파일을 제거합니다. 자세한 내용은 [유지 관리 계획](../../relational-databases/maintenance-plans/maintenance-plans.md) 및 [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)을 참조하세요.  
  
 유지 관리 정리 태스크를 사용하여 패키지에서 지정한 서버의 백업 파일 또는 유지 관리 계획 보고서를 제거할 수 있습니다. 유지 관리 정리 태스크는 특정 파일을 제거하거나 폴더에 있는 파일 그룹을 제거하는 옵션을 포함합니다. 필요에 따라 삭제할 파일의 확장명을 지정할 수 있습니다.  
  
 백업 파일을 제거하도록 유지 관리 정리 태스크를 구성할 때 기본 파일 이름 확장명은 BAK이며 보고서 파일의 경우 기본 파일 이름 확장명은 TXT입니다. 필요에 맞게 확장명을 업데이트할 수 있으며 확장명이 256자 미만이기만 하면 됩니다.  
  
 일반적으로 더 이상 필요하지 않은 기존 파일을 제거하며 유지 관리 정리 태스크를 구성하여 지정된 보존 기간에 도달한 파일을 삭제하도록 할 수 있습니다. 예를 들면 4주 이상된 파일을 삭제하도록 태스크를 구성할 수 있습니다. 일, 주, 월 또는 년을 사용하여 삭제할 파일의 보존 기간을 지정할 수 있습니다. 삭제할 파일의 최소 보존 기간을 지정하지 않으면 지정한 형식의 파일이 모두 삭제됩니다.  
  
 이전 버전의 유지 관리 정리 태스크와 달리 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 태스크에서는 지정된 디렉터리의 하위 디렉터리에 있는 파일이 자동으로 삭제되지 않습니다. 이러한 제약 조건으로 인해 유지 관리 정리 태스크의 기능을 이용하여 파일을 악의적으로 삭제할 수 있는 공격에 대한 노출 영역이 줄어듭니다. 첫 번째 수준의 하위 폴더를 삭제하려면 **유지 관리 정리 태스크** 대화 상자에서 **첫 번째 수준의 하위 폴더 포함** 옵션을 선택하여 이 작업을 수행하도록 명시적으로 선택해야 합니다.  
  
## <a name="configuration-of-the-maintenance-cleanup-task"></a>유지 관리 정리 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 속성을 설정할 수 있습니다. 이 태스크는 **디자이너의** 도구 상자 **에 있는** 유지 관리 계획 태스크 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 섹션에서 수행할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [유지 관리 정리 태스크&#40;유지 관리 계획&#41;](../../relational-databases/maintenance-plans/maintenance-cleanup-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법에 대한 자세한 내용은 [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [제어 흐름](../../integration-services/control-flow/control-flow.md)  
  
  

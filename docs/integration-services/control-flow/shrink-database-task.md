---
title: 데이터베이스 축소 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.shrinkdatabasetask.f1
helpviewer_keywords:
- Shrink Database task
- database shrinking [Integration Services]
- shrinking databases
ms.assetid: e66286f8-97b1-4e5a-86b4-e56f1932b7d5
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 76201a45200c66e1ba6a22eb46a7accef5a905d4
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="shrink-database-task"></a>데이터베이스 축소 태스크
  데이터베이스 축소 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 데이터와 로그 파일의 크기를 줄입니다.  
  
 데이터베이스 축소 태스크를 사용하면 패키지가 단일 데이터베이스나 여러 데이터베이스의 파일을 축소할 수 있습니다.  
  
 파일 끝에 있는 데이터 페이지를 파일 앞의 사용되지 않은 공간으로 이동하여 데이터 파일을 축소하면 공간이 복구됩니다. 파일 끝에 사용 가능한 공간을 충분히 확보한 다음 파일 끝에 있는 데이터 페이지를 할당 해제하고 파일 시스템에 반환할 수 있습니다.  
  
> [!WARNING]  
>  파일 축소를 위해 이동되는 데이터는 파일 내의 모든 사용 가능한 위치로 분산될 수 있습니다. 이로 인해 인덱스 조각화가 발생하여 인덱스 범위를 검색하는 쿼리 성능이 저하될 수 있습니다. 조각화를 방지하려면 축소 후 파일에 대한 인덱스를 다시 작성하는 것이 좋습니다.  
  
## <a name="commands"></a>명령  
 데이터베이스 축소 태스크는 다음 인수와 옵션을 포함하여 DBCC SHRINKDATABASE 명령을 캡슐화합니다.  
  
-   *database_name*  
  
-   *target_percent*  
  
-   NOTRUNCATE 또는 TRUNCATEONLY  
  
 데이터베이스 축소 태스크에서 여러 데이터베이스를 축소하는 경우 각 데이터베이스에 대해 하나씩, 여러 개의 SHRINKDATABASE 명령이 실행됩니다. SHRINKDATABASE 명령의 각 인스턴스는 *database_name* 인수를 제외하고 모두 동일한 인수 값을 사용합니다. 자세한 내용은 [DBCC SHRINKDATABASE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)를 참조하세요.  
  
## <a name="configuration-of-the-shrink-database-task"></a>데이터베이스 축소 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 속성을 설정할 수 있습니다. 이 태스크는 **디자이너의** 도구 상자 **에 있는** 유지 관리 계획 태스크 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 섹션에서 수행할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [데이터베이스 축소 태스크&#40;유지 관리 계획&#41;](../../relational-databases/maintenance-plans/shrink-database-task-maintenance-plan.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  

---
title: 패키지 실행 및 기타 작업 모니터링 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: cbbcd79f-ab9b-46ec-84cb-4821c1d16b99
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b985193eb9aa9b73d513f2d5ce8368f5d8fbb6ab
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060700"
---
# <a name="monitoring-for-package-executions-and-other-operations"></a>패키지 실행 및 기타 작업 모니터링
  다음 도구 중 하나 이상을 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 실행, 프로젝트 유효성 검사 및 기타 작업을 모니터링할 수 있습니다. 데이터 탭과 같은 일부 도구는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포된 프로젝트에 대해서만 사용할 수 있습니다.  
  
-   로그  
  
     자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](integration-services-ssis-logging.md)을 참조하세요.  
  
-   보고서  
  
     자세한 내용은 [Reports for the Integration Services Server](../reports-for-the-integration-services-server.md)을(를) 참조하세요.  
  
-   뷰  
  
     자세한 내용은 [뷰&#40;Integration Services 카탈로그&#41;](/sql/integration-services/system-views/views-integration-services-catalog)를 참조하세요.  
  
-   성능 카운터  
  
     자세한 내용은 [성능 카운터](performance-counters.md)를 참조하세요.  
  
-   데이터 탭  
  
## <a name="operation-types"></a>작업 유형  
 여러 다양 한 유형의 작업에 모니터링 되는 `SSISDB` 카탈로그는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버. 각 작업과 연관된 메시지가 여러 개 있을 수 있습니다. 각 메시지는 여러 가지 유형 중 하나로 분류될 수 있습니다. 예를 들어 정보, 경고 또는 오류 메시지일 수 있습니다. 메시지 유형에 대한 전체 목록은 Transact-SQL [catalog.operation_messages&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database) 뷰를 참조하세요. 작업 유형에 대한 전체 목록은 [catalog.operations&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database)를 참조하세요.  
  
 한 작업의 상태를 나타내기 위해 9가지 상태 유형이 사용됩니다. 상태 유형에 대한 전체 목록은 [catalog.operations&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database) 뷰를 참조하세요.  
  
## <a name="related-content"></a>관련 내용  
 blogs.msdn.com의 블로그 항목, [SSIS T-SQL API 개요](http://go.microsoft.com/fwlink/?LinkId=249051)  
  
  

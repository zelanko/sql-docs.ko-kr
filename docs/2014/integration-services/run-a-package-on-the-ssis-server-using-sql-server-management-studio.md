---
title: SQL Server Management Studio를 사용 하 여 SSIS 서버에서 패키지 실행 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 56dc1bf8-99d4-41dc-bdc4-f64f1ccfd688
caps.latest.revision: 8
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 58348805f20f33124e0a789c79aa2ef71f9d8793
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37225553"
---
# <a name="run-a-package-on-the-ssis-server-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 SSIS 서버에서 패키지 실행
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 프로젝트를 배포한 후에는 서버에서 패키지를 실행할 수 있습니다.  
  
 작업 보고서를 사용하여 서버에서 실행되었거나 현재 실행 중인 패키지에 대한 정보를 볼 수 있습니다. 자세한 내용은 [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md)을(를) 참조하세요.  
  
### <a name="to-run-a-package-on-the-server-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 서버에서 패키지를 실행하려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 열고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 카탈로그가 포함된 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 **Integration Services 카탈로그** 노드와 **SSISDB** 노드를 차례로 확장하고, 배포한 프로젝트에 포함된 패키지로 이동합니다.  
  
3.  패키지 이름을 마우스 오른쪽 단추로 클릭하고 **실행**을 선택합니다.  
  
4.  **패키지 실행**대화 상자의 **매개 변수**, **연결 관리자** 및 **고급** 탭의 설정을 사용하여 패키지 실행을 구성합니다.  
  
5.  **확인** 을 클릭하여 패키지를 실행합니다.  
  
     -또는-  
  
     저장 프로시저를 사용하여 패키지를 실행합니다. **스크립트** 를 클릭하여 실행 인스턴스를 만들고 실행 인스턴스를 시작하는 Transact-SQL 문을 생성합니다. 문에는 catalog.create_execution, catalog.set_execution_parameter_value에 대한 호출과 catalog.start_execution 저장 프로시저가 포함되어 있습니다. 이러한 저장 프로시저에 대한 자세한 내용은 [catalog.create_execution&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database), [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) 및 [catalog.start_execution&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database)을 참조하세요.  
  
  

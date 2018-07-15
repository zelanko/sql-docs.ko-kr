---
title: 부모 패키지 구현 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- parent packages [Integration Services]
ms.assetid: d8f94830-fa27-4151-88df-cbdc6bf0fc80
caps.latest.revision: 23
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 037c803cd11135c0f04e0e716b5a04b75344a177
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37329813"
---
# <a name="implementation-of-the-parent-package"></a>부모 패키지 구현
  여러 서버에서 SSIS 패키지의 로드 균형을 조정할 때 자식 패키지를 만들어 배포하고 이러한 패키지를 실행하기 위한 원격 SQL Server 에이전트 작업을 만든 다음에는 부모 패키지를 만들어야 합니다. 부모 패키지에는 많은 SQL Server 에이전트 작업 실행 태스크가 포함되며 각 태스크는 자식 패키지 중 하나를 실행하는 서로 다른 SQL Server 에이전트 작업을 호출합니다. 그러면 부모 패키지의 SQL Server 에이전트 작업 실행 태스크가 다양한 SQL Server 에이전트 작업을 실행합니다. 부모 패키지의 각 태스크에는 원격 서버 연결 방법 및 해당 서버에서 실행할 작업과 같은 정보가 포함되어 있습니다. 자세한 내용은 [Execute SQL Server Agent Job Task](control-flow/execute-sql-server-agent-job-task.md)을 참조하세요.  
  
 자식 패키지를 실행하는 부모 패키지를 확인하려면 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 의 솔루션 탐색기에서 패키지를 마우스 오른쪽 단추로 클릭한 다음 **진입점 패키지**를 클릭합니다.  
  
## <a name="listing-child-packages"></a>하위 패키지 나열  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 상위 패키지와 하위 패키지가 들어 있는 프로젝트를 배포하는 경우, 상위 패키지에서 실행되는 하위 패키지 목록을 볼 수 있습니다. 상위 패키지를 실행할 때 상위 패키지의 **개요** 보고서가 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에 자동으로 생성됩니다. 이 보고서에는 다음 이미지처럼 상위 패키지에 포함되는 패키지 실행 태스크에 의해 수행된 하위 패키지가 나열됩니다.  
  
 ![자식 패키지 목록이 있는 개요 보고서](media/overviewreport-childpackagelisting.png "자식 패키지 목록이 있는 개요 보고서")  
  
 **개요** 보고서에 액세스하는 방법은 [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md)를 참조하세요.  
  
## <a name="precedence-constraints-in-the-parent-package"></a>부모 패키지의 선행 제약 조건  
 부모 패키지의 여러 SQL Server 에이전트 작업 실행 태스크 간에 선행 제약 조건을 만들면 이러한 선행 제약 조건은 원격 서버의 SQL Server 에이전트 작업이 시작되는 시간만 제어합니다. 선행 제약 조건은 SQL Server 에이전트 작업 단계에서 실행된 자식 패키지의 성공 또는 실패 여부 정보를 받을 수 없습니다.  
  
 즉, 부모 패키지의 SQL Server 에이전트 작업 실행이 가지는 유일한 기능은 SQL Server 에이전트 작업이 자식 패키지를 실행하도록 요청하는 것이므로 자식 패키지의 성공 또는 실패 상태가 부모에게 전파되지 않습니다. SQL Server 에이전트 작업이 성공적으로 호출되면 부모 패키지는 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success>의 결과를 받습니다.  
  
 이 시나리오에서 실패는 원격 SQL Server 에이전트 작업 태스크 호출에만 실패했음을 의미합니다. 원격 서버가 다운되어 에이전트가 응답하지 않는 경우에 이러한 상황이 발생할 수 있습니다. 부모 패키지는 에이전트가 시작된 이상 태스크를 완료합니다.  
  
> [!NOTE]  
>  Transact-SQL 문인 **sp_start_job N'package_name'** 을 포함하는 SQL 실행 태스크를 사용할 수 있습니다. 자세한 내용은 [sp_start_job&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql)을 참조하세요.  
  
## <a name="debugging-environment"></a>디버깅 환경  
 부모 패키지를 테스트할 때는 디버그/디버깅 시작(F5)을 사용하여 디자이너의 디버깅 환경을 실행한 다음 사용합니다. 또는 명령 프롬프트 유틸리티인 **dtexec**를 사용할 수 있습니다. 자세한 내용은 [dtexec Utility](packages/dtexec-utility.md)를 참조하세요.  
  
  

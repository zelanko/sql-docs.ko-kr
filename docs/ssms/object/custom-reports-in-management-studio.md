---
title: Management Studio의 사용자 지정 보고서 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.summary.new.custom.report.f1
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 1ba3f758-f39b-4f5f-91ca-516cedc78979
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8f2fd6eb4e5c3c6b50f7fd96a0dd5ff51034d305
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68259511"
---
# <a name="custom-reports-in-management-studio"></a>Management Studio의 사용자 지정 보고서
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 많은 개체 탐색기 노드에는 [!INCLUDE[msCoName](../../includes/msconame_md.md)]에서 만든 표준 보고서 집합이 표시됩니다. 이러한 보고서는 일반적으로 요청되는 서버 정보를 요약합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 서비스 팩 2부터 관리자는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] 를 사용하여 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 만든 사용자 지정 보고서를 실행할 수 있습니다.  
  
## <a name="implementation"></a>구현  
사용자 지정 보고서는 보고서 정의 파일(.rdl)로 저장되며 RDL(Report Definition Language)을 사용하여 생성됩니다. RDL에는 보고서에 대한 데이터 검색 및 레이아웃 정보가 XML 형식으로 포함됩니다. RDL은 개방형 스키마입니다. 개발자는 추가 특성 및 요소를 사용하여 RDL을 확장할 수 있습니다. 보고서는 보고서 내의 모든 유효한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있습니다.  
  
개체 탐색기가 서버에 연결되어 있는 경우 사용자 지정 보고서가 현재 개체 탐색기 노드의 보고서 매개 변수를 참조하면 사용자 지정 보고서를 해당 노드의 컨텍스트에서 실행할 수 있습니다. 이렇게 하면 보고서가 현재 컨텍스트(예: 현재 데이터베이스)나 일관된 컨텍스트(예: 지정된 데이터베이스를 사용자 지정 보고서에 포함된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 일부로 지정)를 사용할 수 있습니다.  
  
## <a name="running-a-custom-report"></a>사용자 지정 보고서 실행  
다음과 같은 방법으로 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 사용자 지정 보고서를 실행할 수 있습니다.  
  
-   개체 탐색기의 노드를 마우스 오른쪽 단추로 클릭하고 **보고서** 를 가리킨 다음 **사용자 지정 보고서**를 마우스 왼쪽 단추로 클릭합니다. **파일 열기** 대화 상자에서 .rdl 파일이 포함된 폴더를 찾은 다음 적절한 보고서 파일을 엽니다.  
  
-   개체 탐색기의 노드를 마우스 오른쪽 단추로 클릭하고 **보고서**, **사용자 지정 보고서**를 차례로 가리킨 다음 가장 최근에 사용한 파일 목록에서 사용자 지정 보고서를 선택합니다.  
  
## <a name="limitations"></a>제한 사항  
사용자 지정 보고서를 사용할 때는 다음과 같은 제한 사항을 고려해야 합니다.  
  
-   악의적인 코드를 실수로 실행할 수 있으므로 .rdl 파일이 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 와 연결되도록 파일 시스템을 구성한 경우에도 보고서를 자동으로 실행하도록 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 구성할 수 없습니다. 보고서는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 프로그래밍 방식으로 실행할 수 없으며 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 통해 명령줄에서 실행할 수도 없습니다.  
  
-   예상한 값을 산출하지 않는 컨텍스트에서 사용자 지정 보고서를 실행할 수 있습니다. 예를 들어 복제와 관련되지 않은 데이터베이스의 컨텍스트에서 복제에 대한 보고서를 실행하거나 정확한 보고서를 생성하는 데 필요한 정보에 대한 액세스 권한이 없는 사용자로 보고서를 실행할 수 있습니다. 사용자 지정 보고서의 작성자는 보고서 구조와 해당 컨텍스트의 유효성을 검사해야 합니다.  
  
-   사용자 지정 보고서는 표준 보고서 목록에 추가할 수 없습니다.  
  
-   보고서에서 처리하는 코드는 서버 성능에 영향을 줄 수 있습니다.  
  
-   사용자 지정 보고서는 하위 보고서를 지원하지 않습니다.  
  
-   보고서 내의 각 쿼리에 대한 명령 텍스트는 식을 통해 정의하면 안 됩니다.  
  
-   명령(쿼리)에 사용되는 모든 쿼리 매개 변수는 단일 보고서 매개 변수만 참조할 수 있으며 식 연산자를 사용할 수 없습니다.  
  
-   Text 및 StoredProcedure 명령 유형만 보고서 명령(쿼리)에 사용할 수 있습니다.  
  
-   보고서 프레임워크는 쿼리에 대해 매개 변수 이스케이프를 제공하지 않습니다. 쿼리 작성자는 쿼리가 SQL 인젝션 공격으로부터 안전한지 확인해야 합니다.  
  
## <a name="managing-custom-reports"></a>사용자 지정 보고서 관리  
많은 사용자 지정 보고서를 보유하고 있는 사용자의 경우 적절한 NTFS 파일 시스템 권한이 있는 파일 시스템 폴더를 사용하여 보고서를 구성하는 것이 좋습니다.  
  
## <a name="permissions"></a>사용 권한  
사용자 지정 보고서는 현재 사용자의 사용 권한을 사용하여 실행됩니다. 보고서에서 실행하는 쿼리를 악의적인 사용자가 변경하지 못하게 하려면 보고서 파일이 있는 파일 시스템 폴더에 대한 액세스가 제한되도록 사용 권한을 설정해야 합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 사용되는 사용자와 계정 모두에는 보고서 파일이 있는 파일 시스템 폴더에 대한 읽기 권한이 필요합니다.  
  
유효한 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 명령은 보고서에 포함할 수 있지만 명령이 실행되지는 않습니다.  
  
> [!CAUTION]  
> 유효한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 보고서에 포함할 수 있으며 실행할 수도 있습니다. 권한이 높은 사용자 계정에서 보고서를 실행하면 포함된 모든 명령을 문제 없이 실행할 수 있습니다.  
  

  
## <a name="see-also"></a>참고 항목  
[Management Studio에 사용자 지정 보고서 추가](../../ssms/object/add-a-custom-report-to-management-studio.md)  
[사용자 지정 보고서 실행 경고 표시](../../ssms/object/unsuppress-run-custom-report-warnings.md)  
[개체 탐색기 노드 속성과 함께 사용자 지정 보고서 사용](../../ssms/object/use-custom-reports-with-object-explorer-node-properties.md)  
  

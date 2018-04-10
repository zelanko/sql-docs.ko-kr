---
title: Excel 연결 관리자 | Microsoft Docs
ms.date: 04/02/2018
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c36d49debc132b6e67b2bcbd2a37df75007419ff
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="excel-connection-manager"></a>Excel 연결 관리자
  Excel 연결 관리자를 사용하면 패키지에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 통합 문서 파일에 연결할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 포함되는 Excel 원본과 Excel 대상에서 Excel 연결 관리자가 사용됩니다.  
 
> [!IMPORTANT]
> Excel 파일 연결 및 Excel 파일에서 데이터를 로드할 때 제한 사항 및 알려진 문제에 대한 자세한 내용은 [SSIS(SQL Server Integration Services)를 통해 Excel로 데이터 로드](../load-data-to-from-excel-with-ssis.md)를 참조하세요.

 패키지에 Excel 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 Excel 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하고, 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다.  
  
 연결 관리자의 **ConnectionManagerType** 속성이 **EXCEL**로 설정됩니다.  
  
## <a name="configure-the-excel-connection-manager"></a>Excel 연결 관리자 구성  
 다음과 같은 방법으로 Excel 연결 관리자를 구성할 수 있습니다.  
  
-   Excel 통합 문서 파일의 경로를 지정합니다.  
  
-   파일을 만드는 데 사용된 Excel 버전을 지정합니다.  
  
-   선택한 워크시트 또는 범위에서 첫 데이터 행에 열 이름이 포함되는지 여부를 나타냅니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [Excel 연결 관리자 편집기](../../integration-services/connection-manager/excel-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="excel-connection-manager-editor"></a>Excel 연결 관리자 편집기
  **Excel 연결 관리자 편집기** 대화 상자를 사용하여 기존 또는 새 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 통합 문서 파일에 대한 연결을 추가할 수 있습니다.  
  
### <a name="options"></a>변수  
 **Excel 파일 경로**  
 기존 또는 새 Excel 통합 문서 파일의 경로와 파일 이름을 입력합니다.  
   
 **찾아보기**  
 **열기** 대화 상자를 사용하여 Excel 파일이 있는 폴더 또는 새 파일을 만들려는 폴더로 이동합니다.  
  
 **Excel 버전**  
 파일을 만드는 데 사용된 Microsoft Excel 버전을 지정합니다.  
  
 **첫 행은 열 이름으로**  
 선택한 워크시트의 첫 데이터 행에 열 이름이 포함되는지 여부를 지정합니다. 이 옵션의 기본값은 **True**입니다.  
  
## <a name="related-tasks"></a>관련 작업  
[SSIS(SQL Server Integration Services)를 통해 Excel에서 데이터 로드](../load-data-to-from-excel-with-ssis.md)  
[Excel 원본](../data-flow/excel-source.md)  
[Excel 대상](../data-flow/excel-destination.md)

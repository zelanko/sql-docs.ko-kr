---
title: "Excel 연결 관리자 | Microsoft Docs"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "파일 [Integration Services], 연결"
  - "연결 [Integration Services], Excel"
  - "Excel [Integration Services]"
  - "연결 관리자 [Integration Services], Excel"
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 41
---
# Excel 연결 관리자
  Excel 연결 관리자를 사용하면 패키지에서 기존 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 통합 문서 파일에 연결할 수 있습니다.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 포함되는 Excel 원본과 Excel 대상에서 Excel 연결 관리자가 사용됩니다.  
  
 패키지에 Excel 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 런타임에 Excel 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하고, 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다.  
  
 연결 관리자의 **ConnectionManagerType** 속성이 **EXCEL**로 설정됩니다.  
  
## Excel 연결 관리자 구성  
 다음과 같은 방법으로 Excel 연결 관리자를 구성할 수 있습니다.  
  
-   Excel 통합 문서 파일의 경로를 지정합니다.  
  
    > [!NOTE]  
    >  암호로 보호된 Excel 파일에는 연결할 수 없습니다.  
  
-   파일을 만드는 데 사용된 Excel 버전을 지정합니다.  
  
-   선택한 워크시트 또는 범위에서 액세스한 첫 데이터 행에 열 이름이 포함되는지 여부를 나타냅니다.  
  
 Excel 연결 관리자가 Excel 원본에 사용될 경우 열 이름이 추출한 데이터에 포함됩니다. Excel 대상에 사용될 경우에는 열 이름이 기록된 데이터에 포함됩니다.  
  
 Excel 원본 및 Excel 대상의 동작에 대한 자세한 내용은 [Excel Source](../../integration-services/data-flow/excel-source.md) 및 [Excel Destination](../../integration-services/data-flow/excel-destination.md)을(를) 참조하십시오.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [Excel 연결 관리자 편집기](../../integration-services/connection-manager/excel-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)를 참조하세요.  
  
 Excel 파일 그룹을 통한 루핑 방법에 대한 자세한 내용은 [Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)을 참조하세요.  
  
## 관련 작업  
  
-   [Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [Excel 통합 문서에 연결](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
  
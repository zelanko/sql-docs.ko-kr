---
title: "ADO.NET 연결 관리자 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "연결 관리자 [Integration Services], ADO.NET"
  - "ADO.NET 연결 관리자 [Integration Services]"
  - "연결 [Integration Services], ADO.NET"
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
caps.latest.revision: 59
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 59
---
# ADO.NET 연결 관리자
  [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 사용하면 패키지에서 .NET 공급자를 사용하여 데이터 원본에 액세스할 수 있습니다. 이 연결 관리자는 일반적으로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 같은 데이터 원본에 액세스하는 데 사용되며, C#과 같은 언어를 사용하여 관리 코드로 작성된 사용자 지정 태스크의 OLE DB 및 XML로 제공되는 데이터 원본에 액세스하는 데에도 사용됩니다.  
  
 패키지에 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 추가하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 런타임에 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하며, 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다.  
  
 연결 관리자의 **ConnectionManagerType** 속성이 **ADO.NET**로 설정됩니다. **ConnectionManagerType** 의 값은 연결 관리자에서 사용되는 .NET 공급자 이름이 포함되도록 한정됩니다.  
  
## ADO.NET 연결 관리자 문제 해결  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자가 외부 데이터 공급자에 대해 수행하는 호출을 로깅할 수 있습니다. 이 로깅 기능을 사용하여 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자가 수행하는 외부 데이터 원본에 대한 연결 문제를 해결할 수 있습니다. [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자가 외부 데이터 공급자에 대해 수행하는 호출을 로깅하려면 패키지 로깅을 설정하고 패키지 수준에서 **Diagnostic** 이벤트를 선택합니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자에서 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜 데이터 형식의 데이터를 읽으면 다음 표에 표시된 결과가 생성됩니다.  
  
|SQL Server 데이터 형식|결과|  
|--------------------------|------------|  
|**time**, **datetimeoffset**|매개 변수가 있는 SQL 명령이 패키지에 사용되지 않을 경우 패키지가 실패합니다. 매개 변수가 있는 SQL 명령을 사용하려면 패키지에서 SQL 실행 태스크를 사용하십시오. 자세한 내용은 [SQL 실행 태스크](../../integration-services/control-flow/execute-sql-task.md) 및 [SQL 실행 태스크의 매개 변수 및 반환 코드](../Topic/Parameters%20and%20Return%20Codes%20in%20the%20Execute%20SQL%20Task.md)를 참조하세요.|  
|**datetime2**|[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자가 밀리초 값을 자릅니다.|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 및 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식에 매핑하는 방법에 대한 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) 및 [Integration Services 데이터 형식](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## ADO.NET 연결 관리자 구성  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자는 다음과 같은 방법으로 구성할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
-   선택된 .NET 공급자에 대한 요구 사항을 만족하도록 구성된 특정 연결 문자열을 제공합니다.  
  
-   공급자에 따라 연결할 데이터 원본의 이름을 포함시킵니다.  
  
-   선택된 공급자에 적합한 보안 자격 증명을 제공합니다.  
  
-   연결 관리자에서 만든 연결이 런타임에 유지될지 여부를 나타냅니다.  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자의 여러 구성 옵션은 연결 관리자에서 사용되는 .NET 공급자에 따라 달라집니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [ADO.NET 연결 관리자 구성](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)를 참조하세요.  
  
## 관련 항목:  
 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
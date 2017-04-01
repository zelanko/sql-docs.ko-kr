---
title: "DataReader 대상 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.datareaderdest.f1"
helpviewer_keywords: 
  - "DataReader 대상"
  - "대상 [Integration Services], DataReader"
ms.assetid: 56fcc4bf-c901-42c3-a71d-110039293431
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# DataReader 대상
  DataReader 대상은 ADO.NET **DataReader** 인터페이스를 사용하여 데이터 흐름에 데이터를 제공합니다. 그러면 다른 응용 프로그램에서 이 데이터를 사용할 수 있습니다. 예를 들어 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 실행 결과를 사용하도록 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서의 데이터 원본을 구성할 수 있습니다. 이렇게 하려면 DataReader 대상을 구현하는 데이터 흐름을 만듭니다.  
  
 DataReader 대상의 값을 프로그래밍 방식으로 액세스하고 읽는 방법에 대한 자세한 내용은 [로컬 패키지의 출력 로드](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)를 참조하세요.  
  
## DataReader 대상 구성  
 DataReader 대상에 대해 제한 시간 값을 지정하고 제한 시간이 초과될 경우 대상이 실패하는지 여부를 나타낼 수 있습니다. 응용 프로그램이 지정된 시간 내에 데이터를 요청하지 않으면 제한 시간이 초과됩니다.  
  
 DataReader 대상은 하나의 입력을 갖습니다. 오류 출력은 지원하지 않습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](../Topic/Common%20Properties.md)  
  
-   [DataReader 대상 사용자 지정 속성](../../integration-services/data-flow/datareader-destination-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
  
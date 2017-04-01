---
title: "패키지 구성 도우미 | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.packageconfigurationorganizer.f1"
helpviewer_keywords: 
  - "패키지 구성 도우미 대화 상자"
ms.assetid: f20ae6cb-9e6a-4d24-88ff-d7a903a4e8d3
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 39
---
# 패키지 구성 도우미
  **패키지 구성 도우미** 대화 상자를 사용하여 패키지 구성을 설정하고, 현재 패키지에 대한 구성 목록을 보고, 구성을 로드해야 하는 기본 순서를 지정할 수 있습니다.  
  
> **참고:** 구성은 패키지 배포 모델에 사용할 수 있습니다. 매개 변수는 프로젝트 배포 모델에 대한 구성 대신 사용됩니다. 프로젝트 배포 모델을 사용하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다. 배포 모델에 대한 자세한 내용은 [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)를 참조하십시오.  
  
 여러 구성에서 동일한 속성을 업데이트하는 경우 구성 목록에서 더 아래에 있는 구성의 값이 목록에서 위에 있는 구성의 값을 대체합니다. 패키지를 실행하면 마지막으로 속성에 로드된 값이 사용됩니다. 또한 패키지가 XML 구성 파일 등의 직접 구성과 환경 변수 등의 간접 구성을 조합해서 사용하는 경우 직접 구성의 위치를 가리키는 간접 구성이 목록에서 더 위에 있어야 합니다.  
  
> **참고:** 패키지 구성이 기본 순서로 로드되는 경우 **패키지 구성 도우미** 대화 상자에 표시된 목록의 맨 위에서 맨 아래까지의 구성이 로드됩니다. 그러나 런타임 시 패키지 구성이 기본 순서로 로드되지 않을 수 있습니다. 특히 부모 패키지 구성은 다른 유형의 구성보다 뒤에 로드됩니다.  
  
 패키지 구성은 런타임 시 패키지 개체의 속성 값을 업데이트합니다. 패키지가 로드되면 구성의 값이 패키지 개발 시 설정한 값을 대체합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 여러 가지 구성 유형을 지원합니다. 예를 들어 여러 구성이 포함될 수 있는 XML 파일이나 단일 구성이 포함되는 환경 변수를 사용할 수 있습니다. 자세한 내용은 [Package Configurations](../../integration-services/packages/package-configurations.md)을 참조하세요.  
  
## 옵션  
 **패키지 구성 설정**  
 패키지에 구성을 사용하려면 선택합니다.  
  
 **구성 이름**  
 구성의 이름을 봅니다.  
  
 **구성 유형**  
 구성이 저장된 위치의 유형을 봅니다.  
  
 **구성 문자열**  
 구성 값이 저장된 위치를 봅니다. 위치는 파일 경로, 환경 변수 이름, 부모 패키지 변수 이름, 레지스트리 키 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 이름일 수 있습니다.  
  
 **대상 개체**  
 구성에서 업데이트하는 개체의 이름을 봅니다. 구성이 XML 구성 파일이나 SQL Server 테이블인 경우 여러 개체를 포함할 수 있으므로 열이 비어 있습니다.  
  
 **대상 속성**  
 구성에서 수정하는 속성의 이름을 봅니다. 구성 유형에서 여러 구성을 지원하는 경우 이 열은 비어 있습니다.  
  
 **추가**  
 패키지 구성 마법사를 사용하여 구성을 추가합니다.  
  
 **편집**  
 패키지 구성 마법사를 다시 실행하여 기존 구성을 편집합니다.  
  
 **제거**  
 구성을 선택한 다음 **제거**를 클릭합니다.  
  
 **화살표**  
 구성을 선택하고 위로 화살표 및 아래로 화살표를 사용하여 해당 구성을 목록에서 위 또는 아래로 이동합니다. 구성은 목록에 나타나는 순서대로 로드됩니다.  
  
## 관련 항목:  
 [패키지 구성 만들기](../../integration-services/packages/create-package-configurations.md)  
  
  
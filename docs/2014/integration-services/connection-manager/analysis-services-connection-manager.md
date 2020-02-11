---
title: Analysis Services 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], Analysis Services
- connection managers [Integration Services], Analysis Services
- Analysis Services connection manager
ms.assetid: 9f9cadad-a1d0-4db5-98f5-df5dbbec1be4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8f8ca9ce77e151e761e2cbb1f9128a44784af8ca
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68890398"
---
# <a name="analysis-services-connection-manager"></a>Analysis Services 연결 관리자
  연결 관리자를 사용 하면 패키지 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 데이터베이스를 실행 하는 서버 또는 큐브 및 차원 데이터 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 대 한 액세스를 제공 하는 프로젝트에 연결할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 패키지를 개발하는 동안에는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]프로젝트에만 연결할 수 있습니다. 런타임에는 사용자가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 배포하는 서버 및 데이터베이스에 패키지가 연결됩니다.  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 실행 태스크 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 처리 태스크와 같은 태스크와 데이터 마이닝 모델 학습 대상과 같은 대상에는 모두 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자가 사용됩니다.  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 대한 자세한 내용은 [다차원 model 데이터베이스&#40;SSAS&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/multidimensional-model-databases-ssas)를 참조하세요.  
  
## <a name="configuration-of-the-analysis-services-connection-manager"></a>Analysis Services 연결 관리자 구성  
 패키지 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 연결 관리자를 추가 하면에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 런타임에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결로 확인 되는 연결 관리자를 만들고, 연결 관리자 속성을 설정 하 고, 연결 관리자를 패키지의 `Connections` 컬렉션에 추가 합니다. 연결 관리자의 `ConnectionManagerType` 속성이 `MSOLAP100`로 설정됩니다.  
  
 다음과 같은 방법으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자를 구성할 수 있습니다.  
  
-   Microsoft OLE Provider for Analysis Services 공급자의 요구 사항에 맞게 구성된 연결 문자열을 제공합니다.  
  
-   연결할 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 지정합니다.  
  
-   
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하는 경우 인증 모드를 지정합니다.  
  
-   연결 관리자에서 만든 연결이 런타임에 유지될지 여부를 나타냅니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 
  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [Analysis Services 연결 관리자 추가 대화 상자 UI 참조](add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
  

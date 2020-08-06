---
title: 데이터 원본 | Microsoft Docs
ms.custom: ''
ms.date: 08/27/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data sources [Integration Services], about data sources
ms.assetid: 7ac81612-9822-470f-8d0f-a1dc96142fe3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 20bd12bf7d7fd516bfa660252c34964a4cf9bec7
ms.sourcegitcommit: 7035d9471876c70b99c58bf9b46af5cce6e9c66c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2020
ms.locfileid: "87523325"
---
# <a name="data-sources-for-ssisnoversion-packages"></a>[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지용 데이터 원본

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에 사용할 수 있는 데이터 원본인 디자인 타임 개체를 포함합니다.  
  
 데이터 원본 개체는 연결에 대한 참조이며 최소한 연결 문자열과 데이터 원본 식별자가 포함됩니다. 또한 여기에는 설명, 이름, 사용자 이름 및 암호와 같은 추가 메타데이터가 포함될 수 있습니다.  
  
> **참고:** 패키지 배포 모델을 사용하도록 구성된 프로젝트에만 데이터 원본을 추가할 수 있습니다. 프로젝트가 프로젝트 배포 모델을 사용하도록 구성된 경우 데이터 원본을 사용하는 대신 프로젝트 수준에서 만든 연결 관리자를 사용하여 연결을 공유합니다.  
>   
>  배포 모델에 대한 자세한 내용은 [Deployment of Projects and Packages](../packages/deploy-integration-services-ssis-projects-and-packages.md)를 참조하십시오. 프로젝트를 프로젝트 배포 모델로 변환하는 방법은 [Deploy Projects to Integration Services Server](https://msdn.microsoft.com/library/hh231102.aspx)를 참조하십시오.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 데이터 원본을 사용하면 다음과 같은 이점이 있습니다.  
  
-   데이터 원본에는 프로젝트 범위가 있습니다. 즉, 특정 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트에서 만든 데이터 원본은 해당 프로젝트의 모든 패키지에서 사용할 수 있습니다. 데이터 원본을 한 번 정의한 다음에는 여러 패키지에서 연결 관리자를 통해 참조할 수 있습니다.  
  
-   데이터 원본은 데이터 원본 개체와 해당 패키지 참조 간의 동기화를 제공합니다. 데이터 원본과 이를 참조하는 패키지가 동일 프로젝트에 들어 있는 경우 데이터 원본 참조에 대한 연결 문자열 속성은 데이터 원본이 변경될 때 자동으로 업데이트됩니다.  
  
## <a name="reference-data-sources"></a>데이터 원본 참조  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트에 데이터 원본 개체를 추가하려면 **솔루션 탐색기** 에서 **데이터 원본** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터 원본**을 클릭합니다. **데이터 원본** 폴더에 항목이 추가됩니다. 다른 프로젝트에서 만든 데이터 원본 개체를 사용하려면 이를 먼저 프로젝트에 추가해야 합니다.  
  
 패키지에서 데이터 원본 개체를 사용하려면 해당 데이터 원본 개체를 참조하는 연결 관리자를 패키지에 추가하면 됩니다. 패키지 제어 흐름 및 데이터 흐름을 작성하기 전이나 제어 흐름 또는 데이터 흐름을 구성하는 단계에서 패키지에 연결 관리자를 추가할 수 있습니다.  
  
 데이터 원본 개체는 데이터 원본에 대한 간단한 연결을 나타내며 데이터 저장소에서 참조되는 개체에 대한 액세스를 제공합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]AdventureWorks 샘플 데이터베이스에 연결하는 데이터 원본 개체에는 데이터베이스의 60개 테이블이 모두 포함됩니다.  
  
 데이터 원본과 이를 참조하는 연결 관리자 사이에는 종속성이 없습니다. 데이터 원본이 더 이상 프로젝트에 속하지 않는 경우에도 패키지는 계속 유효한 상태로 남습니다. 그 이유는 연결 형식과 연결 문자열과 같은 데이터 원본에 대한 정보가 패키지 정의에 포함되기 때문입니다.  
  
  

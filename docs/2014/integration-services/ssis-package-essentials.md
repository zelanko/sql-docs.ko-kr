---
title: SSIS 패키지 Essentials | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- package requirements
ms.assetid: b0c86c35-e3d3-4724-9a96-4087e9d74bf3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8cba1fb860d884b568fe132fc2b38ff50fbd480d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66055423"
---
# <a name="ssis-package-essentials"></a>SSIS 패키지 주요 사항
  패키지는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 기능을 구현하여 데이터를 추출, 변환 및 로드하는 개체입니다. 패키지는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 의 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]디자이너를 사용하여 만들거나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사나 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 연결 프로젝트 마법사를 사용하여 만들 수도 있습니다. 자세한 내용은 [SQL Server Data Tools에서 패키지 만들기](create-packages-in-sql-server-data-tools.md) SSIS 디자이너에서 하 고 [프로젝트 가져오기 마법사](../../2014/integration-services/import-project-wizard.md)합니다.  
  
 기본 패키지에는 다음 요소가 포함됩니다.  
  
 **제어 흐름 요소**  
 이 필수 요소는 다양한 기능을 수행하고 구조를 제공하며 요소의 실행 순서를 제어합니다. 주 제어 흐름 요소는 태스크, 컨테이너 및 선행 제약 조건입니다. 패키지에는 적어도 하나의 제어 흐름 요소가 있어야 합니다.  
  
 자세한 내용은 [Control Flow](control-flow/control-flow.md)을 참조하세요.  
  
 **데이터 흐름 요소**  
 이 선택적 요소는 데이터를 추출하고 수정하며 데이터 원본으로 데이터를 로드합니다. 주 데이터 흐름 요소는 원본, 변환 및 대상입니다. 패키지의 데이터 흐름 요소가 아니어도 됩니다.  
  
 자세한 내용은 [Data Flow](data-flow/data-flow.md)을 참조하세요.  
  
 기본 패키지를 만드는 방법의 예제를 참조 하세요. [1 단원: 프로젝트 및 기본 패키지 만들기](lesson-1-create-a-project-and-basic-package-with-ssis.md)합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [SQL Server Data Tools에서 패키지 만들기](create-packages-in-sql-server-data-tools.md)  
  
-   [제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
-   [태스크 또는 컨테이너의 속성 설정](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
-   [데이터 흐름에서 구성 요소 추가 또는 삭제](data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
## <a name="related-content"></a>관련 내용  
  
1.  MSDN.Microsoft.com의 비디오, [기본 패키지 만들기(SQL Server 비디오)](https://go.microsoft.com/fwlink/?LinkId=131023)  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services&#40;SSIS&#41; 패키지](../../2014/integration-services/integration-services-ssis-packages.md)   
 [선행 제약 조건](control-flow/precedence-constraints.md)  
  
  

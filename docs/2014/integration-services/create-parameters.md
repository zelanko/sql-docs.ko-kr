---
title: 매개 변수를 만들 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.parameterwindow.f1
ms.assetid: cd5d675b-dd5d-49cc-8b1f-dc717a973f99
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 639e31d8ec9282a948a7eda9050cc1a2025ac65e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060139"
---
# <a name="create-parameters"></a>Create Parameters
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 를 사용하여 프로젝트 매개 변수 및 패키지 매개 변수를 만들 수 있습니다. 다음 절차에서는 패키지/프로젝트 매개 변수를 만드는 단계별 지침을 제공합니다.  
  
> [!NOTE]  
>  이전 버전의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 를 사용하여 만든 프로젝트를 프로젝트 배포 모델로 변환하는 경우 **Integration Services 프로젝트 변환 마법사** 를 사용하여 구성에 따라 매개 변수를 만들 수 있습니다. 자세한 내용은 [Deploy Projects to Integration Services Server](../../2014/integration-services/deploy-projects-to-integration-services-server.md)을 참조하세요.  
  
### <a name="to-create-package-parameters"></a>패키지 매개 변수를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 패키지를 열고 SSIS 디자이너에서 **매개 변수** 탭을 클릭합니다.  
  
     ![패키지 매개 변수 탭](media/denali-package-parameters.gif "패키지 매개 변수 탭")  
  
2.  도구 모음에서 **매개 변수 추가** 단추를 클릭합니다.  
  
     ![도구 모음 단추 추가](media/denali-parameter-add.gif "도구 모음 단추 추가")  
  
3.  목록 자체에서 또는 **속성**창에서 **이름**, **데이터 형식**, **값**, **구분** 및 **필수** 속성의 값을 입력합니다. 다음 표에서는 이러한 속성을 설명합니다.  
  
    |속성|Description|  
    |--------------|-----------------|  
    |속성|매개 변수의 이름입니다.|  
    |이름|매개 변수의 데이터 형식입니다.|  
    |기본값|디자인 타임에 할당되는 매개 변수의 기본값입니다. 디자인 기본값이라고도 합니다.|  
    |구분|중요한 매개 변수 값은 카탈로그에서 암호화되고 Transact-SQL 또는 SQL Server Management Studio를 사용하여 볼 경우 NULL 값으로 나타납니다.|  
    |필수|패키지를 실행하기 전에 반드시 지정해야 하는 디자인 기본값 이외의 값입니다.|  
    |Description|유지 관리의 편의를 위한 매개 변수 설명입니다. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 경우 Visual Studio 속성 창의 해당 매개 변수 창에서 매개 변수를 선택할 때 매개 변수 설명을 설정합니다.|  
  
    > [!NOTE]  
    >  프로젝트를 카탈로그에 배포하면 몇 가지 추가 속성이 프로젝트와 연결됩니다. 카탈로그의 모든 매개 변수에 대한 모든 속성을 보려면 [catalog.object_parameters&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database) 뷰를 참조하세요.  
  
4.  프로젝트를 저장하여 매개 변수 변경 내용을 저장합니다. 매개 변수 값은 프로젝트 파일에 저장됩니다.  
  
    > [!WARNING]  
    >  목록에서 직접 편집하거나 **속성** 창을 사용하여 매개 변수 속성의 값을 수정할 수 있습니다. **삭제(X)** 도구 모음 단추를 사용하여 매개 변수를 삭제할 수 있습니다. 마지막 도구 모음 단추를 사용하면 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 패키지를 실행할 때만 사용되는 매개 변수의 값을 지정할 수 있습니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 프로젝트를 열지 않고 패키지 파일을 다시 열면 **매개 변수** 탭이 비어 있고 비활성화된 상태로 나타납니다.  
  
### <a name="to-create-project-parameters"></a>프로젝트 매개 변수를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 **Project.params**를 마우스 오른쪽 단추로 클릭한 다음 **열기**를 클릭하거나 **Project.params**를 두 번 클릭하여 이 항목을 엽니다.  
  
     ![프로젝트 매개 변수 창](media/denali-project-parameters.gif "프로젝트 매개 변수 창")  
  
3.  도구 모음에서 **매개 변수 추가** 단추를 클릭합니다.  
  
     ![도구 모음 단추 추가](media/denali-parameter-add.gif "도구 모음 단추 추가")  
  
4.  **이름**, **데이터 형식**, **값**, **구분**및 **필수** 속성의 값을 입력합니다.  
  
    |속성|Description|  
    |--------------|-----------------|  
    |속성|매개 변수의 이름입니다.|  
    |이름|매개 변수의 데이터 형식입니다.|  
    |기본값|디자인 타임에 할당되는 매개 변수의 기본값입니다. 디자인 기본값이라고도 합니다.|  
    |구분|중요한 매개 변수 값은 카탈로그에서 암호화되고 Transact-SQL 또는 SQL Server Management Studio를 사용하여 볼 경우 NULL 값으로 나타납니다.|  
    |필수|패키지를 실행하기 전에 반드시 지정해야 하는 디자인 기본값 이외의 값입니다.|  
    |Description|유지 관리의 편의를 위한 매개 변수 설명입니다. [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]의 경우 Visual Studio 속성 창의 해당 매개 변수 창에서 매개 변수를 선택할 때 매개 변수 설명을 설정합니다.|  
  
5.  프로젝트를 저장하여 매개 변수 변경 내용을 저장합니다. 매개 변수 값은 프로젝트 파일의 구성에 저장됩니다. 매개 변수 값의 모든 변경 사항을 디스크에 커밋하려면 프로젝트 파일을 저장합니다.  
  
    > [!WARNING]  
    >  목록에서 직접 편집하거나 **속성** 창을 사용하여 매개 변수 속성의 값을 수정할 수 있습니다. **삭제(X)** 도구 모음 단추를 사용하여 매개 변수를 삭제할 수 있습니다. 마지막 도구 모음 단추를 사용하여 **매개 변수 값 관리** 대화 상자를 열면 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 패키지를 실행할 때만 사용되는 매개 변수의 값을 지정할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services &#40;SSIS&#41; 매개 변수](integration-services-ssis-package-and-project-parameters.md)  
  
  

---
title: 원격 파티션-고급 설정 대화 상자 (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.advancedrestoresettings.f1
ms.assetid: a03bb7e1-efaf-47c8-b0ee-f3e4438311cb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1ca3f12ff53c4291d8bbe7c8eb97ce8e47172ea3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070376"
---
# <a name="remote-partitions---advanced-settings-dialog-box-analysis-services---multidimensional-data"></a>원격 파티션 - 고급 설정 대화 상자(Analysis Services - 다차원 데이터)
  
  **의** 원격 파티션 - 고급 설정 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 대화 상자를 사용하여 원격 파티션을 유지 관리하는 원격 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 나타내는 데이터 원본의 연결 문자열과 같은 고급 설정을 편집하는 동시에 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스 복원 **대화 상자를 사용하여 원격 백업 파일에서** 데이터베이스로 원격 파티션을 복원할 수 있습니다. 
  **원격 파티션 - 고급 설정** 대화 상자는 **원격 파티션 복원** 옵션을 선택한 후 원격 파티션에 대한 줄임표 단추( **...** )를 클릭하여**데이터베이스 복원**대화 상자의 **파티션** 페이지에서 표시할 수 있습니다.  
  
## <a name="options"></a>옵션  
  
|용어|정의|  
|----------|----------------|  
|**데이터 원본 이름**|나열된 원격 파티션을 관리하는 원격 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 나타내는 데이터 원본의 이름을 표시합니다.|  
|**백업 파일**|나열된 원격 파티션에 대해 복원될 데이터가 포함된 원격 백업 파일의 이름을 표시합니다.<br /><br /> 참고: **데이터베이스 복원** 대화 상자의 **파티션** 페이지에 있는 **백업 파일** 열에서 원격 백업 파일을 지정한 경우에는 백업 파일이 표시 되지 않습니다.|  
|**연결 문자열**|
  **데이터 원본 이름**에 표시된 데이터 원본에 대한 연결 문자열을 표시합니다.|  
|**편집**|
  **데이터 연결 속성** 대화 상자를 표시하고 연결 문자열에 포함된 속성을 편집하려면 클릭합니다.|  
|**파티션 목록**|원격 파티션을 복원할 다른 위치를 지정하려면 선택합니다. 큐브의 원격 파티션에 대해 기본 위치 이외의 위치를 지정한 경우에만 원격 파티션의 복원 폴더를 변경할 수 있습니다. 이 옵션을 선택하면 활성화되는 다음 표는 각 원격 파티션에 대한 복원 폴더를 지정하는 데 사용됩니다.<br /><br /> **큐브**: 원격 파티션이 포함 된 큐브의 이름을 표시 합니다.<br /><br /> **MeasureGroup**: 원격 파티션이 포함 된 측정값 그룹의 이름을 표시 합니다.<br /><br /> **파티션**: 원격 파티션의 이름을 표시 합니다.<br /><br /> **크기 (mb)**: 원격 파티션의 크기 (mb)를 표시 합니다.<br /><br /> **원본 폴더**: 원격 파티션이 저장 된 원본 폴더의 이름을 표시 합니다.<br /><br /> **복원 폴더**: 원격 파티션에 대 한 복원 폴더의 이름을 입력 하거나 줄임표 단추 (**...**)를 클릭 하 여 **원격 폴더 찾아보기** 대화 상자를 표시 하 고 사용할 폴더의 경로를 선택 합니다. 
  **원격 폴더 찾아보기** 대화 상자에 대한 자세한 내용은 [원격 폴더 찾아보기 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.|  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 디자이너 및 대화 상자 &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [파티션 &#40;데이터베이스 복원 대화 상자&#41; &#40;Analysis Services-다차원 데이터&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Analysis Services 데이터베이스 백업 및 복원](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  

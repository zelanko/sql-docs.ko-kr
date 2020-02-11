---
title: 참조 추가 대화 상자 (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.addreference.f1
- sql12.asvs.bidevstudio.assembly.addassembly.f1
helpviewer_keywords:
- Add Reference dialog box
ms.assetid: 457958c4-6baa-474d-99a0-34c195ceba09
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 541b7371cdc05ee316e9fb9de9f50affc4f14fc7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66062854"
---
# <a name="add-reference-dialog-box-analysis-services---multidimensional-data"></a>참조 추가 대화 상자(Analysis Services - 다차원 데이터)
  
  **의** 참조 추가 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 대화 상자를 사용하여 개발 프로젝트에 [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework 어셈블리 또는 다른 프로젝트에 대한 참조를 추가할 수 있습니다. 
  **솔루션 탐색기** 에서 **프로젝트의** 어셈블리 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 폴더를 마우스 오른쪽 단추로 클릭한 다음 상황에 맞는 메뉴에서 **새 어셈블리 참조** 를 선택하여 **참조 추가** 대화 상자를 표시할 수 있습니다.  
  
## <a name="options"></a>옵션  
  
|용어|정의|  
|----------|----------------|  
|**.NET**|등록된 구성 요소에 대한 참조를 추가하려면 이 탭을 선택합니다. 이 탭에서는 등록된 .NET Framework 구성 요소 목록을 포함하는 표를 표시합니다. 표에서 하나 이상의 항목을 선택한 다음 **추가** 를 클릭하여 선택한 .NET 구성 요소를 **선택한 프로젝트 및 구성 요소**에 추가합니다. 표에는 다음 열이 있습니다.<br /><br /> **구성 요소 이름**: 구성 요소의 전체 또는 "친숙 한" 이름입니다. 제목을 선택하면 구성 요소 이름을 기준으로 정렬합니다.<br /><br /> **버전**: 구성 요소의 나열 된 버전 번호입니다. 제목을 선택하면 버전을 기준으로 정렬합니다.<br /><br /> **런타임**: 구성 요소의 기반이 되는 .NET Framework의 버전입니다. 제목을 선택하면 런타임 버전을 기준으로 정렬합니다.<br /><br /> **경로**: 구성 요소의 파일 이름과 경로가 있는 경로입니다. 제목을 선택하면 경로를 기준으로 정렬합니다.|  
|**찾아보기**|
  **.NET** 또는 **최근에 사용한 파일** 탭에 나열되어 있지 않은 어셈블리를 파일 시스템에서 찾아보려면 클릭합니다. 이 탭에서는 다음 옵션을 표시합니다.<br /><br /> **찾는 위치**:이 드롭다운 목록에서 폴더를 선택 합니다. 이 목록에서 폴더를 선택하면 주 창에 해당 폴더의 내용이 표시됩니다.<br /><br /> **마지막으로 방문한 폴더로 이동**: 이전 위치에 **조회** 를 반환 합니다.<br /><br /> **한 수준 위로**: 계층에서 다음 상위 폴더를 찾습니다.<br /><br /> **새 폴더 만들기**: **찾는 위치**에서 선택한 폴더 아래에 새 자식 폴더를 만들려면 선택 합니다.<br /><br /> **보기 메뉴**: 주 창의 내용 보기를 변경 하려면 선택 합니다.  
  **메뉴 보기**의 옵션에 대한 자세한 내용은 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 설명서의 "파일 및 폴더 보기 개요" 항목을 참조하십시오. 다음 옵션을 사용할 수 있습니다.<br />썸네일<br />타일<br />아이콘<br />목록<br />세부 정보<br /><br /> **주 창**: **찾는 위치**에서 선택한 폴더의 내용을 표시 합니다. 하나 이상의 항목을 선택한 다음 **추가** 를 클릭 하 여 선택한 **제품 및 구성 요소**에 선택한 파일을 추가 합니다. 주 창의 옵션 및 상황에 맞는 메뉴에 대한 자세한 내용은 Windows 설명서의 "파일 및 폴더 보기 개요" 항목을 참조하십시오.<br /><br /> **파일 이름**: 표시 되는 파일과 폴더를 필터링 하려면이 옵션을 사용 합니다. 필터링할 전체 또는 부분 파일 이름을 입력합니다. 별표(\*)를 와일드카드로 사용할 수 있습니다. 여러 파일을 선택하려면 각 파일 이름을 큰따옴표(")로 묶은 다음 공백으로 구분하여 여러 파일 이름을 입력합니다. 드롭다운 목록에서 파일 이름을 선택하여 이전에 검토한 파일을 선택할 수도 있습니다. 팁: **파일 이름**에 URL 또는 네트워크 경로를 입력 하 여 웹 서버 및 네트워크 컴퓨터를 찾을 수 있습니다. 예를 들어 " http://mywebsite "를 입력하면 "mywebsite" 웹 위치에서 사용 가능한 파일이 표시되고 "\\myserver\myshare"를 입력하면 "myserver"의 "myshare" 위치에서 사용 가능한 파일이 표시됩니다.<br /><br /> **파일 형식**: **찾는 위치** 에서 선택한 폴더 또는 디렉터리의 내용을 특정 파일 형식으로 필터링 하려면이 옵션을 사용 합니다.|  
|**문서**|최근에 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 프로젝트에 추가한 구성 요소 참조 목록을 표시합니다. 표에서 하나 이상의 항목을 선택한 다음 **추가** 를 클릭하여 **선택한 프로젝트 및 구성 요소**에 선택한 .NET Framework 어셈블리를 추가합니다. 표에는 다음 열이 있습니다.<br /><br /> **구성 요소 이름**: 구성 요소의 전체 또는 "친숙 한" 이름입니다. 제목을 선택하면 구성 요소 이름을 기준으로 정렬합니다.<br /><br /> **버전**: 구성 요소의 나열 된 버전 번호입니다. 제목을 선택하면 버전을 기준으로 정렬합니다.<br /><br /> **런타임**: 구성 요소의 기반이 되는 .NET Framework의 버전입니다. 제목을 선택하면 런타임 버전을 기준으로 정렬합니다.<br /><br /> **경로**: 구성 요소의 파일 이름과 경로가 있는 경로입니다. 제목을 선택하면 경로를 기준으로 정렬합니다.|  
|**추가**|
  **.NET**, **찾아보기**또는 **최근에 사용한 파일** 탭에서 선택한 구성 요소를 **선택한 프로젝트 및 구성 요소**에 추가하려면 클릭합니다.|  
|**제거**|
  **선택한 프로젝트 및 구성 요소**에서 선택한 구성 요소를 제거하려면 클릭합니다.|  
|**선택한 프로젝트 및 구성 요소**|
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]프로젝트에 추가할 구성 요소 참조 목록을 표시합니다. 표에서 하나 이상의 항목을 선택한 다음 **제거** 를 클릭하여 선택한 구성 요소를 표에서 제거합니다. 표에는 다음 열이 있습니다.<br /><br /> **구성 요소 이름**: 구성 요소의 전체 또는 "친숙 한" 이름입니다. 제목을 선택하면 구성 요소 이름을 기준으로 정렬합니다.<br /><br /> **버전**: 구성 요소의 나열 된 버전 번호입니다. 제목을 선택하면 버전을 기준으로 정렬합니다.<br /><br /> **런타임**: 구성 요소의 기반이 되는 .NET Framework의 버전입니다. 제목을 선택하면 런타임 버전을 기준으로 정렬합니다.<br /><br /> **경로**: 구성 요소의 파일 이름과 경로가 있는 경로입니다. 제목을 선택하면 경로를 기준으로 정렬합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 디자이너 및 대화 상자 &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [다차원 모델 어셈블리 관리](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  

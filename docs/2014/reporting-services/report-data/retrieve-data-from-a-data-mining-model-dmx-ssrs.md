---
title: 데이터 마이닝 모델에서 데이터 검색(DMX)(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- retrieving report data
- datasets [Reporting Services], with DMX queries
- datasets [Reporting Services], Analysis Services
- queries [Reporting Services], data mining prediction
ms.assetid: d9cd3624-1594-4707-8887-55437dd7e07c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4a55d34c86622ef837d9c7264a614ba59552c978
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48089193"
---
# <a name="retrieve-data-from-a-data-mining-model-dmx-ssrs"></a>데이터 마이닝 모델에서 데이터 검색(DMX)(SSRS)
  보고서에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터 마이닝 모델의 데이터를 사용하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터 원본 및 하나 이상의 보고서 데이터 집합을 정의해야 합니다. 데이터 원본 정의를 만들 때는 클라이언트 컴퓨터에서 데이터 원본에 액세스할 수 있도록 연결 문자열 및 자격 증명을 지정해야 합니다.  
  
 단일 보고서에 사용할 포함된 데이터 원본 정의를 만들거나 여러 보고서에 사용할 수 있는 공유 데이터 원본 정의를 만들 수 있습니다. 이 항목의 절차에서는 포함된 데이터 원본을 만드는 방법에 대해 설명합니다. 공유 데이터 원본에 대한 자세한 내용은 [포함된 데이터 연결 및 공유 데이터 연결 또는 데이터 원본&#40;보고서 작성기 및 SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md) 및 [공유 데이터 원본 만들기, 수정 및 삭제&#40;SSRS&#41;](create-modify-and-delete-shared-data-sources-ssrs.md)를 참조하세요.  
  
 만든 후에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터 원본에 하나 이상의 데이터 집합을 만들 수 있습니다. 각 데이터 세트에 대해 DMX(Data Mining Prediction Expression) 쿼리 디자이너를 사용하여 필드 컬렉션을 지정하는 DMX 쿼리를 만듭니다. 자세한 내용은 [Analysis Services DMX 쿼리 디자이너 사용자 인터페이스](analysis-services-dmx-query-designer-user-interface.md)를 참조하세요.  
  
 데이터 세트를 만들면 데이터 세트의 이름이 보고서 데이터 창의 해당 데이터 원본 아래에 노드로 나타납니다.  
  
 보고서를 게시한 후 보고서를 보고서 서버에서 실행할 때 데이터를 검색할 수 있는 권한이 유효하도록 데이터 원본에 대한 자격 증명을 변경해야 할 수도 있습니다.  
  
### <a name="to-create-an-embedded-microsoft-sql-server-analysis-services-data-source"></a>포함된 Microsoft SQL Server Analysis Services 데이터 원본을 만들려면  
  
1.  보고서 데이터 창의 도구 모음에서 **새로 만들기**, **데이터 원본**을 차례로 클릭합니다.  
  
2.  **데이터 원본 속성** 대화 상자의 **이름** 입력란에 이름을 입력하거나 기본 이름을 적용합니다.  
  
3.  **포함된 연결** 이 선택되어 있는지 확인합니다.  
  
4.  **유형** 드롭다운 목록에서 **Microsoft SQL Server Analysis Services**를 선택합니다.  
  
5.  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터 원본에 사용할 연결 문자열을 지정합니다.  
  
     데이터 원본 연결에 사용할 자격 증명 및 연결 정보는 데이터베이스 관리자에게 문의하십시오. 다음 연결 문자열 예에서는 로컬 클라이언트에 있는 [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] 예제 데이터베이스를 지정합니다.  
  
    ```  
    Data Source=localhost;Initial Catalog=AdventureWorksDW2012  
    ```  
  
6.  **자격 증명**을 클릭합니다.  
  
     데이터 원본 연결에 사용할 자격 증명을 설정합니다. 자세한 내용은 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../integration-services/connection-manager/data-sources.md)을 참조하세요.  
  
    > [!NOTE]  
    >  데이터 원본 연결을 테스트하려면 **편집**을 클릭하십시오. 그런 다음 **연결 속성** 대화 상자에서 **연결 테스트**를 클릭하십시오. 테스트에 성공한 경우 "연결 테스트에 성공했습니다"라는 정보 메시지가 표시됩니다. 테스트에 실패할 경우에는 테스트에 성공하지 못한 이유에 대한 자세한 정보가 포함된 경고 메시지가 표시됩니다.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     데이터 원본이 보고서 데이터 창에 나타납니다.  
  
### <a name="to-create-a-dataset-for-a-microsoft-sql-server-analysis-services"></a>Microsoft SQL Server Analysis Services에 대한 데이터 세트를 만들려면  
  
1.  에 **보고서 데이터** 창에 연결 하는 데이터 원본의 이름을 마우스 오른쪽 단추로 클릭는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터 원본 및 클릭 **데이터 집합 추가**합니다.  
  
2.  **데이터 집합 속성** 대화 상자에서 **이름** 입력란에 이름을 입력합니다.  
  
3.  에 **데이터 원본 상자**, 이름에 연결 하는 데이터 원본의 이름 인지 확인는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터 원본입니다.  
  
4.  **쿼리 디자이너** 를 클릭하여 열리는 그래픽 쿼리 디자이너에서 쿼리를 대화형으로 작성합니다. 쿼리 디자이너가 MDX 모드로 열리는 경우 도구 모음에서 **DMX 명령 유형**(![DMX 쿼리 언어 뷰로 변경](../media/rsqdicon-commandtypedmx.gif "DMX 쿼리 언어 뷰로 변경"))을 클릭하여 데이터 마이닝 쿼리 디자이너로 전환합니다. 자세한 내용은 [Analysis Services DMX 쿼리 디자이너 사용자 인터페이스](analysis-services-dmx-query-designer-user-interface.md)를 참조하세요.  
  
     또는 다른 보고서에서 기존 DMX 쿼리를 가져오려면 **가져오기**를 클릭한 다음 DMX 쿼리를 사용하여 .rdl 파일로 이동합니다. .dmx 파일에서 쿼리를 가져올 수는 없습니다.  
  
5.  쿼리를 만들고 실행하여 예제 결과를 본 후 **확인**을 클릭합니다.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     데이터 세트 및 해당 필드 컬렉션이 데이터 원본 노드 아래의 보고서 데이터 창에 표시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [DMX 용 analysis Services 연결 형식 &#40;SSRS&#41;](analysis-services-connection-type-for-dmx-ssrs.md)   
 [데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)   
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  

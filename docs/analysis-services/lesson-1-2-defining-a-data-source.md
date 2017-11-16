---
title: "데이터 원본 정의 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 5a3e83c9-8788-431e-85b0-a68c79377ff3
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3c8256f6029efcb956e68325b134b72fcce452c8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-1-2---defining-a-data-source"></a>단원 1-2-데이터 원본 정의
[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트를 만든 후 일반적으로 프로젝트에 사용할 하나 이상의 데이터 원본을 정의하여 프로젝트 작업을 시작합니다. 데이터 원본을 정의하면 데이터 원본에 연결하는 데 사용할 연결 문자열 정보가 정의됩니다. 자세한 내용은 [데이터 원본 만들기&#40;SSAS 다차원&#41;](../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)를 참조하세요.  
  
다음 태스크에서는 AdventureWorksDWSQLServer2012 예제 데이터베이스를 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 프로젝트의 데이터 원본으로 정의합니다. 이 자습서에서는 이 데이터베이스가 로컬 컴퓨터에 있지만 원본 데이터베이스는 대부분 하나 이상의 원격 컴퓨터에서 호스팅됩니다.  
  
### <a name="to-define-a-new-data-source"></a>새 데이터 원본을 정의하려면  
  
1.  Microsoft Visual Studio 창의 오른쪽에 있는 솔루션 탐색기에서 **데이터 원본**을 마우스 오른쪽 단추로 클릭하고 **새 데이터 원본**을 클릭합니다.  
  
2.  **데이터 원본 마법사** 의 **데이터 원본 마법사 시작**페이지에서 **다음** 을 클릭하여 **연결 정의 방법 선택** 페이지를 엽니다.  
  
3.  **연결 정의 방법 선택** 페이지에서 새 연결, 기존 연결 또는 이전에 정의한 데이터 원본 개체를 기반으로 데이터 원본을 정의할 수 있습니다. 이 자습서에서는 새 연결을 기반으로 데이터 원본을 정의합니다. **기존 연결 또는 새 연결을 사용하여 데이터 원본 만들기** 가 선택되어 있는지 확인한 다음 **새로 만들기**를 클릭합니다.  
  
4.  **연결 관리자** 대화 상자에서 데이터 원본에 대한 연결 속성을 정의합니다. **공급자** 목록 상자에서 **네이티브 OLE DB\SQL Server Native Client 11.0** 이 선택되어 있는지 확인합니다.  
  
    [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 **공급자** 목록에 표시된 다른 공급자도 지원합니다.  
  
5.  **서버 이름** 입력란에 **localhost**를 입력합니다.  
  
    로컬 컴퓨터의 명명된 인스턴스에 연결하려면 **localhost\\<instance name>**를 참조하세요. 로컬 컴퓨터 대신 특정 컴퓨터에 연결하려면 컴퓨터 이름 또는 IP 주소를 입력합니다.  
  
6.  **Windows 인증 사용** 이 선택되어 있는지 확인합니다. **데이터베이스 이름 선택 또는 입력** 목록에서 **AdventureWorksDW2012**를 선택합니다.  
  
7.  **연결 테스트** 를 클릭하여 데이터베이스에 대한 연결을 테스트합니다.  
  
8.  **확인**, **다음**을 차례로 클릭합니다.  
  
9. 마법사의 **가장 정보** 페이지에서 데이터 원본 연결에 사용할 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 의 보안 자격 증명을 정의합니다. 가장은 Windows 인증이 선택된 경우 데이터 원본에 연결하는 데 사용되는 Windows 계정에 영향을 줍니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 OLAP 개체 처리를 위한 가장을 지원하지 않습니다. **서비스 계정 사용**을 선택한 후 **다음**을 클릭합니다.  
  
10. **마법사 완료** 페이지에서 기본 이름인 **Adventure Works DW 2012**를 적용한 다음 **마침** 을 클릭하여 새 데이터 원본을 만듭니다.  
  
> [!NOTE]  
> 데이터 원본을 만든 후 속성을 수정하려면 **데이터 원본** 폴더에서 데이터 원본을 두 번 클릭하여 **데이터 원본 디자이너**에 데이터 원본 속성을 표시합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[데이터 원본 뷰 정의](../analysis-services/lesson-1-3-defining-a-data-source-view.md)  
  
## <a name="see-also"></a>참고 항목  
[데이터 원본 만들기&#40;SSAS 다차원&#41;](../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  


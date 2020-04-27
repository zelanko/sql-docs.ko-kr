---
title: 포함 된 데이터 연결 및 공유 데이터 연결 또는 데이터 원본 (보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- embedded data sources
- shared data sources
- data sources
ms.assetid: f417782c-b85a-4c4d-8a40-839176daba56
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b987dd46f6a60a0d0cadc95cf187566eafa4f527
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109269"
---
# <a name="embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs"></a>포함된 데이터 연결 및 공유 데이터 연결 또는 데이터 원본(보고서 작성기 및 SSRS)
  보고서는 쿼리가 실행되거나 보고서가 처리될 때 데이터 연결을 사용하여 보고서에 대한 데이터를 검색합니다. 기본 제공 데이터 연결 형식 목록에서 선택하여 관계형 데이터베이스, 다차원 데이터베이스, 웹 서비스 또는 다른 데이터 원본에 연결할 수 있습니다. 데이터 연결 설명에는 다음과 같은 용어가 사용됩니다.  
  
-   **데이터 연결** *데이터 원본*이라고도 합니다. 데이터 연결에는 연결 형식에 따라 달라지는 이름 및 연결 속성이 포함되어 있습니다. 기본적으로 데이터 연결에는 자격 증명이 포함되지 않습니다. 데이터 연결은 외부 데이터 원본에서 어떤 데이터를 검색할 것인지 지정하지 않습니다. 이렇게 하려면 데이터 세트를 만들 때 쿼리를 지정합니다.  
  
-   **데이터 원본 정의.** 보고서 데이터 원본의 XML 표현을 포함하는 파일입니다. 보고서를 게시할 때 해당 데이터 원본은 보고서 정의와는 별도로 보고서 서버 또는 SharePoint 사이트에 데이터 원본 정의로 저장됩니다. 예를 들어 보고서 서버 관리자가 연결 문자열이나 자격 증명을 업데이트할 수 있습니다. 기본 보고서 서버의 파일 형식은 .rds입니다. SharePoint 사이트의 파일 형식은 .rsds입니다.  
  
-   **연결 문자열입니다.** 연결 문자열은 데이터 원본에 연결하는 데 필요한 연결 속성의 문자열 버전입니다. 연결 속성은 데이터 연결 형식에 따라 다릅니다. 예를 보려면 [Data Connections, Data Sources, and Connection Strings in Report Builder](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)를 참조하세요.  
  
-   **공유 데이터 원본.** 여러 보고서에서 사용할 수 있도록 보고서 서버 또는 SharePoint 사이트에 제공되는 데이터 원본입니다.  
  
-   **포함된 데이터 원본.** *보고서별 데이터 원본*이라고도 합니다. 보고서에서 정의되어 해당 보고서에서만 사용되는 데이터 원본입니다.  
  
-   **자격 증명.** 자격 증명은 외부 데이터 액세스를 위해 제공해야 하는 인증 정보입니다.  
  
 포함된 데이터 원본과 공유 데이터 원본은 작성,  저장 및 관리되는 방법이 다릅니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
## <a name="shared-data-sources"></a>공유 데이터 원본  
 공유 데이터 원본은 자주 사용하는 데이터 원본이 있는 경우에 유용합니다. 가능한 한 공유 데이터 원본을 사용하는 것이 좋습니다. 공유 데이터 원본을 사용하면 보고서 및 보고서 액세스 관리가 더 쉬울 뿐만 아니라 보고서 및 보고서에서 액세스하는 데이터 원본을 보다 안전하게 유지할 수 있습니다. 공유 데이터 원본이 필요한 경우에는 공유 데이터 원본을 만들어 주도록 시스템 관리자에게 요청하세요.  
  
 보고서 작성기에서는 공유 데이터 원본을 만들 수 없습니다. 보고서 서버에서 공유 데이터 원본을 찾아보고 선택할 수 있습니다. 자세한 내용은 [데이터 연결, 데이터 원본 및 연결 문자열](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)을 참조하세요.  
  
 보고서 디자이너에서는 보고서 서버에 있는 공유 데이터 원본을 찾아볼 수 없습니다. 솔루션 탐색기에서 프로젝트의 일부로 공유 데이터 원본을 만들고 보고서 서버에 배포할지 여부를 선택할 수 있습니다. 사용자 컴퓨터와 보고서 서버에서 필요한 자격 증명의 차이로 인해 로컬에서만 사용하도록 선택할 수도 있습니다. 자세한 내용은 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)을 참조하세요.  
  
 다음 아이콘은 보고서 서버 폴더 계층 구조에서 공유 데이터 원본 항목을 나타냅니다. ![공유 데이터 원본 아이콘](media/hlp-16datasource.png "공유 데이터 원본 아이콘")  
  
## <a name="embedded-data-sources"></a>포함된 데이터 원본  
 포함된 데이터 원본은 보고서 정의에 저장되는 데이터 연결입니다. 포함된 데이터 원본 연결 정보는 해당 정보가 포함된 보고서에서만 사용될 수 있습니다. 포함된 데이터 원본을 정의하고 관리하려면 보고서의 **데이터 원본 속성** 대화 상자를 사용합니다.  
  
##  <a name="comparing-embedded-and-shared-data-sources"></a><a name="Comparing"></a>포함 된 데이터 원본 및 공유 데이터 원본 비교  
 다음 표에는 포함된 데이터 원본과 공유 데이터 원본의 차이점이 요약되어 있습니다.  
  
|설명|포함된<br /><br /> 데이터 원본|Shared<br /><br /> 데이터 원본|  
|-----------------|------------------------------|----------------------------|  
|데이터 연결이 보고서 정의에 포함되어 있습니다.|![사용 가능](media/greencheck.gif "사용 가능")||  
|보고서 서버의 데이터 연결에 대한 포인터가 보고서 정의에 포함되어 있습니다.||![사용 가능](media/greencheck.gif "사용 가능")|  
|보고서 서버에서 관리됩니다.|![사용 가능](media/greencheck.gif "사용 가능")|![사용 가능](media/greencheck.gif "사용 가능")|  
|공유 데이터 세트에 필요합니다.||![사용 가능](media/greencheck.gif "사용 가능")|  
|구성 요소에 필요합니다.||![사용 가능](media/greencheck.gif "사용 가능")|  
  
## <a name="data-source-credentials"></a>데이터 원본 자격 증명  
 자격 증명은 포함된 데이터 원본을 만들거나 쿼리를 실행하거나 보고서 처리 중 데이터를 검색하는 데 사용합니다. 데이터 원본의 소유자는 데이터에 액세스할 때 사용해야 하는 자격 증명의 유형을 결정합니다. 자격 증명은 보고서 서버, SharePoint 사이트 또는 보고서 제작 환경의 로컬 컴퓨터의 데이터 연결과 독립적으로 관리됩니다. 데이터 원본 유형에 따라 자격 증명을 사용자에게 요청하지 않도록 저장하거나 각 사용자에게 자격 증명을 요청하도록 설정할 수 있습니다. 사용자 컴퓨터에 있는 데이터 원본에 연결하는지 보고서 서버에 있는 데이터 원본에 연결하는지에 따라 필요한 자격 증명은 다를 수 있습니다. 자세한 내용은 [Reporting Services의 보고서 작성기 및 데이터 연결, 데이터 원본 및 연결 문자열](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md) [에 자격 증명 지정](../../2014/reporting-services/specify-credentials-in-report-builder.md) 을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 &#40;보고서 작성기 및 SSRS&#41;에 데이터를 추가 합니다.](report-data/report-datasets-ssrs.md)   
 [보고서 작성기 및 SSRS &#40;보고서 제작 개념&#41;](report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [Reporting Services &#40;SSRS&#41;에서 지 원하는 데이터 원본](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [데이터 연결이 나 데이터 원본 &#40;보고서 작성기 및 SSRS를 추가 하 고 확인&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)  
  
  

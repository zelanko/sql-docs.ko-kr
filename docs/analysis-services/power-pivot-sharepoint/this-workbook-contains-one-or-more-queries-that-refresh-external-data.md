---
title: 이 통합 문서를 외부 데이터를 새로 고치는 쿼리가 하나 이상 포함 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d1e16f972a77399aa8f05af86ebf09d84c924b47
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="this-workbook-contains-one-or-more-queries-that-refresh-external-data"></a>이 통합 문서를 외부 데이터를 새로 고치는 쿼리가 하나 이상 포함
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터를 포함하는 Excel 통합 문서의 경우 Excel Services는 연결 정보가 검색되면 이 경고를 표시하고 이 통합 문서에 대해 쿼리를 사용할지 여부를 묻는 메시지를 표시합니다.  
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint|  
|제품 버전|[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11_md](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)]|  
|원인|Excel Services가 데이터를 새로 고칠 때 경고하도록 구성된 경우|  
|메시지 텍스트|이 통합 문서에는 외부 데이터를 새로 고치는 쿼리가 하나 이상 포함되어 있습니다. 악의적인 사용자가 쿼리를 디자인하여 기밀 정보에 액세스하고 다른 사용자에게 이러한 정보를 배포하거나 다른 유해한 작업을 수행할 수 있습니다.<br /><br /> 이 통합 문서의 원본을 신뢰하는 경우 예를 클릭하여 이 통합 문서에서 외부 데이터에 대한 쿼리를 사용합니다. 통합 문서의 출처를 신뢰할 수 있는지 모르는 경우 변경 내용이 통합 문서에 적용되지 않도록 아니요를 클릭합니다.<br /><br /> 이 통합 문서의 외부 데이터에 대한 쿼리를 사용하시겠습니까?|  
  
## <a name="explanation"></a>설명  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 통합 문서에는 Excel에서 데이터를 로드하고 계산하는 외부 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 서버와 통신하는 데 사용하는 포함된 데이터 연결 문자열이 들어 있습니다. 새로 고칠 때 경고가 설정된 경우 Excel 서비스에서 이 연결 문자열을 검색하고 이에 따라 사용자에게 경고를 표시합니다.  
  
 통합 문서의 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 데이터를 필터링하고 조각화하려면 쿼리를 사용해야 합니다. 신뢰하는 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 통합 문서에 대해서만 쿼리를 사용하십시오.  
  
## <a name="user-action"></a>사용자 동작  
 쿼리를 사용하려면 **예** 를 클릭합니다.  
  
 또한 다음과 같이 새로 고칠 때 경고가 더 이상 나타나지 않도록 구성 설정을 변경할 수도 있습니다.  
  
1.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭합니다.  
  
2.  **Excel 서비스 응용 프로그램**을 클릭합니다.  
  
3.  **신뢰할 수 있는 파일 위치**를 클릭합니다.  
  
4.  **http://** 또는 구성할 위치를 클릭합니다.  
  
5.  외부 데이터에서 **새로 고칠 때 경고**확인란의 선택을 취소합니다.  
  
6.  **확인**을 클릭합니다.  
  
 또는 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 통합 문서를 포함하는 사이트에 대한 신뢰할 수 있는 위치를 새로 만든 다음 해당 사이트에 대한 구성 설정을 수정할 수도 있습니다. 자세한 내용은 [중앙 관리에서 파워 피벗 사이트에 대한 신뢰할 수 있는 위치 만들기](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)을 참조하세요.  
  
  

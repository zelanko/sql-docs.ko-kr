---
title: "데이터 연결 추가 및 확인(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1d3b2573-e29d-480d-9dde-d26379c86618
caps.latest.revision: "11"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 663fa0c211e0261a243638116f130565a4778a1a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="add-and-verify-a-data-connection-report-builder-and-ssrs"></a>데이터 연결 추가 및 확인(보고서 작성기 및 SSRS)
  보고서 작성기에서는 보고서 서버에 있는 공유 데이터 원본을 추가하거나 보고서에 대한 포함된 데이터 원본을 만들 수 있습니다. 보고서 디자이너에서 공유 데이터 원본이나 포함된 데이터 원본을 만들고 보고서 서버에 배포할 수 있습니다.  
  
 공유 데이터 원본을 보고서에 추가하려면 보고서 서버로 이동하고 공유 데이터 원본을 선택합니다. 보고서의 공유 데이터 원본은 보고서 서버에 있는 공유 데이터 원본 정의를 가리킵니다.  
  
 포함된 데이터 원본을 만들려면 데이터의 외부 원본에 대한 연결 정보가 있어야 하고 데이터에 액세스하는 데 필요한 사용 권한을 알고 있어야 합니다. 이 정보는 대개 데이터 원본의 소유자가 제공합니다. 연결을 테스트하여 지정된 자격 증명이 충분한지 확인할 수 있습니다.  
  
 자세한 내용은 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34) 및 [보고서 작성기에 자격 증명 지정](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-connection-to-a-shared-data-source-in-report-builder"></a>보고서 작성기에서 공유 데이터 원본에 대한 연결을 만들려면  
  
1.  보고서 데이터 창의 도구 모음에서 **새로 만들기** , **데이터 원본**을 차례로 클릭합니다. **데이터 원본 속성** 대화 상자가 열립니다.  
  
2.  **이름** 입력란에 데이터 원본의 이름을 입력합니다.  
  
    > [!NOTE]  
    >  이 이름은 로컬 보고서 정의에 저장됩니다. 이 이름은 보고서 서버에 있는 공유 데이터 원본의 이름이 아닙니다.  
  
3.  **공유 연결 또는 보고서 모델 사용**을 선택합니다. 최근에 사용된 공유 데이터 원본과 보고서 모델의 목록이 나타납니다. 보고서 서버에서 하나를 선택하려면 **찾아보기** 를 클릭하고 공유 데이터 원본을 사용할 수 있는 보고서 서버의 폴더로 이동합니다.  
  
4.  공유 데이터 원본을 선택한 다음 **열기**를 클릭합니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 데이터 원본이 보고서 데이터 창에 나타납니다.  
  
### <a name="to-verify-a-data-connection"></a>데이터 연결을 확인하려면  
  
1.  보고서 데이터 창의 도구 모음에서 데이터 원본을 두 번 클릭합니다. **데이터 원본 속성** 대화 상자가 열립니다.  
  
2.  **연결 테스트**를 클릭합니다.  
  
3.  연결이 성공적이면 “연결되었습니다.”라는 메시지가 나타납니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  연결이 성공적이지 않으면 "데이터 원본에 연결할 수 없습니다."라는 메시지가 나타납니다.  
  
5.  **자세히**를 클릭하고 표시되는 정보를 사용하여 문제를 해결합니다.  
  
     자세한 내용은 [보고서 작성기에 자격 증명 지정](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)을 참조하세요.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 데이터 집합&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
  
  

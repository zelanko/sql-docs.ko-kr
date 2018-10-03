---
title: 추가 및 확인 데이터 연결이 나 데이터 원본 (보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 1d3b2573-e29d-480d-9dde-d26379c86618
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 60c12e1ea7f184770d07fcd4af42b81ca41d13db
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082020"
---
# <a name="add-and-verify-a-data-connection-or-data-source-report-builder-and-ssrs"></a>데이터 연결이나 데이터 원본 추가 및 확인(보고서 작성기 및 SSRS)
  보고서 작성기에서는 보고서 서버에 있는 공유 데이터 원본을 추가하거나 보고서에 대한 포함된 데이터 원본을 만들 수 있습니다. 보고서 디자이너에서 공유 데이터 원본이나 포함된 데이터 원본을 만들고 보고서 서버에 배포할 수 있습니다.  
  
 공유 데이터 원본을 보고서에 추가하려면 보고서 서버로 이동하고 공유 데이터 원본을 선택합니다. 보고서의 공유 데이터 원본은 보고서 서버에 있는 공유 데이터 원본 정의를 가리킵니다.  
  
 포함된 데이터 원본을 만들려면 데이터의 외부 원본에 대한 연결 정보가 있어야 하고 데이터에 액세스하는 데 필요한 사용 권한을 알고 있어야 합니다. 이 정보는 대개 데이터 원본의 소유자가 제공합니다. 연결을 테스트하여 지정된 자격 증명이 충분한지 확인할 수 있습니다.  
  
 자세한 내용은 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](../data-connections-data-sources-and-connection-strings-in-report-builder.md) 및 [보고서 작성기에 자격 증명 지정](../specify-credentials-in-report-builder.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-reference-to-a-shared-data-source"></a>공유 데이터 원본에 대한 참조를 만들려면  
  
1.  보고서 데이터 창의 도구 모음에서 **새로 만들기** , **데이터 원본**을 차례로 클릭합니다. **데이터 원본 속성** 대화 상자가 열립니다.  
  
2.  **이름** 입력란에 데이터 원본의 이름을 입력합니다.  
  
    > [!NOTE]  
    >  이 이름은 로컬 보고서 정의에 저장됩니다. 이 이름은 보고서 서버에 있는 공유 데이터 원본의 이름이 아닙니다.  
  
3.  **공유 연결 또는 보고서 모델 사용**을 선택합니다. 최근에 사용된 공유 데이터 원본과 보고서 모델의 목록이 나타납니다. 보고서 서버에서 하나를 선택하려면 **찾아보기** 를 클릭하고 공유 데이터 원본을 사용할 수 있는 보고서 서버의 폴더로 이동합니다.  
  
4.  공유 데이터 원본을 선택한 다음 **열기**를 클릭합니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 데이터 원본이 보고서 데이터 창에 나타납니다.  
  
### <a name="to-create-an-embedded-data-source"></a>포함된 데이터 원본을 만들려면  
  
1.  보고서 데이터 창의 도구 모음에서 **새로 만들기**, **데이터 원본**을 차례로 클릭합니다. **데이터 원본 속성** 대화 상자가 열립니다.  
  
2.  **이름** 입력란에 데이터 원본 이름을 입력하거나 기본값을 적용합니다.  
  
3.  **내 보고서에 포함된 연결 사용** 이 선택되어 있는지 확인합니다.  
  
    1.  **연결 형식 선택** 드롭다운 목록에서 데이터 원본 유형(예: **Microsoft SQL Server** 또는 **OLE DB**)을 선택합니다.  
  
    2.  다음 대체 방법 중 하나를 사용하여 연결 문자열을 지정합니다.  
  
    -   **연결 문자열** 입력란에 연결 문자열을 직접 입력합니다. 연결 문자열 예 목록은 참조 하세요 [데이터 연결, 데이터 원본 및 보고서 작성기에서 연결 문자열](../data-connections-data-sources-and-connection-strings-in-report-builder.md)합니다.  
  
    -   식 단추(**fx** )를 클릭하여 연결 문자열로 계산되는 식을 만듭니다. **식** 대화 상자의 식 창에 식을 입력합니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    -   2단계에서 선택한 데이터 원본 유형에 대해 **작성** 을 클릭하여 **연결 속성** 대화 상자를 엽니다.  
  
         **연결 속성** 대화 상자의 필드에 데이터 원본 유형에 대해 적합한 항목을 입력합니다. 연결 속성에는 데이터 원본 유형, 데이터 원본 이름 및 사용할 자격 증명이 포함됩니다. 이 대화 상자에서 값을 지정한 후 **연결 테스트** 를 클릭하여 데이터 원본이 사용 가능한지와 지정한 자격 증명이 올바른지 확인합니다.  
  
4.  **자격 증명**을 클릭합니다.  
  
     이 데이터 원본에 사용할 자격 증명을 지정합니다. 데이터 원본의 소유자는 지원되는 자격 증명 유형을 선택합니다. 경우에 따라 데이터 원본 소유자가 보고서 서버에 공유 데이터 원본을 유지하고 다른 사용자가 사용할 수 있는 자격 증명으로 해당 데이터 원본을 구성할 수 있습니다. 이 정보에 대해서는 데이터 원본 소유자에게 문의하십시오. 자세한 내용은 [보고서 작성기에 자격 증명 지정](../specify-credentials-in-report-builder.md)을 참조하세요.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 데이터 원본이 보고서 데이터 창에 나타납니다.  
  
### <a name="to-verify-a-data-connection"></a>데이터 연결을 확인하려면  
  
1.  보고서 데이터 창의 도구 모음에서 데이터 원본을 두 번 클릭합니다. **데이터 원본 속성** 대화 상자가 열립니다.  
  
2.  **연결 테스트**를 클릭합니다.  
  
3.  연결이 성공적이면 “연결되었습니다.”라는 메시지가 나타납니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  연결이 성공적이지 않으면 "데이터 원본에 연결할 수 없습니다."라는 메시지가 나타납니다.  
  
5.  **자세히**를 클릭하고 표시되는 정보를 사용하여 문제를 해결합니다.  
  
     자세한 내용은 [보고서 작성기에 자격 증명 지정](../specify-credentials-in-report-builder.md)을 참조하세요.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [보고서에 데이터 추가 &#40;보고서 작성기 및 SSRS&#41;](report-datasets-ssrs.md)   
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
  

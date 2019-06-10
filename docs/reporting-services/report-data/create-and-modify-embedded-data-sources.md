---
title: 포함된 데이터 원본 만들기 및 수정 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 1c38c2e8-7a29-4f79-a4a3-85ed2b13723b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0daca68faa97a59b9c98b13ab9ca8f867341917c
ms.sourcegitcommit: 1800fc15075bb17b50d0c18b089d8a64d87ae726
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66500474"
---
# <a name="create-and-modify-embedded-data-sources"></a>포함된 데이터 원본 만들기 및 수정
  포함된 데이터 원본은 보고서 정의에서 정의되고 해당 보고서에서만 사용됩니다.  
  
## <a name="to-create-an-embedded-data-source-in-report-designer"></a>보고서 디자이너에서 포함된 데이터 원본을 만들려면  
  
1.  보고서 데이터 창의 도구 모음에서 **새로 만들기** , **데이터 원본**을 차례로 클릭합니다. **데이터 원본 속성** 대화 상자가 열립니다.  
  
    > [!NOTE]  
    >  보고서 데이터 창이 표시되지 않는 경우 **보기** 메뉴에서 **보고서 데이터** 를 클릭합니다.  
  
2.  **이름** 입력란에 데이터 원본 이름을 입력하거나 기본값을 적용합니다. 데이터 원본 이름은 보고서 내부에서만 사용됩니다. 의미를 명확하게 전달하려면 연결 문자열에서 지정된 데이터베이스의 이름을 데이터 원본 이름에 포함하는 것이 좋습니다.  
  
3.  **포함된 연결** 이 선택되어 있는지 확인하고 다음을 수행합니다.  
  
    1.  **유형** 드롭다운 목록에서 데이터 원본 유형(예: **Microsoft SQL Server** 또는 **OLE DB**)을 선택합니다.  
  
    2.  다음 대체 방법 중 하나를 사용하여 연결 문자열을 지정합니다.  
  
        -   **연결 문자열** 입력란에 연결 문자열을 직접 입력합니다. 연결 문자열 예제 목록은 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 또는 [데이터 연결, 데이터 원본 및 연결 문자열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)을 참조하세요.  
  
        -   식 단추(**fx** )를 클릭하여 연결 문자열로 계산되는 식을 만듭니다. **식** 대화 상자의 식 창에 식을 입력합니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
        -   2단계에서 선택한 데이터 원본 유형에 대해 **편집** 을 클릭하여 **연결 속성** 대화 상자를 엽니다.  
  
             **연결 속성** 대화 상자의 필드에 데이터 원본 유형에 대해 적합한 항목을 입력합니다. 연결 속성에는 데이터 원본 유형, 데이터 원본 이름 및 사용할 자격 증명이 포함됩니다. 이 대화 상자에서 값을 지정한 후 **연결 테스트** 를 클릭하여 데이터 원본이 사용 가능한지와 지정한 자격 증명이 올바른지 확인합니다. 특정 데이터 원본 유형에 대한 자세한 내용은 [외부 데이터 원본의 데이터 추가&#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md)의 항목을 참조하세요.  
  
    3.  **자격 증명**을 클릭합니다.  
  
         이 데이터 원본에 사용할 자격 증명을 지정합니다. 데이터 원본의 소유자는 지원되는 자격 증명 유형을 선택합니다.  
  
4.  새 포함된 데이터 원본이 보고서 데이터 창에 나타납니다.  
  
## <a name="to-create-an-embedded-data-source-in-report-builder"></a>보고서 작성기에서 포함된 데이터 원본을 만들려면  
  
1.  보고서 데이터 창의 도구 모음에서 **새로 만들기**, **데이터 원본**을 차례로 클릭합니다. **데이터 원본 속성** 대화 상자가 열립니다.  
  
2.  **이름** 입력란에 데이터 원본 이름을 입력하거나 기본값을 적용합니다.  
  
3.  **내 보고서에 포함된 연결 사용** 이 선택되어 있는지 확인합니다.  
  
    1.  **연결 형식 선택** 드롭다운 목록에서 데이터 원본 유형(예: **Microsoft SQL Server** 또는 **OLE DB**)을 선택합니다.  
  
    2.  다음 대체 방법 중 하나를 사용하여 연결 문자열을 지정합니다.  
  
        -   **연결 문자열** 입력란에 연결 문자열을 직접 입력합니다. 연결 문자열 예제 목록은 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)을 참조하세요.  
  
        -   식 단추(**fx** )를 클릭하여 연결 문자열로 계산되는 식을 만듭니다. **식** 대화 상자의 식 창에 식을 입력합니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
        -   2단계에서 선택한 데이터 원본 유형에 대해 **작성** 을 클릭하여 **연결 속성** 대화 상자를 엽니다.  
  
             **연결 속성** 대화 상자의 필드에 데이터 원본 유형에 대해 적합한 항목을 입력합니다. 연결 속성에는 데이터 원본 유형, 데이터 원본 이름 및 사용할 자격 증명이 포함됩니다. 이 대화 상자에서 값을 지정한 후 **연결 테스트** 를 클릭하여 데이터 원본이 사용 가능한지와 지정한 자격 증명이 올바른지 확인합니다.  
  
4.  **자격 증명**을 클릭합니다.  
  
     이 데이터 원본에 사용할 자격 증명을 지정합니다. 데이터 원본의 소유자는 지원되는 자격 증명 유형을 선택합니다. 자세한 내용은 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](specify-credential-and-connection-information-for-report-data-sources.md)을 참조하세요.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     데이터 원본이 보고서 데이터 창에 나타납니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](specify-credential-and-connection-information-for-report-data-sources.md)  
  
  

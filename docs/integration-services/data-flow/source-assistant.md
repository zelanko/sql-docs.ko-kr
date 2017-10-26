---
title: "원본 길잡이 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sourceassistant.f1
- sql13.dts.designer.addNewSource.f1
ms.assetid: 5ca9d821-7d61-4727-9133-5f9cb485c7f3
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9b7406edf9f7234db739730473772d77c42399ec
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="source-assistant"></a>원본 길잡이
  원본 길잡이 구성 요소는 원본 구성 요소 및 연결 관리자 만들기를 도와줍니다. 이 구성 요소는 SSIS 도구 상자의 **즐겨찾기** 섹션에 있습니다.  
  
> [!NOTE]  
>  원본 길잡이는 Integration Services 연결 프로젝트 및 해당 마법사를 대체합니다.  
  
## <a name="add-a-source-with-source-assistant"></a>원본 길잡이 원본 추가
원본 길잡이 사용 하 여 새 원본을 추가 하는 단계를 제공 하 고 또한에서 사용할 수 있는 옵션을 나열 하는이 섹션의 **새 원본 추가** 대화 상자를 끌어서 놓으면 원본 길잡이를 SSIS 디자이너에 표시 됩니다.  

1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원본 구성 요소를 추가할 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  SSIS 도구 상자에서 **데이터 흐름** 탭으로 **원본 길잡이** 구성 요소를 끌어 옵니다. **새 원본 추가** 대화 상자가 나타납니다. 다음 섹션에서는 대화 상자에서 사용할 수 있는 옵션에 대해 자세히 설명합니다.  
  
3.  **유형** 목록에서 대상의 유형을 선택합니다.  
  
4.  기존 연결 관리자를 선택는 **연결 관리자** 목록 하거나 선택  **\<새로 만들기 >** 새 연결 관리자를 만듭니다.  
  
5.  기본 연결 관리자를 선택한 경우 **확인** 을 클릭하여 **새 대상 추가** 대화 상자를 닫습니다. 데이터 흐름에 추가된 대상 및 연결 관리자가 표시됩니다.  
  
6.  클릭 하면  **\<새로 만들기 >** 새 연결 관리자를 만들려면 표시 됩니다는 **연결 관리자** 대화 상자는 연결에 대 한 매개 변수를 지정할 수 있습니다. 새 연결 관리자 만들기 작업을 마치면 SSIS 디자이너에 대상 및 연결 관리자가 표시됩니다.  

## <a name="add-new-source-dialog-box"></a>새 원본 추가 대화 상자
다음 표에서에서 사용할 수 있는 옵션은 **새 원본 추가** 대화 상자.  
  
|옵션|Description|  
|------------|-----------------|  
|유형|연결할 원본 유형을 선택합니다.|  
|연결 관리자|기존 연결 관리자를 선택 하거나 클릭  **\<새로 만들기 >** 새 연결 관리자를 만듭니다.|  
|설치된 항목만 표시|설치된 원본만 볼 것인지 여부를 지정합니다.|  
|확인|변경 내용을 저장하고 모든 후속 대화 상자를 열어 추가 옵션을 구성하려면 클릭합니다.| 
  


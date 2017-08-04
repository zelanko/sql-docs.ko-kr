---
title: "플랫 파일 연결 관리자 편집기 (일반 페이지) | Microsoft Docs"
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
- sql13.dts.designer.ffileconnection.general.f1
helpviewer_keywords:
- Flat File Connection Manager Editor
ms.assetid: 77296024-5c1a-4f6a-9665-0b50d45d744c
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6e94228deef3c278239cc9f24026677a175d3a65
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="flat-file-connection-manager-editor-general-page"></a>플랫 파일 연결 관리자 편집기(일반 페이지)
  **플랫 파일 연결 관리자 편집기** 대화 상자의 **일반** 페이지를 사용하여 파일과 데이터 형식을 선택할 수 있습니다. 플랫 파일 연결을 사용하면 패키지를 텍스트 파일에 연결할 수 있습니다.  
  
 플랫 파일 연결 관리자에 대한 자세한 내용은 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)를 참조하십시오.  
  
## <a name="options"></a>옵션  
 **연결 관리자 이름**  
 워크플로의 플랫 파일 연결에 고유한 이름을 지정합니다. 제공한 이름은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
 **Description**  
 연결에 대한 설명을 입력합니다. 해당 연결의 용도를 설명하여 패키지를 이해하기 쉽고 유지 관리하기 편하도록 만드는 것이 가장 좋습니다.  
  
 **파일 이름**  
 플랫 파일 연결에 사용할 경로와 파일 이름을 입력합니다.  
  
 **찾아보기**  
 플랫 파일 연결에 사용할 파일 이름을 찾습니다.  
  
 **로캘**  
 정렬과 날짜 및 시간 형식에 사용할 언어별 정보를 제공하는 로캘을 지정합니다.  
  
 **유니코드**  
 유니코드를 사용할지 여부를 나타냅니다. 유니코드를 사용하면 코드 페이지를 지정할 수 없습니다.  
  
 **코드 페이지**  
 비유니코드 텍스트에 대한 코드 페이지를 지정합니다.  
  
 **형식**  
 구분 기호로 분리됨, 고정 폭, 왼쪽 정렬 중 어떤 형식을 사용할지를 지정합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|구분 기호로 분리됨|**열** 페이지에 지정된 구분 기호로 열을 구분합니다.|  
|고정 폭|열에 고정 폭이 지정됩니다.|  
|왼쪽 정렬|왼쪽 정렬 파일은 마지막 열을 제외한 모든 열에 고정 폭이 지정된 파일입니다. 마지막 열은 행 구분 기호로 구분됩니다.|  
  
 **텍스트 한정자**  
 사용할 텍스트 한정자를 지정합니다. 예를 들어 텍스트 필드를 따옴표로 묶도록 지정할 수 있습니다.  
  
> [!NOTE]  
>  텍스트 한정자를 선택한 후에는 **없음** 옵션을 다시 선택할 수 없습니다. 텍스트 한정자의 선택을 취소하려면 **없음** 을 입력합니다.  
  
 **머리글 행 구분 기호**  
 구분 기호 목록에서 머리글 행 구분 기호를 선택하거나 구분 기호 텍스트를 입력합니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**{CR}{LF}**|머리글 행을 캐리지 리턴-줄 바꿈 조합으로 구분합니다.|  
|**{CR}**|머리글 행을 캐리지 리턴으로 구분합니다.|  
|**{LF}**|머리글 행을 줄 바꿈으로 구분합니다.|  
|**세미콜론 {;}**|머리글 행을 세미콜론으로 구분합니다.|  
|**콜론 {:}**|머리글 행을 콜론으로 구분합니다.|  
|**쉼표 {,}**|머리글 행을 쉼표로 구분합니다.|  
|**탭 {t}**|머리글 행을 탭으로 구분합니다.|  
|**세로 막대{&#124;}**|머리글 행을 세로 막대로 구분합니다.|  
  
 **건너뛸 머리글 행**  
 건너뛸 머리글 행 또는 초기 데이터 행 수를 지정합니다(있는 경우).  
  
 **첫 번째 데이터 행의 열 이름**  
 첫 번째 데이터 행에 열 이름을 제공할지 여부를 나타냅니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [플랫 파일 연결 관리자 편집기 &#40; 열 페이지 &#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)   
 [플랫 파일 연결 관리자 편집기 &#40; 고급 페이지 &#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)   
 [플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)  
  
  

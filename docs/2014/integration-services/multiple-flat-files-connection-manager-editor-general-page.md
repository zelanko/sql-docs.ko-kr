---
title: 다중 플랫 파일 연결 관리자 편집기 (일반 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multifile.general.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: 00129d43-2772-413b-bdf8-ac5de81cf4a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8d1932d314e8d2c1eb48526d87246da2051bc3b5
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58391641"
---
# <a name="multiple-flat-files-connection-manager-editor-general-page"></a>다중 플랫 파일 연결 관리자 편집기(일반 페이지)
  **다중 플랫 파일 연결 관리자 편집기** 대화 상자의 **일반** 페이지를 사용하여 데이터 형식이 같은 파일 그룹을 선택하고 데이터 형식을 지정할 수 있습니다. 다중 플랫 파일 연결 기능을 사용하면 패키지를 같은 형식의 텍스트 파일 그룹에 연결할 수 있습니다.  
  
 다중 플랫 파일 연결 관리자에 대한 자세한 내용은 [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md)를 참조하십시오.  
  
## <a name="options"></a>변수  
 **연결 관리자 이름**  
 워크플로에서의 다중 플랫 파일 연결에 대한 고유 이름을 지정합니다. 제공한 이름은 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
 **설명**  
 연결에 대한 설명을 입력합니다. 해당 연결의 용도를 설명하여 패키지를 이해하기 쉽고 유지 관리하기 편하도록 만드는 것이 가장 좋습니다.  
  
 **파일 이름**  
 다중 플랫 파일 연결에 사용할 경로와 파일 이름을 입력합니다. "C:\\*.txt"와 같이 와일드카드 문자를 사용하거나 파일 이름을 구분하는 세로줄 문자(|)를 사용하여 다중 파일을 지정할 수 있습니다. 모든 파일의 데이터 형식은 동일해야 합니다.  
  
 **찾아보기**  
 다중 플랫 파일 연결에 사용할 파일 이름을 찾습니다. 여러 파일을 선택할 수 있습니다. 모든 파일의 데이터 형식은 동일해야 합니다.  
  
 **로캘**  
 정렬 순서와 날짜 및 시간 변환 정보를 제공하는 지역을 지정합니다.  
  
 **유니코드**  
 유니코드를 사용할지 여부를 나타냅니다. 유니코드를 사용하면 코드 페이지를 지정할 수 없습니다.  
  
 **코드 페이지**  
 비유니코드 텍스트에 대한 코드 페이지를 지정합니다.  
  
 **형식**  
 구분 기호로 분리됨, 고정 폭, 왼쪽 정렬 중 어떤 서식을 사용할지를 지정합니다. 모든 파일의 데이터 형식은 동일해야 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|구분 기호로 분리됨|**열** 페이지에 지정된 구분 기호로 열을 구분합니다.|  
|고정 폭|열에 고정 폭이 지정됩니다. 폭은 **열** 페이지의 표식 줄을 끌어 지정할 수 있습니다.|  
|왼쪽 정렬|왼쪽 정렬 파일은 마지막 열을 제외한 모든 열에 고정 폭이 지정된 파일입니다. 마지막 열은 **열** 페이지에서 지정한 행 구분 기호로 구분됩니다.|  
  
 **텍스트 한정자**  
 사용할 텍스트 한정자를 지정합니다. 예를 들어 텍스트 필드를 따옴표로 묶도록 지정할 수 있습니다.  
  
 **머리글 행 구분 기호**  
 구분 기호 목록에서 머리글 행 구분 기호를 선택하거나 구분 기호 텍스트를 입력합니다.  
  
|값|Description|  
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
 건너뛸 머리글 행 수를 지정합니다(있는 경우).  
  
 **첫 번째 데이터 행의 열 이름**  
 첫 번째 데이터 행에 열 이름을 제공할지 여부를 나타냅니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [다중 플랫 파일 연결 관리자 편집기&#40;열 페이지&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)   
 [다중 플랫 파일 연결 관리자 편집기&#40;고급 페이지&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)   
 [다중 플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  

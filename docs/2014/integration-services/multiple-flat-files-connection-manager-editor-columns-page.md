---
title: 다중 플랫 파일 연결 관리자 편집기 (열 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multifile.columns.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: ad0cb668-0df2-4d4e-9a20-d20692a0b67a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b44fe16f89e154c1008c73400a6815e9e548bb69
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057503"
---
# <a name="multiple-flat-files-connection-manager-editor-columns-page"></a>다중 플랫 파일 연결 관리자 편집기(열 페이지)
  **다중 플랫 파일 연결 관리자 편집기** 대화 상자의 **열** 노드를 사용하여 행 정보 및 열 정보를 지정하고 선택한 첫 번째 파일을 미리 볼 수 있습니다.  
  
 다중 플랫 파일 연결 관리자에 대한 자세한 내용은 [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md)를 참조하십시오.  
  
## <a name="static-options"></a>정적 옵션  
 **연결 관리자 이름**  
 워크플로에서의 다중 플랫 파일 연결에 대한 고유 이름을 지정합니다. 제공한 이름은 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
 **설명**  
 연결에 대한 설명을 입력합니다. 해당 연결의 용도를 설명하여 패키지를 이해하기 쉽고 유지 관리하기 편하도록 만드는 것이 가장 좋습니다.  
  
## <a name="flat-file-format-dynamic-options"></a>플랫 파일 형식 동적 옵션  
  
### <a name="format--delimited"></a>형식 = 구분 기호로 분리됨  
 **행 구분 기호**  
 사용 가능한 행 구분 기호의 목록에서 선택하거나 구분 기호 텍스트를 입력합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|행이 캐리지 리턴-줄 바꿈 조합으로 구분됩니다.|  
|**{CR}**|행이 캐리지 리턴으로 구분됩니다.|  
|**{LF}**|행이 줄 바꿈으로 구분됩니다.|  
|**세미콜론 {;}**|행이 세미콜론으로 구분됩니다.|  
|**콜론 {:}**|행이 콜론으로 구분됩니다.|  
|**쉼표 {,}**|행이 쉼표로 구분됩니다.|  
|**탭 {t}**|행이 탭으로 구분됩니다.|  
|**세로 막대{&#124;}**|행이 세로 막대로 구분됩니다.|  
  
 **열 구분 기호**  
 사용 가능한 열 구분 기호의 목록에서 선택하거나 구분 기호 텍스트를 입력합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|열이 캐리지 리턴-줄 바꿈 조합으로 구분됩니다.|  
|**{CR}**|열이 캐리지 리턴으로 구분됩니다.|  
|**{LF}**|열이 줄 바꿈으로 구분됩니다.|  
|**세미콜론 {;}**|열이 세미콜론으로 구분됩니다.|  
|**콜론 {:}**|열이 콜론으로 구분됩니다.|  
|**쉼표 {,}**|열이 쉼표로 구분됩니다.|  
|**탭 {t}**|열이 탭으로 구분됩니다.|  
|**세로 막대{&#124;}**|열이 세로 막대로 구분됩니다.|  
  
 **열 다시 설정**  
 **열 다시 설정**을 클릭하여 원래 열을 제외한 모든 열을 제거합니다.  
  
### <a name="format--fixed-width"></a>형식 = 고정 폭  
 **글꼴**  
 미리 보기 데이터를 표시할 글꼴을 선택합니다.  
  
 **원본 데이터 열**  
 세로 행 표식을 밀어 행 너비를 조정하고 미리 보기 창의 맨 위에 있는 눈금자를 클릭하여 열 너비를 조정합니다.  
  
 **행 너비**  
 개별 열의 구분 기호를 추가하기 전에 행 길이를 지정합니다. 또는 미리 보기 창에서 세로줄을 끌어 행의 끝을 표시합니다. 행 너비 값이 자동으로 업데이트됩니다.  
  
 **열 다시 설정**  
 **열 다시 설정**을 클릭하여 원래 열을 제외한 모든 열을 제거합니다.  
  
### <a name="format--ragged-right"></a>형식 = 왼쪽 정렬  
  
> [!NOTE]  
>  왼쪽 정렬 파일에서는 마지막 열을 제외한 모든 열에 고정 폭이 지정됩니다. 마지막 열은 행 구분 기호로 구분됩니다.  
  
 **글꼴**  
 미리 보기 데이터를 표시할 글꼴을 선택합니다.  
  
 **원본 데이터 열**  
 세로 행 표식을 밀어 행 너비를 조정하고 미리 보기 창의 맨 위에 있는 눈금자를 클릭하여 열 너비를 조정합니다.  
  
 **행 구분 기호**  
 사용 가능한 행 구분 기호의 목록에서 선택하거나 구분 기호 텍스트를 입력합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|행이 캐리지 리턴-줄 바꿈 조합으로 구분됩니다.|  
|**{CR}**|행이 캐리지 리턴으로 구분됩니다.|  
|**{LF}**|행이 줄 바꿈으로 구분됩니다.|  
|**세미콜론 {;}**|행이 세미콜론으로 구분됩니다.|  
|**콜론 {:}**|행이 콜론으로 구분됩니다.|  
|**쉼표 {,}**|행이 쉼표로 구분됩니다.|  
|**탭 {t}**|행이 탭으로 구분됩니다.|  
|**세로 막대{&#124;}**|행이 세로 막대로 구분됩니다.|  
  
 **열 다시 설정**  
 **열 다시 설정**을 클릭하여 원래 열을 제외한 모든 열을 제거합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [다중 플랫 파일 연결 관리자 편집기&#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [다중 플랫 파일 연결 관리자 편집기&#40;고급 페이지&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)   
 [다중 플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  

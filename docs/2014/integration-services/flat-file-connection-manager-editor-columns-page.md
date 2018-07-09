---
title: 플랫 파일 연결 관리자 편집기 (열 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ffileconnection.columns.f1
helpviewer_keywords:
- Flat File Connection Manager Editor
ms.assetid: 40ce7537-abd0-4973-97fd-6ccb90fddfa0
caps.latest.revision: 20
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 166393522090c1d5c0455104c0d046319741f2b4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37240959"
---
# <a name="flat-file-connection-manager-editor-columns-page"></a>플랫 파일 연결 관리자 편집기(열 페이지)
  **플랫 파일 연결 관리자 편집기** 대화 상자의 **열** 페이지를 사용하여 행 및 열 정보를 지정하고 파일을 미리 볼 수 있습니다.  
  
 플랫 파일 연결 관리자에 대한 자세한 내용은 [Flat File Connection Manager](connection-manager/file-connection-manager.md)를 참조하십시오.  
  
## <a name="static-options"></a>정적 옵션  
 **연결 관리자 이름**  
 워크플로의 플랫 파일 연결에 고유한 이름을 지정합니다. 제공한 이름은 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
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
  
 **새로 고침**  
 **새로 고침**을 클릭하여 건너뛸 구분 기호의 변경 결과를 검토합니다. 이 단추는 다른 연결 옵션을 변경한 후에만 표시됩니다.  
  
 **행 미리 보기**  
 선택한 옵션을 사용하여 열과 행으로 구분된 플랫 파일로 샘플 데이터를 표시합니다.  
  
 **열 다시 설정**  
 **열 다시 설정**을 클릭하여 원래 열을 제외한 모든 열을 제거합니다.  
  
### <a name="format--fixed-width"></a>형식 = 고정 폭  
 **글꼴**  
 미리 보기 데이터를 표시할 글꼴을 선택합니다.  
  
 **원본 데이터 열**  
 빨간색 세로 행 표식을 밀어 행 너비를 조절하고 미리 보기 창의 맨 위에 있는 눈금자를 클릭하여 열 너비를 조절합니다.  
  
 **행 너비**  
 개별 열의 구분 기호를 추가하기 전에 행 길이를 지정합니다. 또는 미리 보기 창에서 빨간색 세로줄을 끌어 행의 끝을 표시합니다. 행 너비 값이 자동으로 업데이트됩니다.  
  
 **열 다시 설정**  
 **열 다시 설정**을 클릭하여 원래 열을 제외한 모든 열을 제거합니다.  
  
### <a name="format--ragged-right"></a>형식 = 왼쪽 정렬  
  
> [!NOTE]  
>  왼쪽 정렬 파일은 마지막 열을 제외한 모든 열에 고정 폭이 지정된 파일입니다. 마지막 열은 행 구분 기호로 구분됩니다.  
  
 **글꼴**  
 미리 보기 데이터를 표시할 글꼴을 선택합니다.  
  
 **원본 데이터 열**  
 빨간색 세로 행 표식을 밀어 행 너비를 조절하고 미리 보기 창의 맨 위에 있는 눈금자를 클릭하여 열 너비를 조절합니다.  
  
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
 [플랫 파일 연결 관리자 편집기 &#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [플랫 파일 연결 관리자 편집기 &#40;고급 페이지&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)   
 [플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)  
  
  

---
title: 다중 플랫 파일 연결 관리자 편집기 (고급 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multifile.advanced.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: fc883131-c03d-4ab3-8220-b51cbe243a82
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4e67507aa23e29f7a0f6d675538f254fbf41f76d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58391739"
---
# <a name="multiple-flat-files-connection-manager-editor-advanced-page"></a>다중 플랫 파일 연결 관리자 편집기(고급 페이지)
  **다중 플랫 파일 연결 관리자 편집기** 대화 상자의 **고급** 페이지를 사용하여 플랫 파일 연결 관리자에서 연결하는 텍스트 파일에 있는 각 열의 데이터 형식 및 구분 기호와 같은 속성을 설정할 수 있습니다.  
  
 기본적으로 문자열 열의 길이는 50자입니다. 샘플 데이터를 평가한 다음 자동으로 이러한 열의 길이를 조정하여 데이터 잘림이나 열 너비 초과를 방지할 수 있습니다. 또한 대상 열과의 호환성을 위해 다른 메타데이터를 업데이트할 수 있습니다. 예를 들어 정수 데이터만 포함하는 열의 데이터 형식을 DT_I2와 같은 숫자 데이터 형식으로 변경할 수 있습니다.  
  
 다중 플랫 파일 연결 관리자에 대한 자세한 내용은 [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md)를 참조하십시오.  
  
## <a name="options"></a>변수  
 **연결 관리자 이름**  
 워크플로에서의 다중 플랫 파일 연결 관리자에 대한 고유 이름을 지정합니다. 제공한 이름은 **디자이너의** 연결 관리자 [!INCLUDE[ssIS](../includes/ssis-md.md)] 영역에 표시됩니다.  
  
 **설명**  
 연결 관리자에 대한 설명을 입력합니다. 설명에 해당 연결 관리자의 용도를 정의하면 패키지를 이해하기 쉬우며 유지 관리가 간편합니다.  
  
 **각 열의 속성을 구성하십시오.**  
 왼쪽 창에서 열을 선택하면 오른쪽 창에 해당 속성이 표시됩니다. 데이터 형식 속성에 대한 설명은 다음 표를 참조하십시오. 나열된 일부 속성은 일부 플랫 파일 형식에 대해서만 구성 가능합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**ColumnType**|열 유형이 구분 기호로 분리됨, 고정 폭 또는 왼쪽 정렬 중 어떤 것인지를 나타냅니다. 이 속성은 읽기 전용입니다. 왼쪽 정렬 파일은 마지막 열을 제외한 모든 열에 고정 폭이 지정된 파일입니다. 마지막 열은 행 구분 기호로 종료됩니다.|  
|**OutputColumnWidth**|저장할 값을 바이트 수로 지정합니다. 유니코드 파일의 경우 문자 수로 표시됩니다. 데이터 흐름 태스크에서 이 값은 플랫 파일 원본의 출력 열 너비를 설정하는 데 사용됩니다.<br /><br /> 참고: 개체 모델에서 이 속성의 이름은 MaximumWidth입니다.|  
|**DataType**|사용 가능한 데이터 형식의 목록에서 선택합니다. 자세한 내용은 [Integration Services Data Types](data-flow/integration-services-data-types.md)을 참조하세요.|  
|**TextQualified**|텍스트 한정자를 사용하여 텍스트 데이터를 한정할지 여부를 나타냅니다. 유효한 값은<br /><br /> **True**: 플랫 파일의 텍스트 데이터가 한정됩니다.<br /><br /> **False**: 플랫 파일의 텍스트 데이터가 한정되지 않습니다.|  
|**이름**|열 이름을 지정합니다. 기본값은 열 번호 매기기 목록이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.|  
|**DataScale**|숫자 데이터의 소수 자릿수를 지정합니다. 소수 자릿수란 소수점 이하 자릿수를 말합니다. 자세한 내용은 [Integration Services Data Types](data-flow/integration-services-data-types.md)을 참조하세요.|  
|**ColumnDelimiter**|사용 가능한 열 구분 기호의 목록에서 선택합니다. 텍스트에 거의 사용되지 않는 구분 기호를 선택합니다. 고정 폭 열에 대해서는 이 값이 무시됩니다.<br /><br /> **{CR}{LF}** – 열이 캐리지 리턴-줄 바꿈 조합으로 구분됩니다.<br /><br /> **{CR}** – 열이 캐리지 리턴으로 구분됩니다.<br /><br /> **{LF}** – 열이 줄 바꿈으로 구분됩니다.<br /><br /> **세미콜론{;}** – 열이 세미콜론으로 구분됩니다.<br /><br /> **콜론{:}** – 열이 콜론으로 구분됩니다.<br /><br /> **쉼표 {,}** – 열이 쉼표로 구분됩니다.<br /><br /> **탭{t}** – 열이 탭으로 구분됩니다.<br /><br /> **세로 막대{&#124;}** – 열이 세로 막대로 구분됩니다.|  
|**DataPrecision**|숫자 데이터의 전체 자릿수를 지정합니다. 전체 자릿수란 숫자의 자릿수를 말합니다. 자세한 내용은 [Integration Services Data Types](data-flow/integration-services-data-types.md)을 참조하세요.|  
|**InputColumnWidth**|저장할 값을 바이트 수로 지정합니다. 유니코드 파일의 경우 문자 수로 표시됩니다. 구분 기호로 분리된 열에 대해서는 이 값이 무시됩니다.<br /><br /> **참고** 개체 모델에서 이 속성의 이름은 ColumnWidth입니다.|  
  
 **새로 만들기**  
 **새로 만들기**를 클릭하여 새 열을 추가합니다. 기본적으로 **새로 만들기** 단추는 목록 끝에 새 열을 추가합니다. 이 단추의 드롭다운 목록에서 다음 옵션도 사용할 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**열 추가**|목록 끝에 새 열을 추가합니다.|  
|**앞에 삽입**|선택한 열 앞에 새 열을 삽입합니다.|  
|**뒤에 삽입**|선택한 열 뒤에 새 열을 삽입합니다.|  
  
 **Delete**  
 열을 선택한 다음 **삭제**를 클릭하여 제거합니다.  
  
 **유형 제안**  
 **열 유형 제안** 대화 상자를 사용하여 첫 번째로 선택한 파일에 있는 샘플 데이터를 평가하고 각 열의 데이터 형식과 길이에 대한 제안을 가져올 수 있습니다. 자세한 내용은 [열 유형 제안 대화 상자 UI 참조](connection-manager/suggest-column-types-dialog-box-ui-reference.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [다중 플랫 파일 연결 관리자 편집기&#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [다중 플랫 파일 연결 관리자 편집기&#40;열 페이지&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)   
 [다중 플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  

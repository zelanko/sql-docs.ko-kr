---
title: 상태 변수 정의 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 45d66152-883a-49a7-a877-2e8ab45f8f79
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 786d9b2e0d3a3f00d3f9e00496d8a11e9d2c18c1
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35402995"
---
# <a name="define-a-state-variable"></a>상태 변수 정의
  이 절차에서는 CDC 상태가 저장되는 패키지 변수를 정의하는 방법을 설명합니다.  
  
 CDC 상태 변수는 CDC 제어 태스크에 의해 로드, 초기화 및 업데이트되고 변경 레코드의 현재 처리 범위를 결정하기 위해 CDC 원본 데이터 흐름 구성 요소에 사용됩니다. CDC 상태 변수는 CDC 제어 태스크 및 CDC 원본에 공통되는 모든 컨테이너에 정의할 수 있습니다. 이는 패키지 수준에 있을 수 있지만 루프 컨테이너와 같은 다른 컨테이너에 있을 수도 있습니다.  
  
 수동으로 CDC 상태 변수 값을 수정하는 것은 좋지 않지만 해당 내용을 이해하는 데에는 유용할 수 있습니다.  
  
 다음 표에서는 CDC 상태 변수 값의 구성 요소를 자세히 설명합니다.  
  
|구성 요소|설명|  
|---------------|-----------------|  
|**\<상태 이름 >**|현재 CDC 상태의 이름입니다.|  
|**CS**|이렇게 하면 현재 처리 범위 시작점(현재 시작)이 표시됩니다.|  
|**\<cs-lsn>**|이전 CDC 실행 시 마지막으로 처리된 LSN(로그 시퀀스 번호)입니다.|  
|**CE**|이렇게 하면 현재 처리 범위 끝점(현재 끝)이 표시됩니다. CDC 상태에 CE 구성 요소가 있으면 CDC 패키지가 현재 처리 중이거나 해당 CDC 패키지에서 CDC 처리 범위를 완전히 처리하기 전에 실패했음을 나타냅니다.|  
|**\<ce-lsn>**|현재 CDC 실행 시 마지막으로 처리된 LSN입니다. 항상 처리할 마지막 시퀀스 번호를 최대값(0xFFF…)으로 가정합니다.|  
|**IR**|이렇게 하면 초기 처리 범위가 표시됩니다.|  
|**\<ir-start>**|초기 로드가 시작되기 직전 변경 내용의 LSN입니다.|  
|**\<ir-end>**|초기 로드가 끝난 직후 변경 내용의 LSN입니다.|  
|**TS**|이렇게 하면 마지막 CDC 상태 업데이트의 타임 스탬프가 표시됩니다.|  
|**\<timestamp>**|System.DateTime.UtcNow 속성인 64비트의 10진수 표현입니다.|  
|**ER**|마지막 작업이 실패했을 때 표시되며 오류의 원인에 대한 간단한 설명이 포함되어 있습니다. 이 구성 요소가 있으면 항상 마지막에 표시됩니다.|  
|**\<short-error-text>**|간단한 오류 설명입니다.|  
  
 LSN 및 시퀀스 번호는 LSN 값을 Binary(10)로 표현하는 최대 20자리의 16진수 문자열로 각각 인코딩됩니다.  
  
 다음 표에는 가능한 CDC 상태 값에 대한 설명이 나와 있습니다.  
  
|State|설명|  
|-----------|-----------------|  
|(INITIAL)|현재 CDC 그룹에서 패키지가 실행되기 전의 초기 상태입니다. CDC 상태가 비어 있을 때의 상태이기도 합니다.|  
|ILSTART(초기 로드 시작)|CDC 제어 태스크에 대한 **MarkInitialLoadStart** 작업 호출 이후 초기 로드 패키지를 시작할 때의 상태입니다.|  
|ILEND(초기 로드 종료)|CDC 제어 태스크에 대한 **MarkInitialLoadEnd** 작업 호출 이후 초기 로드 패키지가 성공적으로 끝날 때의 상태입니다.|  
|ILUPDATE(초기 로드 업데이트)|초기 처리 범위를 처리 중인 동안 초기 로드 이후에 trickle feed 업데이트 패키지를 실행할 때의 상태입니다. CDC 제어 태스크에 대한 **GetProcessingRange** 작업 호출 이후에 발생합니다.<br /><br /> __$reprocessing 열을 사용하는 경우 이 상태는 패키지가 이미 대상에 있는 행을 다시 처리하고 있을 수 있음을 나타내는 1로 설정됩니다.|  
|TFEND(Trickle-Feed 업데이트 종료)|일반 CDC 실행에 대해 예상되는 상태입니다. 이 상태는 이전 실행이 성공적으로 완료되었으며 새 처리 범위를 사용한 새 실행을 시작할 수 있음을 나타냅니다.|  
|TFSTART|이 상태는 CDC 제어 태스크에 대한 **GetProcessingRange** 작업 호출 이후에 trickle feed 업데이트 패키지를 처음 실행하는 것이 아닌 두 번째 실행부터 발생하는 상태입니다.<br /><br /> 이 상태는 일반 CDC 실행이 시작되었지만 종료되지 않았거나 아직 확실하게 종료되지 않았음을 나타냅니다(**MarkProcessedRange**).|  
|TFREDO(Trickle-Feed 업데이트 다시 처리)|이 상태는 TFSTART 실행 후 **GetProcessingRange** 에서 발생하는 상태입니다. 이 상태는 이전 실행이 성공적으로 완료되지 않았음을 나타냅니다.<br /><br /> __$reprocessing 열을 사용하는 경우 이 상태는 패키지가 이미 대상에 있는 행을 다시 처리하고 있을 수 있음을 나타내는 1로 설정됩니다.|  
|ERROR|CDC 그룹이 ERROR 상태에 있습니다.|  
  
 다음은 CDC 상태 변수 값의 예입니다.  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   TFEND/CS/0x0000025B000001BC0003/TS/2011-07-17T12:05:58.1001145/  
  
-   TFSTART/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:43.9344900/  
  
-   TFREDO/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:59.5544900/  
  
### <a name="to-define-a-cdc-state-variable"></a>CDC 상태 변수를 정의하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 변수를 정의해야 하는 CDC 흐름이 있는 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 패키지를 엽니다.  
  
2.  **패키지 탐색기** 탭을 클릭하고 새 변수를 추가합니다.  
  
3.  상태 변수로 인식할 수 있는 이름을 변수에 지정합니다.  
  
4.  변수에 **문자열** 데이터 형식을 지정합니다.  
  
 변수 정의의 일환으로 변수에 값을 지정하지 마십시오. 값은 CDC 제어 태스크에 의해 설정되어야 합니다.  
  
 **자동 상태 지속**과 함께 CDC 제어 태스크를 사용하려는 경우 CDC 상태 변수는 사용자가 지정하는 데이터베이스 상태 테이블에서 읽히고 해당 값이 변경될 때 동일한 테이블로 다시 업데이트됩니다. 상태 테이블에 대한 자세한 내용은 [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md)및 [CDC Control Task Editor](../../integration-services/control-flow/cdc-control-task-editor.md)를 참조하십시오.  
  
 자동 상태 지속과 함께 CDC 제어 태스크를 사용하지 않는 경우에는 패키지가 마지막으로 실행되었을 때 변수 값이 저장된 영구 저장소에서 해당 값을 로드하고 현재 처리 범위에 대한 처리가 완료될 때 영구 저장소에 다시 써야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md)   
 [CDC 제어 태스크 편집기](../../integration-services/control-flow/cdc-control-task-editor.md)  
  
  

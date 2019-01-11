---
title: CDC 제어 태스크 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2a073699-79a2-4ea1-a68e-fc17a80b74ba
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c0eb2d790181b73f948e04a0e25f9d9702c6c62e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761891"
---
# <a name="cdc-control-task-custom-properties"></a>CDC 제어 태스크 사용자 지정 속성
  다음 표에서는 CDC 제어 태스크의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|설명|  
|-------------------|---------------|-----------------|  
|연결|ADO.NET 연결|변경 테이블과 CDC 상태(동일한 데이터베이스에 저장되어 있는 경우)에 액세스하기 위한 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC 데이터베이스에 대한 ADO.NET 연결입니다.<br /><br /> CDC에 사용할 수 있고 선택한 변경 테이블이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결해야 합니다.|  
|TaskOperation|Integer(열거형)|CDC 제어 태스크에 대해 선택한 작업입니다. 가능한 값은 **초기 로드 시작 표시**, **초기 로드 끝 표시**, **CDC 시작 표시**, **처리 범위 가져오기**, **처리된 범위 표시**및 **CDC 상태 다시 설정**입니다.<br /><br /> **CDC(Oracle이 아님)에서 작업할 때**MarkCdcStart **,** MarkInitialLoadStart **또는** MarkInitialLoadEnd [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 선택하는 경우 연결 관리자에서 지정하는 사용자가  **db_owner** 또는 **sysadmin**이어야 합니다.<br /><br /> 이러한 작업에 대한 자세한 내용은 [CDC Control Task Editor](../../integration-services/control-flow/cdc-control-task-editor.md) 및 [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md)를 참조하십시오.|  
|OperationParameter|String|현재 **MarkCdcStart** 작업에 사용됩니다. 이 매개 변수를 사용하면 특정 작업에 필요한 추가 입력이 가능해집니다. **MarkCdcStart** 작업에 필요한 LSN 번호를 예로 들 수 있습니다.|  
|StateVariable|String|현재 CDC 컨텍스트의 CDC 상태를 저장하는 SSIS 패키지 변수입니다. CDC 제어 태스크가 상태를 읽고 **StateVariable** 에 쓰며, **AutomaticStatePersistence** 가 선택되지 않은 한 상태를 로드하거나 영구 스토리지에 저장하지 않습니다. [상태 변수 정의](../../integration-services/data-flow/define-a-state-variable.md)|  
|AutomaticStatePersistence|Boolean|CDC 제어 태스크가 CDC 상태 패키지 변수에서 CDC 상태를 읽습니다. 작업 다음에 CDC 제어 태스크가 CDC 상태 패키지 변수의 값을 업데이트합니다. **AutomaticStatePersistence** 속성은 SSIS 패키지 실행 간에 CDC 상태 값을 유지하는 주체가 누구인지를 CDC 제어 태스크에 알려 줍니다.<br /><br /> 이 속성이 **true**이면 CDC 제어 태스크가 상태 테이블에서 자동으로 CDC 상태 변수의 값을 로드합니다. CDC 제어 태스크가 CDC 상태 변수의 값을 업데이트할 때는 특수 테이블의 상태인 동일한 상태 **table.stores**의 값과 StateVariable도 업데이트됩니다. 개발자는 상태 테이블 및 해당 이름이 포함되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 제어할 수 있습니다. 이 상태 테이블의 구조는 미리 정의되어 있습니다.<br /><br /> **false**이면 CDC 제어 태스크가 해당 값을 유지하는 작업을 처리하지 않습니다. true이면 CDC 제어 태스크가 특수 테이블에 상태를 저장하고 StateVariable을 업데이트합니다.<br /><br /> 기본값은 상태 지속이 자동으로 업데이트됨을 나타내는 **true**입니다.|  
|StateConnection|ADO.NET 연결|**AutomaticStatePersistence**사용 시 상태 테이블이 상주하는 데이터베이스에 대한 ADO.NET 연결입니다. 기본값은 **Connection**과 같습니다.|  
|StateName|String|영구 상태에 연결되는 이름입니다. 동일한 CDC 컨텍스트를 사용하는 CDC 패키지 및 전체 로드는 일반적인 CDC 컨텍스트 이름을 지정합니다. 이 이름은 상태 테이블에서 상태 행을 조회하는 데 사용됩니다.<br /><br /> 이 속성은 **AutomaticStatePersistence** 가 **true**로 설정되어 있는 경우에만 적용 가능합니다.|  
|StateTable|String|CDC 컨텍스트 상태가 저장되는 테이블의 이름을 지정합니다. 이 테이블은 이 구성 요소에 대해 구성된 연결을 사용하여 액세스할 수 있어야 합니다. 이 테이블에는 **이름** 및 **상태**라는 varchar 열을 포함해야 합니다. **상태** 열에는 256자 이상의 문자가 있어야 합니다.<br /><br /> 이 속성은 **AutomaticStatePersistence** 가 **true**로 설정되어 있는 경우에만 적용 가능합니다.|  
|CommandTimeout|integer|이 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 통신할 때 사용할 제한 시간(초)을 나타냅니다. 이 값은 데이터베이스로부터의 응답이 매우 느리고 기본값(30초)이 충분하지 않은 경우 사용됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md)   
 [CDC 제어 태스크 편집기](../../integration-services/control-flow/cdc-control-task-editor.md)  
  
  

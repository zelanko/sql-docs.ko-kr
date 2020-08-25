---
description: ReadyState 속성(RDS)
title: ReadyState 속성 (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ReadyState property [ADO]
ms.assetid: 5be75bc7-1171-4440-a37e-c8cc6b5cd865
author: rothja
ms.author: jroth
ms.openlocfilehash: 9915f76e336f7c8814428440460d1b0bfd7b9288
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767662"
---
# <a name="readystate-property-rds"></a>ReadyState 속성(RDS)
데이터를 [레코드 집합](../ado-api/recordset-object-ado.md) 개체로 검색할 때 [DataControl](./datacontrol-object-rds.md) 개체의 진행 상태를 나타냅니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 다음 값 중 하나를 설정 하거나 반환 합니다.  
  
|값|설명|  
|-----------|-----------------|  
|**adcReadyStateLoaded**|현재 쿼리가 계속 실행 중 이며 행을 가져오지 않았습니다. **DataControl** 개체의 **레코드 집합** 을 사용할 수 없습니다.|  
|**adcReadyStateInteractive**|현재 쿼리에서 검색 된 초기 행 집합은 **DataControl** 개체의 **레코드 집합** 에 저장 되 고 사용할 수 있습니다. 나머지 행은 계속 인출 됩니다.|  
|**adcReadyStateComplete**|현재 쿼리에서 검색 된 모든 행은 **DataControl** 개체의 **레코드 집합** 에 저장 되 고 사용할 수 있습니다.<br /><br /> 이 상태는 작업이 오류로 인해 중단 되었거나 **레코드 집합** 개체가 초기화 되지 않은 경우에도 존재 합니다.|  
  
> [!NOTE]
>  이러한 상수를 사용 하는 각 클라이언트 쪽 실행 파일은 이러한 상수에 대 한 선언을 제공 해야 합니다. RDS 라이브러리의 기본 설치 폴더에 있는 Adcvbs. inc. 파일에서 원하는 상수 선언을 잘라내어 붙여 넣을 수 있습니다.  
  
## <a name="remarks"></a>설명  
 비동기 쿼리 작업을 수행 하는 동안 [onReadyStateChange](./onreadystatechange-event-rds.md) 이벤트를 사용 하 여 **ReadyState** 속성의 변경 내용을 모니터링 합니다. 이는 주기적으로 속성의 값을 확인 하는 것 보다 효율적입니다.  
  
 비동기 작업 중에 오류가 발생 하면 **ReadyState** 속성이 **adcReadyStateComplete**로 변경 되 고 [State](../ado-api/state-property-ado.md) 속성이 **adstateexecuting** 에서 **adStateClosed**로 변경 되며 **레코드 집합** 개체 [값](../ado-api/value-property-ado.md) 속성은 *아무 것도*유지 되지 않습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [ReadyState 속성 예제 (VBScript)](./readystate-property-example-vbscript.md)   
 [Cancel 메서드 (RDS)](./cancel-method-rds.md)   
 [ExecuteOptions 속성(RDS)](./executeoptions-property-rds.md)
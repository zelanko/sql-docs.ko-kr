---
title: DataControl 오류 코드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], DataControl
- DataControl errors [ADO]
ms.assetid: 293df9d5-e1a2-406d-9107-07bf7cdc6f96
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34d749e90ed9e2d3c7819e23a9d7c552e0b4e8c0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="datacontrol-object-error-codes"></a>DataControl 개체가 오류 코드
다음 표에 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체 오류 코드입니다. 낮은 2 바이트의 양의 10 진수로 변환한 음의 10 진수로 변환한 전체 오류 코드 및 16 진수 값의 표시 됩니다.

|.RDS DataControl 오류 코드|Number|Description|
|---------------------------------|------------|-----------------|
|**IDS_AsyncPending**|4107 -2146824175 0x800A1011|비동기 작업이 보류 중인 동안에 작업을 수행할 수 없습니다.|
|**IDS_BadInlineTablegram**|4105 -2146824183 0x800A1009|잘못 된 인라인 테이블 그램입니다.|
|**IDS_CantConnect**|4099 -2146824189 0x800A1003|서버에 연결할 수 없습니다.|
|**IDS_CantCreateObject**|4100 -2146824188 0x800A1004|비즈니스 개체를 만들 수 없습니다.|
|**IDS_CantFindDataspace**|4102 -2146824186 0x800A1006|Dataspace 속성이 올바르지 않습니다.|
|**IDS_CantInvokeMethod**|4101 -2146824187 0x800A1005|비즈니스 개체의 메서드를 호출할 수 없습니다.|
|**IDS_CrossDomainWarning**|4112 -2146824170 0x800A1016|이 페이지에는 다른 도메인의 데이터에 액세스합니다. 이 기능을 허용 하 시겠습니까? Internet Explorer에서이 메시지를 방지 하려면 추가할 수 있습니다 보안 웹 사이트를 신뢰할 수 있는 사이트 영역에는 **보안** 탭은 **인터넷 옵션** 대화 상자.|
|**IDS_InvalidADCClientVersion**|4106 -2146824176 0x800A1010|RDS 클라이언트 버전이 잘못 되었습니다. 클라이언트는 서버를 보다 최신입니다.|
|**IDS_INVALIDARG**|5376 -2147019520 0x80071500|하나 이상의 인수가 잘못 되었습니다.|
|**IDS_InvalidBindings**|4097 -2146824191 0x800A1001|바인딩 속성에 오류가 발생 했습니다.|
|**IDS_InvalidParam**|4110 -2146824172 0x800A1014|하나 이상의 인수가 잘못 되었습니다.|
|**IDS_NOINTERFACE**|5377 -2147019519 0x80071501|이러한 인터페이스가 사용할 수 있습니다.|
|**IDS_NotReentrant**|4111 -2146824171 0x800A1015|이벤트 처리기가 처리 하는 동안 요청을 실행할 수 없습니다.|
|**IDS_ObjectNotSafe**|4103 -2146824185 0x800A1007|이 컴퓨터에 안전 설정 비즈니스 개체를 만들 수 없습니다.|
|**IDS_RecordsetNotOpen**|4109 -2146824173 0x800A1013|**레코드 집합** 열려 있지 않습니다.|
|**IDS_ResetInvalidField**|4108 -2146824174 0x800A1012|에 지정 된 열 **SortColumn** 또는 **FilterColumn** 존재 하지 않습니다.|
|**IDS_RowsetNotUpdateable**|4104 -2146824184 0x800A1008|행 집합을 업데이트할 수 없습니다.|
|**IDS_UnexpectedError**|4351 -2146823937 0x800A10FF|예기치 않은 오류가 발생 했습니다.|
|**IDS_UpdatesFailed**|4098 -2146824190 0x800A1002|데이터베이스를 업데이트할 수 없습니다.|
|**IDS_URLMONNotFound**|4119 -2146824169 0x800A1017|DataControl **URL** 속성 Urlmon.dll을 찾을 수 없는 시스템 파일에 필요 합니다.|

## <a name="see-also"></a>관련 항목:
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)

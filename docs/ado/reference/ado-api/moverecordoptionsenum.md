---
title: MoveRecordOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- MoveRecordOptionsEnum
helpviewer_keywords:
- MoveRecordOptionsEnum enumeration [ADO]
ms.assetid: f53c2ce4-1021-4a45-92b8-775e8bebad99
author: rothja
ms.author: jroth
ms.openlocfilehash: 849f3720d831c17b6b9d6d2829ae0b28f19992de
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762444"
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
[Record](../../../ado/reference/ado-api/record-object-ado.md) 개체 [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) 메서드의 동작을 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified 되지 않음**|-1|기본값 기본 이동 작업을 수행 합니다. 대상 파일이 나 디렉터리가 이미 있는 경우 작업이 실패 하 고 작업에서 하이퍼텍스트 링크를 업데이트 합니다.|  
|**adMoveOverWrite**|1|이미 존재 하는 경우에도 대상 파일이 나 디렉터리를 덮어씁니다.|  
|**adMoveDontUpdateLinks**|2|소스 **레코드**의 하이퍼텍스트 링크를 업데이트 하지 않고 **MoveRecord** 메서드의 기본 동작을 수정 합니다. 기본 동작은 공급자의 기능에 따라 달라 집니다. 공급자를 사용할 수 있는 경우 이동 작업은 링크를 업데이트 합니다. 공급자가 링크를 수정할 수 없거나이 값이 지정 되지 않은 경우 링크가 수정 되지 않은 경우에도 이동이 성공 합니다.|  
|**adMoveAllowEmulation**|4|다운로드, 업로드 및 삭제 작업을 사용 하 여 공급자가 이동 시뮬레이션을 시도 하도록 요청 합니다. 대상 URL이 다른 서버에 있거나 원본과 다른 공급자가 서비스를 제공 하기 때문에 **레코드** 를 이동 하려는 시도가 실패 하는 경우 공급자 간에 리소스를 이동할 때 다른 공급자 기능으로 인해 대기 시간 또는 데이터 손실이 발생할 수 있습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 이러한 상수에는 ADO/WFC 해당 항목이 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [MoveRecord 메서드(ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)

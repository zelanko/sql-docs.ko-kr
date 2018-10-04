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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb86b01a42a097210801fd3654ff2af80df24e39
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47701592"
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
동작을 지정 합니다 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체 [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) 메서드.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|기본. 기본 이동 작업을 수행 합니다: 하이퍼텍스트 링크를 업데이트 하는 작업 및 대상 파일 또는 디렉터리가 이미 있으면 작업이 실패 합니다.|  
|**adMoveOverWrite**|1|이미 존재 하는 경우에 대상 파일 또는 디렉터리를 덮어씁니다.|  
|**adMoveDontUpdateLinks**|2|기본 동작을 수정 **MoveRecord** 하이퍼텍스트 링크를 통해 소스를 업데이트 하지 않게 메서드 **레코드**합니다. 기본 동작은 공급자의 기능에 따라 달라 집니다. 이동 작업 공급자가 지원 링크를 업데이트 합니다. 공급자 링크를 해결할 수 없는 경우,이 값을 지정 하지 않으면 이동도 경우 링크 수정 되지 않은 성공 후 합니다.|  
|**adMoveAllowEmulation**|4|요청 공급자 시뮬레이션 (다운로드, 업로드 및 삭제 작업을 사용 하 여) 이동 하려고 합니다. 경우 이동 하려고 합니다 **레코드** 대상 URL은 다른 서버에 또는 소스와 다른 공급자에서 처리 하는,이 손실 될 수 있습니다 증가 대기 시간 또는 데이터를 다른 공급자 기능으로 인해 실패할 경우 공급자 간에 리소스를 이동 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [MoveRecord 메서드(ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)

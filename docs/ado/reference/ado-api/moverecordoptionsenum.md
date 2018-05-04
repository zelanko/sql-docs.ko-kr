---
title: MoveRecordOptionsEnum | Microsoft Docs
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
apitype: COM
f1_keywords:
- MoveRecordOptionsEnum
helpviewer_keywords:
- MoveRecordOptionsEnum enumeration [ADO]
ms.assetid: f53c2ce4-1021-4a45-92b8-775e8bebad99
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18508d9103b0be9a0dae3cff013ca2732a00035c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
동작을 지정 된 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체 [범위란](../../../ado/reference/ado-api/moverecord-method-ado.md) 메서드.  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|기본. 기본 이동 작업 수행: 하이퍼텍스트 링크를 업데이트 하는 작업 및 대상 파일 또는 디렉터리가 이미 있으면 작업이 실패 합니다.|  
|**adMoveOverWrite**|1.|이미 있는 경우에 대상 파일 또는 디렉터리를 덮어씁니다.|  
|**adMoveDontUpdateLinks**|2|기본 동작을 수정 **범위란** 하이퍼텍스트 링크를 통해 소스를 업데이트 하지 않음으로써 메서드 **레코드**합니다. 기본 동작 공급자의 기능에 따라 달라 집니다. 공급자가 지원 링크를 업데이트 하는 이동 작업을 수행 합니다. 공급자는 링크를 수정할 수 또는이 값을 지정 하지 않으면 다음 이동에 성공도 경우 링크 수정 되지 않은 합니다.|  
|**adMoveAllowEmulation**|4|요청을 공급자 시뮬레이션 (다운로드, 업로드, 및 삭제 작업을 사용 하 여) 이동 하려고 합니다. 경우 이동 하지는 **레코드** 대상 URL은 다른 서버에 또는 소스 다른 공급자에 의해 서비스 되는,이 손실 될 수 있습니다 증가 된 대기 시간 또는 데이터, 다른 공급자 기능이 실패할 경우 리소스는 공급자 간에 이동 합니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [MoveRecord 메서드(ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)

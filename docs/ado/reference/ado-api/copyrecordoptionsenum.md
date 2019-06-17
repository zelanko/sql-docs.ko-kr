---
title: 메서드의 동작 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CopyRecordOptionsEnum
helpviewer_keywords:
- CopyRecordOptionsEnum enumeration [ADO]
ms.assetid: 2fa4eec5-d50b-4fd3-8ae7-40af441ba12b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a944d3f82940d9364312fb8033ec8b8937b0c49c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66695766"
---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
동작을 지정 합니다 [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) 메서드.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|나타내는 *소스* 공급자로 인해이 방법이 실패 하면 작업을 업로드 및 다운로드를 사용 하 여 복사본을 시뮬레이션 하려고 *대상*다른 서버의 되거나 다른에서 처리 공급자 *원본*합니다. 서로 다른 공급자 기능 성능이 제한 될 수도 있고 데이터가 손실 있음을 참고 합니다.|  
|**adCopyNonRecursive**|2|현재 디렉터리에 있지만 하위 디렉터리의 대상에 복사합니다. 복사 작업은 재귀적이 아님.|  
|**adCopyOverWrite**|1|파일 또는 디렉터리를 덮어씁니다를 *대상* 기존 파일 또는 디렉터리를 가리킵니다.|  
|**adCopyUnspecified**|-1|기본. 기본 복사 작업을 수행합니다. 대상 파일 또는 디렉터리가 이미 있는 경우 작업이 실패 하 고는 작업이 반복적으로 복사 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [CopyRecord 메서드(ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)

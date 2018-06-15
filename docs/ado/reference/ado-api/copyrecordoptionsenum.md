---
title: 메서드의 동작 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CopyRecordOptionsEnum
helpviewer_keywords:
- CopyRecordOptionsEnum enumeration [ADO]
ms.assetid: 2fa4eec5-d50b-4fd3-8ae7-40af441ba12b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6314f9ab11e0704075b6a6cf8d0f9e529a3c0b69
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277162"
---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
동작을 지정 된 [범위란](../../../ado/reference/ado-api/copyrecord-method-ado.md) 메서드.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|나타냅니다는 *소스* 공급자가로 인해이 방법이 실패 하면 작업을 업로드 및 다운로드를 사용 하 여 복사본을 시뮬레이션 하도록 *대상*에서 다른 서비스 또는 다른 서버에 있음 공급자가 *소스*합니다. 참고 하 서로 다른 공급자 기능 인해 성능이 저하 되거나 데이터가 손실 됩니다.|  
|**adCopyNonRecursive**|2|현재 디렉터리를 제외 하 고 그 하위 디렉터리의 대상에 복사 합니다. 복사 작업은 재귀적이 아님.|  
|**adCopyOverWrite**|1|파일 또는 디렉터리를 덮어씁니다는 *대상* 기존 파일 또는 디렉터리를 가리킵니다.|  
|**adCopyUnspecified**|-1|기본. 기본 복사 작업을 수행 합니다: 대상 파일이 나 디렉터리가 이미 있는 경우 작업이 실패 하 고이 반복적으로 작업을 복사 합니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [CopyRecord 메서드(ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)

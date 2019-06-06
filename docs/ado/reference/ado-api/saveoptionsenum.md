---
title: SaveOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 537c5bfa6e1da125b562d4cc26820a2fcb5618fc
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711384"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
파일을 생성 또는 덮어쓸에서 저장 하는 경우 지정 된 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다. 값이 될 수 있습니다 **adSaveCreateNotExist** 하거나 **adSaveCreateOverWrite**...  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|기본. 파일을 지정 하 여 새 파일을 만듭니다는 *FileName* 매개 변수가 이미 존재 하지 않습니다.|  
|**adSaveCreateOverWrite**|2|현재 열려에서 데이터를 사용 하 여 파일을 덮어씁니다 **Stream** 개체를 지정 하는 파일을 *Filename* 매개 변수가 이미 있습니다. 하 여 파일을 지정 합니다 *Filename* 매개 변수가 없는 경우, 새 파일이 만들어집니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [SaveToFile 메서드](../../../ado/reference/ado-api/savetofile-method.md)

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
ms.openlocfilehash: 807a8d7e5757a2caf76f100a1ae51c4a8a3f4e98
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931141"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
[스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체에서 저장할 때 파일을 만들거나 덮어쓸지 여부를 지정 합니다. 값은 **adSaveCreateNotExist** 또는 **adSaveCreateOverWrite**수 있습니다.  
  
|지속적임|값|Description|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|Default. *FileName* 매개 변수에서 지정한 파일이 아직 없는 경우 새 파일을 만듭니다.|  
|**adSaveCreateOverWrite**|2|*Filename* 매개 변수로 지정 된 파일이 이미 있는 경우 현재 열려 있는 **스트림** 개체의 데이터로 파일을 덮어씁니다. *Filename* 매개 변수에서 지정한 파일이 없으면 새 파일이 만들어집니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 이러한 상수에는 ADO/WFC 해당 항목이 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [SaveToFile 메서드](../../../ado/reference/ado-api/savetofile-method.md)

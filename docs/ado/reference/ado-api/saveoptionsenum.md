---
title: SaveOptionsEnum | Microsoft Docs
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
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 502b6cf58647b7fe3a2b8dd8e7b627e60869cb43
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
파일을 만들지, 덮어쓸에서 저장할 때 지정 된 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다. 일 수 있습니다 **adSaveCreateNotExist** 또는 **adSaveCreateOverWrite**...  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1.|기본. 으로 지정한 파일이 있으면 새 파일을 만듭니다는 *FileName* 매개 변수가 이미 존재 하지 않습니다.|  
|**adSaveCreateOverWrite**|2|데이터를 현재 열려 있는 파일을 덮어씁니다 **스트림** 개체를 지정 하는 파일의 *Filename* 매개 변수가 이미 있습니다. 으로 지정한 파일이 있으면는 *Filename* 매개 변수가 없는, 새 파일이 생성 됩니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [SaveToFile 메서드](../../../ado/reference/ado-api/savetofile-method.md)

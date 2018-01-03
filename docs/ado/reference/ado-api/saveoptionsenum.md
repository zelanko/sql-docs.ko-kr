---
title: SaveOptionsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: SaveOptionsEnum
helpviewer_keywords: SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3830c052e6bf50bb8f85392f509f44e702639024
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
파일을 만들지, 덮어쓸에서 저장할 때 지정 된 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다. 일 수 있습니다 **adSaveCreateNotExist** 또는 **adSaveCreateOverWrite**...  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|기본. 으로 지정한 파일이 있으면 새 파일을 만듭니다는 *FileName* 매개 변수가 이미 존재 하지 않습니다.|  
|**adSaveCreateOverWrite**|2|데이터를 현재 열려 있는 파일을 덮어씁니다 **스트림** 개체를 지정 하는 파일의 *Filename* 매개 변수가 이미 있습니다. 으로 지정한 파일이 있으면는 *Filename* 매개 변수가 없는, 새 파일이 생성 됩니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [SaveToFile 메서드](../../../ado/reference/ado-api/savetofile-method.md)

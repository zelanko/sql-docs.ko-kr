---
description: SaveOptionsEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 27284d84bb89c0e742c5166589a60fdc949e7b2e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442195"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
[스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체에서 저장할 때 파일을 만들거나 덮어쓸지 여부를 지정 합니다. 값은 **adSaveCreateNotExist** 또는 **adSaveCreateOverWrite**수 있습니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|기본값 *FileName* 매개 변수에서 지정한 파일이 아직 없는 경우 새 파일을 만듭니다.|  
|**adSaveCreateOverWrite**|2|*Filename* 매개 변수로 지정 된 파일이 이미 있는 경우 현재 열려 있는 **스트림** 개체의 데이터로 파일을 덮어씁니다. *Filename* 매개 변수에서 지정한 파일이 없으면 새 파일이 만들어집니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 이러한 상수에는 ADO/WFC 해당 항목이 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [SaveToFile 메서드](../../../ado/reference/ado-api/savetofile-method.md)

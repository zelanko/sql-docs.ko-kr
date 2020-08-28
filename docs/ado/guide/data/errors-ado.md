---
description: 오류(ADO)
title: 오류 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 8ae6611b-3069-4155-b014-c0c9da37be39
author: rothja
ms.author: jroth
ms.openlocfilehash: e779d6b0aac1e48f64d9544eda0c064f7278c496
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991314"
---
# <a name="errors-ado"></a>오류(ADO)
ADO 개체와 관련 된 모든 작업은 하나 이상의 공급자 오류를 생성할 수 있습니다. 오류가 발생 하는 경우 하나 이상의 **오류** 개체가 **Connection** 개체의 **Errors** 컬렉션에 배치 됩니다. ADO 응용 프로그램의 경고 및 오류를 처리 하는 방법에 대 한 자세한 내용은 [오류 처리](./error-handling.md)를 참조 하세요.  
  
 응용 프로그램 오류는 별도의 메커니즘에 의해 발생할 수 있습니다. 예를 들어 Visual Basic에서 **Err** 개체는 응용 프로그램 수준 오류를 포함 합니다.
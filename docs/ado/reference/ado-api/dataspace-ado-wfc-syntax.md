---
description: 데이터스페이스(ADO - WFC 구문)
title: 스페이스 (ADO-WFC 구문) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace collection [ADO], ADO/WFC syntax
ms.assetid: 950d45d8-07de-467b-b255-f9a7b997204c
author: rothja
ms.author: jroth
ms.openlocfilehash: 6fdc89f6fb9c1c32236d7e4da02ad2afb118ba08
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974254"
---
# <a name="dataspace-ado---wfc-syntax"></a>데이터스페이스(ADO - WFC 구문)
**공간** 클래스의 **createObject** 메서드는*progid*(클라이언트 응용 프로그램 요청) 및 통신 프로토콜 및 서버 (*연결*)를 처리 하는 비즈니스 개체를 모두 지정 합니다. **createObject** 는 서버를 나타내는 [ObjectProxy](../../../ado/reference/ado-api/objectproxy-ado-wfc-syntax.md) 개체를 반환 합니다.  
  
## <a name="package-commswfcdata"></a>package com.  
  
### <a name="constructor"></a>생성자  
  
```  
public DataSpace()  
```  
  
### <a name="methods"></a>메서드  
  
```  
public static ObjectProxy DataSpace.createObject(String  
    progid, String connection)  
```  
  
### <a name="properties"></a>속성  
  
```  
public static int getInternetTimeout()  
public static void setInternetTimeout(int plInetTimeout)  
```  
  
## <a name="see-also"></a>참고 항목  
 [DataSpace 개체(RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)

---
title: 스페이스 (ADO-WFC 구문) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace collection [ADO], ADO/WFC syntax
ms.assetid: 950d45d8-07de-467b-b255-f9a7b997204c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 569944991c029c091f0f17be4e5d943a893333a7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919193"
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

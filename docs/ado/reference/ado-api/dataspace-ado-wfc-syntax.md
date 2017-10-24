---
title: "DataSpace (ADO-WFC 구문) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- DataSpace collection [ADO], ADO/WFC syntax
ms.assetid: 950d45d8-07de-467b-b255-f9a7b997204c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0344190472a9548880e828786bd252bdb17de29b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="dataspace-ado---wfc-syntax"></a>DataSpace (ADO-WFC 구문)
**createObject** 의 메서드는 **DataSpace** 클라이언트 응용 프로그램 요청을 처리할 두 비즈니스 개체를 지정 하는 클래스 (*progid*) 및 통신 프로토콜 와 서버 (*연결*). **createObject** 반환는 [ObjectProxy](../../../ado/reference/ado-api/objectproxy-ado-wfc-syntax.md) 서버를 나타내는 개체입니다.  
  
## <a name="package-commswfcdata"></a>패키지 com.ms.wfc.data  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [DataSpace 개체(RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)


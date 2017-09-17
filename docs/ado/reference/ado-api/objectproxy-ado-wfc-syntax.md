---
title: "ObjectProxy (ADO-WFC 구문) | Microsoft Docs"
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
- ObjectProxy collection [ADO]
ms.assetid: f68f58bc-ad28-46cc-9fb3-099e1a678397
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0bd3aa2bd2cf7b49432e6b29c312e65819d50f4a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy (ADO-WFC 구문)
**ObjectProxy** 개체는 서버를 나타내며에서 반환 되는 **createObject** 의 메서드는 [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) 개체입니다. ObjectProxy 클래스에는 하나의 메서드 **호출**, 서버에서 메서드를 호출 하 고 해당 호출의 결과로 개체를 반환할 수 있는 합니다.  
  
 **패키지 com.ms.wfc.data**  
  
## <a name="methods"></a>메서드  
  
### <a name="call-method-adowfc-syntax"></a>Call 메서드 (ADO/WFC 구문)  
 ObjectProxy가 나타내는 서버에서 메서드를 호출 합니다. 필요에 따라 개체의 배열으로 메서드 인수를 전달할 수 있습니다.  
  
#### <a name="syntax"></a>구문  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>반환 값  
 개체  
 메서드 호출에서 발생 하는 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *ObjectProxy*  
 **ObjectProxy** 서버를 나타내는 개체입니다.  
  
 *메서드*  
 서버에서 호출할 메서드의 이름을 포함 하는 문자열입니다.  
  
 *args*  
 (선택 사항) 인수는 서버에서 메서드를 개체의 배열입니다. 서버에서 사용 하기 위해 적합 한 데이터 형식으로 Java 데이터 형식 자동 변환 됩니다.

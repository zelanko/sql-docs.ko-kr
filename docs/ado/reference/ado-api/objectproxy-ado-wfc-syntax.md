---
title: ObjectProxy (ADO-WFC 구문) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ObjectProxy collection [ADO]
ms.assetid: f68f58bc-ad28-46cc-9fb3-099e1a678397
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 485d011fa6762acd04cad54ff7fffc8d8136e063
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917951"
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy(ADO - WFC 구문)
**ObjectProxy** 개체는 서버를 나타내며에서 반환 되는 **createObject** 메서드를 [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) 개체입니다. ObjectProxy 클래스에 메서드 하나가 **호출**, 서버에서 메서드를 호출할 수 있으며 해당 호출의 결과 개체를 반환 합니다.  
  
 **package com.ms.wfc.data**  
  
## <a name="methods"></a>메서드  
  
### <a name="call-method-adowfc-syntax"></a>Call 메서드 (ADO/WFC 구문)  
 ObjectProxy 나타내는 서버의 메서드를 호출 합니다. 필요에 따라 개체의 배열로 메서드 인수를 전달할 수 있습니다.  
  
#### <a name="syntax"></a>구문  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>반환 값  
 Object  
 메서드를 호출 하 여 얻어지는 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *ObjectProxy*  
 **ObjectProxy** 서버를 나타내는 개체입니다.  
  
 *method*  
 서버에 대해 호출할 메서드의 이름을 포함 하는 문자열입니다.  
  
 *args*  
 (선택 사항) 서버에서 메서드에 대 한 인수는 개체의 배열입니다. 서버에서 사용 하기 적합 한 데이터 형식으로 Java 데이터 형식 자동 변환 됩니다.

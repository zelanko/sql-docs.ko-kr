---
description: ObjectProxy(ADO - WFC 구문)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7809c1b9ce4d090ed63465061045ea04000f47dc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443035"
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy(ADO - WFC 구문)
**ObjectProxy** 개체는 서버를 나타내며 [, 해당 개체](../../../ado/reference/rds-api/dataspace-object-rds.md) 의 **createObject** 메서드에서이를 반환 합니다. ObjectProxy 클래스에는 서버에서 메서드를 호출 하 고 해당 호출로 인해 발생 하는 **개체를 반환할**수 있는 메서드 하나가 있습니다.  
  
 **package com.**  
  
## <a name="methods"></a>메서드  
  
### <a name="call-method-adowfc-syntax"></a>Call 메서드 (ADO/WFC 구문)  
 ObjectProxy가 나타내는 서버에서 메서드를 호출 합니다. 필요에 따라 메서드 인수를 개체의 배열로 전달할 수 있습니다.  
  
#### <a name="syntax"></a>구문  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>반환  
 Object  
 메서드를 호출한 결과로 만들어지는 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *ObjectProxy*  
 서버를 나타내는 **ObjectProxy** 개체입니다.  
  
 *방법이*  
 서버에서 호출할 메서드의 이름을 포함 하는 문자열입니다.  
  
 *args*  
 (선택 사항) 서버에 있는 메서드에 대 한 인수인 개체의 배열입니다. Java 데이터 형식은 서버에서 사용 하기에 적합 한 데이터 형식으로 자동으로 변환 됩니다.

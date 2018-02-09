---
title: "명령 (ADO-WFC 구문) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Command collection [ADO], ADO/WFC syntax
ms.assetid: 39d0aa06-03ac-4c9a-8400-83947756ef99
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 310b7c246fc5d7006cc2e358340d0aa062dc3ab3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="command-ado---wfc-syntax"></a>명령 (ADO-WFC 구문)
## <a name="package-commswfcdata"></a>package com.ms.wfc.data  
  
### <a name="constructor"></a>생성자  
  
```  
public Command()  
public Command(String commandtext)  
```  
  
### <a name="methods"></a>메서드  
  
```  
public void cancel()  
public com.ms.wfc.data.Parameter createParameter(String  
    Name, int Type, int Direction, int Size, Object Value)  
public Recordset execute()  
public Recordset execute(Object[] parameters)  
public Recordset execute(Object[] parameters, int options)  
public int executeUpdate(Object[] parameters)  
public int executeUpdate(Object[] parameters, int options)  
public int executeUpdate()  
```  
  
 **executeUpdate** 메서드는 내부 ADO를 호출 하는 특수 한 사례 방법이 **실행** 특정 매개 변수와 함께 메서드. **executeUpdate** 방법은의 반환을 지원 하지 않습니다는 **레코드 집합** 개체 이므로 **실행** 메서드의 *옵션* 매개 변수는 로 수정 **AdoEnums.ExecuteOptions.NORECORDS**합니다. 이후에 **실행** 메서드가 완료 되 면 해당 업데이트 된 *RecordsAffected* 로 다시 전달 될 매개 변수는 **executeUpdate** 는 로마지막으로반환되는메서드**int**합니다.  
  
### <a name="properties"></a>속성  
  
```  
public com.ms.wfc.data.Connection getActiveConnection()  
public void setActiveConnection(com.ms.wfc.data.Connection con)  
public void setActiveConnection(String conString)  
public String getCommandText()  
public void setCommandText(String command)  
public int getCommandTimeout()  
public void setCommandTimeout(int timeout)  
public int getCommandType()  
public void setCommandType(int type)  
public String getName()  
public void setName(String name)  
public boolean getPrepared()  
public void setPrepared(boolean prepared)  
public int getState()  
public com.ms.wfc.data.Parameter getParameter(int n)  
public com.ms.wfc.data.Parameter getParameter(String n)  
public com.ms.wfc.data.Parameters getParameters()  
public AdoProperties getProperties()  
```  
  
## <a name="see-also"></a>관련 항목:  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)

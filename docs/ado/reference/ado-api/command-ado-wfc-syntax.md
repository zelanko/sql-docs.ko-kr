---
title: 명령 (ADO-WFC 구문) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Command collection [ADO], ADO/WFC syntax
ms.assetid: 39d0aa06-03ac-4c9a-8400-83947756ef99
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6866423ba07ed79992ebd098b7b4f5e5eff91ad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770821"
---
# <a name="command-ado---wfc-syntax"></a>명령(ADO - WFC 구문)
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
  
 합니다 **executeUpdate** 메서드는 특수 한 경우 호출 하는 메서드 내부 ADO **실행** 특정 매개 변수를 사용 하 여 메서드. **executeUpdate** 메서드는 반환을 지원 하지 않습니다는 **레코드 집합** 개체 이므로 **실행** 메서드의 *옵션* 매개 변수는 사용 하 여 수정할 **AdoEnums.ExecuteOptions.NORECORDS**합니다. 후는 **실행** 메서드가 완료 되 면 해당 업데이트 *RecordsAffected* 로 다시 전달 될 매개 변수를 **executeUpdate** 는으로마지막으로반환되는메서드**int**합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)

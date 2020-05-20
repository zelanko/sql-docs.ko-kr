---
title: Command (ADO-WFC 구문) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 61b5a54778bb680b68e923d198831d770973d1a7
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760449"
---
# <a name="command-ado---wfc-syntax"></a>명령(ADO - WFC 구문)
## <a name="package-commswfcdata"></a>package com.  
  
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
  
 **Executeupdate** 메서드는 특정 매개 변수를 사용 하 여 기본 ADO **execute** 메서드를 호출 하는 특별 한 사례 메서드입니다. **Executeupdate** 메서드는 **레코드 집합** 개체의 반환을 지원 하지 않으므로 **execute** 메서드의 *options* 매개 변수는 ADOENUMS를 사용 하 여 수정 됩니다. **NORECORDS**. **Execute** 메서드가 완료 되 면 업데이트 된 *RecordsAffected* 매개 변수가 **executeupdate** 메서드로 다시 전달 되 고,이 메서드는 **int**로 반환 됩니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)

---
title: Connection (ADO-WFC 구문) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Connection collection [ADO], ADO/WFC syntax
ms.assetid: 8cfc35bb-91e2-47da-ad4c-982e9162cd51
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 64647d577170a79b1f600b7162a0338ea19c572e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919532"
---
# <a name="connection-ado---wfc-syntax"></a>연결(ADO - WFC 구문)
## <a name="package-commswfcdata"></a>package com.  
  
### <a name="constructor"></a>생성자  
  
```  
public Connection()  
public Connection(String connectionstring)  
```  
  
### <a name="methods"></a>메서드  
  
```  
public int beginTrans()  
public void commitTrans()  
public void rollbackTrans()  
public void cancel()  
public void close()  
public com.ms.wfc.data.Recordset execute(String commandText)  
public com.ms.wfc.data.Recordset execute(String commandText, int options)  
public int executeUpdate(String commandText)  
public int executeUpdate(String commandText, int options)  
```  
  
 **Executeupdate** 메서드는 특정 매개 변수를 사용 하 여 기본 ADO **execute** 메서드를 호출 하는 특별 한 사례 메서드입니다. **Executeupdate** 메서드는 **레코드 집합** 개체의 반환을 지원 하지 않으므로 **execute** 메서드의 *options* 매개 변수는 ADOENUMS를 사용 하 여 수정 됩니다. **NORECORDS**. **Execute** 메서드가 완료 되 면 업데이트 된 *RecordsAffected* 매개 변수가 **executeupdate** 메서드로 다시 전달 되 고,이 메서드는 **int**로 반환 됩니다.  
  
```  
public void open()   
public void open(String connectionString)  
public void open(String connectionString, String userID)  
public void open(String connectionString, String userID, String password)  
public void open(String connectionString, String userID, String password, int options)  
public Recordset openSchema(int schema, Object[]  
    restrictions, String schemaID)  
public Recordset openSchema(int schema)  
public Recordset openSchema(int schema, Object[] restrictions)  
```  
  
### <a name="properties"></a>속성  
  
```  
public int getAttributes()  
public void setAttributes(int attr)  
public int getCommandTimeout()  
public void setCommandTimeout(int timeout)  
public String getConnectionString()  
public void setConnectionString(String con)  
public int getConnectionTimeout()  
public void setConnectionTimeout(int timeout)  
public int getCursorLocation()  
public void setCursorLocation(int cursorLoc)  
public String getDefaultDatabase()  
public void setDefaultDatabase(String db)  
public int getIsolationLevel()  
public void setIsolationLevel(int level)  
public int getMode()  
public void setMode(int mode)  
public String getProvider()  
public void setProvider(String provider)  
public int getState()  
public String getVersion()  
public AdoProperties getProperties()  
public com.ms.wfc.data.Errors getErrors()  
```  
  
### <a name="events"></a>이벤트  
 ADO/WFC 이벤트에 대 한 자세한 내용은 [언어별 Ado 이벤트 인스턴스화](../../../ado/guide/data/ado-event-instantiation-by-language.md)를 참조 하세요.  
  
```  
public void addOnBeginTransComplete(ConnectionEventHandler handler)  
public void removeOnBeginTransComplete(ConnectionEventHandler handler)  
public void addOnCommitTransComplete(ConnectionEventHandler handler)  
public void removeOnCommitTransComplete(ConnectionEventHandler handler)  
public void addOnConnectComplete(ConnectionEventHandler handler)  
public void removeOnConnectComplete(ConnectionEventHandler handler)  
public void addOnDisconnect(ConnectionEventHandler handler)  
public void removeOnDisconnect(ConnectionEventHandler handler)  
public void addOnExecuteComplete(ConnectionEventHandler handler)  
public void removeOnExecuteComplete(ConnectionEventHandler handler)  
public void addOnInfoMessage(ConnectionEventHandler handler)  
public void removeOnInfoMessage(ConnectionEventHandler handler)  
public void addOnRollbackTransComplete(ConnectionEventHandler handler)  
public void removeOnRollbackTransComplete(ConnectionEventHandler handler)  
public void addOnWillConnect(ConnectionEventHandler handler)  
public void removeOnWillConnect(ConnectionEventHandler handler)  
public void addOnWillExecute(ConnectionEventHandler handler)  
public void removeOnWillExecute(ConnectionEventHandler handler)  
```  
  
## <a name="see-also"></a>참고 항목  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)

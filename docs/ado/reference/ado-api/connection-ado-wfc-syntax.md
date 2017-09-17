---
title: "연결 (ADO-WFC 구문) | Microsoft Docs"
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
- Connection collection [ADO], ADO/WFC syntax
ms.assetid: 8cfc35bb-91e2-47da-ad4c-982e9162cd51
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 05a4b45caddc9110712fdc363f44ba37c4e92d45
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="connection-ado---wfc-syntax"></a>연결 (ADO-WFC 구문)
## <a name="package-commswfcdata"></a>패키지 com.ms.wfc.data  
  
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
  
 **executeUpdate** 메서드는 내부 ADO를 호출 하는 특수 한 사례 방법이 **실행** 특정 매개 변수와 함께 메서드. **executeUpdate** 방법은의 반환을 지원 하지 않습니다는 **레코드 집합** 개체 이므로 **실행** 메서드의 *옵션* 매개 변수는 로 수정 **AdoEnums.ExecuteOptions.NORECORDS**합니다. 이후에 **실행** 메서드가 완료 되 면 해당 업데이트 된 *RecordsAffected* 로 다시 전달 될 매개 변수는 **executeUpdate** 는 로마지막으로반환되는메서드**int**합니다.  
  
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
 ADO/WFC 이벤트에 대 한 자세한 내용은 참조 [언어별 ADO 이벤트 인스턴스 생성](../../../ado/guide/data/ado-event-instantiation-by-language.md)합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)

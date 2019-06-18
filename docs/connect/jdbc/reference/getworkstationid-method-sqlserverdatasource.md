---
title: getWorkstationID 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getWorkstationID
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6a701de-a8fa-4668-9310-99a8c6e32c88
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 117c0ad7ff08cec0c3c0b39758dce1dc55ecb249
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66779884"
---
# <a name="getworkstationid-method-sqlserverdatasource"></a>getWorkstationID 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터 원본에 연결하는 데 사용되는 클라이언트 컴퓨터의 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getWorkstationID()  
```  
  
## <a name="return-value"></a>반환 값  
 클라이언트 컴퓨터 이름이 포함된 **문자열**입니다.  
  
## <a name="remarks"></a>Remarks  
 workstationID는 클라이언트 컴퓨터 또는 워크스테이션의 이름입니다. workstationID 속성이 설정되지 않으면 기본값은 InetAddress.getLocalHost().getHostName() 메서드를 호출하여 생성됩니다. getHostName이 빈 값을 반환하면 getHostAddress().toString() 메서드가 호출됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

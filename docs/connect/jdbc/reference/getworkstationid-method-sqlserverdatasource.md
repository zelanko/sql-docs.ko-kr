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
ms.openlocfilehash: 98cde4953d60f13d1768b06dbfab9ada6ea8af55
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67978051"
---
# <a name="getworkstationid-method-sqlserverdatasource"></a>getWorkstationID 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터 원본에 연결하는 데 사용되는 클라이언트 컴퓨터의 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getWorkstationID()  
```  
  
## <a name="return-value"></a>Return Value  
 클라이언트 컴퓨터 이름이 포함된 **문자열**입니다.  
  
## <a name="remarks"></a>설명  
 workstationID는 클라이언트 컴퓨터 또는 워크스테이션의 이름입니다. workstationID 속성이 설정되지 않으면 기본값은 InetAddress.getLocalHost().getHostName() 메서드를 호출하여 생성됩니다. getHostName이 빈 값을 반환하면 getHostAddress().toString() 메서드가 호출됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

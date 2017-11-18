---
title: "setSendStringParametersAsUnicode 메서드 (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.setSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49198d63-76cb-4843-8d04-e49b1fbb6916
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 554c7e2483e96e27de627f764193a1d4fcabb6dd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setsendstringparametersasunicode-method-sqlserverdatasource"></a>setSendStringParametersAsUnicode 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  설정 된 **부울** 문자열 매개 변수를 서버에 유니코드 형식으로 보낼을 사용할 수 있는지를 나타내는 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setSendStringParametersAsUnicode(boolean sendStringParametersAsUnicode)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sendStringParametersAsUnicode*  
  
 **true 이면** 경우 문자열 매개 변수가 유니코드 형식으로 서버에에서 전송 됩니다. 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>주의  
 SendStringParametersAsUnicode 속성이로 설정 되어 있으면 **true**은 기본 값, 문자열 매개 변수가 유니코드 형식으로 서버에에서 전송 됩니다. Sendstringparametersasunicode 속성이로 설정 되어 있으면 **false** 문자열 매개 변수가 유니코드 아닌 ASCII/MBCS 형식으로 서버에 전송 됩니다. Sendstringparametersasunicode 속성이 설정 되어 있지 않으면 [getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md) 의 기본 값을 반환 **true**합니다.  
  
 SendStringParametersAsUnicode 연결 속성에 대 한 자세한 내용은 참조 [연결 속성을 설정할](../../../connect/jdbc/setting-the-connection-properties.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  


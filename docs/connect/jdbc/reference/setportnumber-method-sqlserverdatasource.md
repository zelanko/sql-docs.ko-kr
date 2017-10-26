---
title: "setPortNumber 메서드 (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.setPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 59c5fa23-bc1a-4142-af17-70e275f0b833
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 26f5f9e97d086e64f008c7f4af2913a5305585a1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setportnumber-method-sqlserverdatasource"></a>setPortNumber 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  와 통신 하는 데 사용할 포트 번호를 설정 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setPortNumber(int portNumber)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *포트 번호*  
  
 **int** 포트 번호를 포함 하는 값입니다.  
  
## <a name="remarks"></a>주의  
 포트 번호는 소켓 연결을 열 때 사용 되는 TCP/IP 포트 번호 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다. PortNumber 속성이 설정 하지 않으면는 [getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md) 메서드는 기본값인 1433 반환 합니다.  
  
> [!NOTE]  
>  SetPortNumber 메서드 범위에 전달 된 포트 값에 검사를 수행 하지 않습니다. 오류가 따라서 99999와 같이 유효 하지 않은 포트 번호를 전달할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  


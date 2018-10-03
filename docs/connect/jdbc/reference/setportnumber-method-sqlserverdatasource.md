---
title: setPortNumber 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 59c5fa23-bc1a-4142-af17-70e275f0b833
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15e0ff764637869428945ab3eb4b6c44b055b436
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47728201"
---
# <a name="setportnumber-method-sqlserverdatasource"></a>setPortNumber 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와의 통신에 사용할 포트 번호를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setPortNumber(int portNumber)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *portNumber*  
  
 포트 번호가 들어 있는 **int** 값입니다.  
  
## <a name="remarks"></a>Remarks  
 포트 번호는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 소켓 연결을 열 때 사용되는 TCP/IP 포트 번호입니다. portNumber 속성이 설정되어 있지 않으면 [getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md) 메서드는 기본값인 1433을 반환합니다.  
  
> [!NOTE]  
>  SetPortNumber 메서드는 전달 된 포트 값에 대해 범위 검사를 수행 하지 않습니다. 오류를 트리거하지 않고 따라서 99999와 같이 올바르지 않은 포트 번호를 전달할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

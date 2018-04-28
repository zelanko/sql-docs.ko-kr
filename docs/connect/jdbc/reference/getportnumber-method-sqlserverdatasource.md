---
title: getPortNumber 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerDataSource.getPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7cc115a11669b586a9e8271aad44e4ce11359c91
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="getportnumber-method-sqlserverdatasource"></a>getPortNumber 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  와 통신 하는 데 사용 되는 현재 포트 번호를 반환 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>반환 값  
 **int** 는 현재 포트 번호를 포함 하는 값입니다.  
  
## <a name="remarks"></a>주의  
 포트 번호는 소켓 연결을 열 때 사용 되는 TCP/IP 포트 번호 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다. portNumber 속성이 설정되어 있지 않으면 getPortNumber 메서드는 기본값인 -1을 반환합니다.  
  
> [!NOTE]  
>  [setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md) 메서드 범위에 전달 된 포트 값에 검사를 수행 하지 않습니다. 오류가 따라서 99999와 같이 유효 하지 않은 번호를 전달할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

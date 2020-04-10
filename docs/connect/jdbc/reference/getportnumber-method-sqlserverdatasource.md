---
title: getPortNumber 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8fcd2c1260ee69cbd3a50573f53b07bf429da402
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925236"
---
# <a name="getportnumber-method-sqlserverdatasource"></a>getPortNumber 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와의 통신에 사용되는 현재 포트 번호를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>Return Value  
 현재 포트 번호가 들어 있는 **int** 값입니다.  
  
## <a name="remarks"></a>설명  
 포트 번호는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 소켓 연결을 열 때 사용되는 TCP/IP 포트 번호입니다. portNumber 속성이 설정되어 있지 않으면 getPortNumber 메서드는 기본값인 -1을 반환합니다.  
  
> [!NOTE]  
>  [setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md) 메서드는 전달된 포트 값에 대해 범위 검사를 수행하지 않습니다. 따라서 99999와 같이 유효하지 않은 포트 번호를 전달해도 오류가 트리거되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

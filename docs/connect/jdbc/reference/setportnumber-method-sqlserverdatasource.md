---
description: setPortNumber 메서드(SQLServerDataSource)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbf1cccfab3cef60193cc9b45921c203821cbfca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458485"
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
  
## <a name="remarks"></a>설명  
 포트 번호는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 소켓 연결을 열 때 사용되는 TCP/IP 포트 번호입니다. portNumber 속성이 설정되어 있지 않으면 [getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md) 메서드는 기본값인 1433을 반환합니다.  
  
> [!NOTE]  
>  setPortNumber 메서드는 전달된 포트 값에 대해 범위 검사를 수행하지 않습니다. 따라서 99999와 같이 유효하지 않은 포트 번호를 전달해도 오류가 트리거되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

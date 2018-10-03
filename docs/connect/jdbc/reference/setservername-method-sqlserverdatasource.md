---
title: setServerName 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 70920828-eda0-4064-be9f-c1e460db8f00
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da3aee4570f579e4a3ed6007412222506ed2e24d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47827961"
---
# <a name="setservername-method-sqlserverdatasource"></a>setServerName 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 실행 중인 컴퓨터의 이름을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setServerName(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *serverName*  
  
 서버 이름을 포함하는 **문자열**입니다.  
  
## <a name="remarks"></a>Remarks  
 서버 이름은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 실행 중인 대상 컴퓨터의 호스트 이름입니다. serverName 속성이 설정되어 있지 않으면 [getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)은 기본값인 null을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

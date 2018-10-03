---
title: getServerName 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3004ed22-5d69-4dd0-8761-d39f0b7dde13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76ff04ce4b2a56387a573f7409b1e56c93fdedff
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47833913"
---
# <a name="getservername-method-sqlserverdatasource"></a>getServerName 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getServerName()  
```  
  
## <a name="return-value"></a>반환 값  
 서버 이름이 들어 있는 **문자열**이며, 값이 설정되어 있지 않은 경우 null입니다.  
  
## <a name="remarks"></a>Remarks  
 서버 이름은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 실행 중인 대상 컴퓨터의 호스트 이름입니다. getServerName 속성이 설정되어 있지 않으면 getServerName은 기본값인 null을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

---
description: getServerName 메서드(SQLServerDataSource)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f8e2045d2c296386f13907ce3b95923a5b58826e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434605"
---
# <a name="getservername-method-sqlserverdatasource"></a>getServerName 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getServerName()  
```  
  
## <a name="return-value"></a>Return Value  
 서버 이름이 들어 있는 **문자열**이며, 값이 설정되어 있지 않은 경우 null입니다.  
  
## <a name="remarks"></a>설명  
 서버 이름은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 실행 중인 대상 컴퓨터의 호스트 이름입니다. getServerName 속성이 설정되어 있지 않으면 getServerName은 기본값인 null을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

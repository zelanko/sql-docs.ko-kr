---
description: setUser 메서드(SQLServerDataSource)
title: setUser 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d2ea7906-2d10-438d-aa51-f576eea923c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b887e5b0af5d4a91a8cbea2b3676fd958ac3c077
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472182"
---
# <a name="setuser-method-sqlserverdatasource"></a>setUser 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터 원본에 연결하는 데 사용되는 사용자 이름을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setUser(java.lang.String user)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *user*  
  
 사용자 이름을 포함하는 **문자열**입니다.  
  
## <a name="remarks"></a>설명  
 setUser 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결하는 데 사용될 사용자 이름을 설정합니다. 사용자 이름 값이 설정되어 있지 않으면 [getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md) 메서드는 기본값인 null을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

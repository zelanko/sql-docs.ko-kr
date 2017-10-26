---
title: "getServerName 메서드 (SQLServerDataSource) | Microsoft Docs"
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
- SQLServerDataSource.getServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3004ed22-5d69-4dd0-8761-d39f0b7dde13
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2f7c77c52a62465eea584e3fa695810a65ffc202
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getservername-method-sqlserverdatasource"></a>getServerName 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이름을 반환 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getServerName()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 포함 하는 서버 이름 또는 null 값이 없는 설정 된 경우.  
  
## <a name="remarks"></a>주의  
 서버 이름은 실행 하는 대상 컴퓨터의 호스트 이름을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다. GetServerName 속성을 설정 하지 않으면 getservername은 기본값인 null 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  


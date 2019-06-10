---
title: getXopenStates 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de6fdf6b-8345-4490-b35e-7115b61e782e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c0a3859c3195d14243ff570493d3ae04c72d0780
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66768810"
---
# <a name="getxopenstates-method-sqlserverdatasource"></a>getXopenStates 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  SQL 상태를 XOPEN 규격 상태로 변환할 수 있는지 여부를 나타내는 **boolean** 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getXopenStates()  
```  
  
## <a name="return-value"></a>반환 값  
 SQL 상태를 XOPEN 규격 상태로 변환할 수 있으면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>Remarks  
 xopenStates 속성이 **true**로 설정되어 있으면 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 SQL 상태를 XOPEN 규격 상태로 변환합니다. 기본값은 **false**이며 JDBC 드라이버에서 SQL 99 상태 코드를 생성하도록 합니다. xopenStates 속성이 설정되어 있지 않으면 getXopenStates 메서드는 기본값인 **false**를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

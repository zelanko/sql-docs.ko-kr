---
title: getApplicationName 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.getApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f71e501c-ccd7-4a1e-b6ea-4d47a81c18c6
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0239d7d251b4104000646a8f98a3cae0be656853
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32829468"
---
# <a name="getapplicationname-method-sqlserverdatasource"></a>getApplicationName 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  응용 프로그램 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getApplicationName()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 응용 프로그램 이름을 포함 하는 또는 "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]" 값이 없는 설정 된 경우.  
  
## <a name="remarks"></a>주의  
 응용 프로그램 이름은 다양 한 특정 응용 프로그램을 식별 하는 데 사용 됩니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 프로 파일링 및 로깅 도구입니다. GetApplicationName 메서드 지역화 되지 않은 문자열을 반환 하는 경우 응용 프로그램 이름이 설정 되지 않은 "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]"입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

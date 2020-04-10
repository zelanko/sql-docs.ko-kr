---
title: getApplicationName 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f71e501c-ccd7-4a1e-b6ea-4d47a81c18c6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ad1a1b199b391e00a3db1c916f349f9cec94713
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924175"
---
# <a name="getapplicationname-method-sqlserverdatasource"></a>getApplicationName 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  애플리케이션 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getApplicationName()  
```  
  
## <a name="return-value"></a>Return Value  
 애플리케이션 이름이 들어 있는 **문자열**이며, 값이 설정되어 있지 않은 경우 “[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]”입니다.  
  
## <a name="remarks"></a>설명  
 애플리케이션 이름은 다양한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로파일링 및 로깅 도구에서 특정 애플리케이션을 식별하는 데 사용됩니다. 애플리케이션 이름이 설정되어 있지 않으면 getApplicationName 메서드는 지역화되지 않은 문자열인 “[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]”를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

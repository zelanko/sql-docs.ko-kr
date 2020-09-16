---
description: setTrustStorePassword 메서드(SQLServerDataSource)
title: setTrustStorePassword 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setTrustStorePassword Method (SQLServerDataSource)
apilocation:
- setTrustStorePassword Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: fa87cbde-71cc-4f21-bc07-f8ba2b6a0a3f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6ded82d7db8e7dade5c203a348375812b4e04dfc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88478630"
---
# <a name="settruststorepassword-method-sqlserverdatasource"></a>setTrustStorePassword 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  trustStore 데이터의 무결성을 검사하는 데 사용되는 암호를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setTrustStorePassword(java.lang.String trustStorePassword)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *trustStorePassword*  
  
 trustStore 데이터의 무결성을 검사하는 데 사용되는 암호가 들어 있는 **문자열**입니다.  
  
## <a name="remarks"></a>설명  
 trustStorePassword 속성은 trustStore 속성과 함께 지정할 수 있으며 해당 값을 사용하여 trustStore 파일의 무결성을 검사합니다.  
  
 trustStore 속성은 설정되어 있지만 trustStorePassword 속성이 설정되어 있지 않는 경우 trustStore의 무결성을 검사하지 않습니다.  
  
 trustStore 속성과 trustStorePassword 속성이 모두 지정되어 있지 않는 경우 드라이버에서 JVM(Java Virtual Machine) 시스템 속성 "javax.net.ssl.trustStore" 및 "javax.net.ssl.trustStorePassword"를 사용합니다. "javax.net.ssl.trustStorePassword" 시스템 속성이 지정되어 있지 않는 경우 trustStore의 무결성을 검사하지 않습니다.  
  
 trustStore 속성은 설정되어 있지 않지만 trustStorePassword 속성이 설정되어 있는 경우 JDBC 드라이버에서는 "javax.net.ssl.trustStore"에 지정된 파일을 트러스트 저장소로 사용하여 지정된 trustStorePassword로 트러스트 저장소의 무결성을 검사합니다. 클라이언트 애플리케이션이 JVM 시스템 속성에 암호를 저장하지 않는 경우 이 방법이 필요할 수 있습니다.  
  
 자세한 내용은 [연결 속성 설정](../../../connect/jdbc/setting-the-connection-properties.md)을 참조하세요.  
  
 JDBC 드라이버 3.0부터는 데이터 원본 속성을 바인딩하기 전에 SQLServerDataSource.setTrustStorePassword를 설정할 경우, 연결을 가져오기 전에 SQLServerDataSource.setTrustStorePassword를 호출해야 합니다. 자세한 내용은 [SQLServerDataSource.getReference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

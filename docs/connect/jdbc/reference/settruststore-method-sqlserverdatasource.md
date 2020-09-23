---
description: setTrustStore 메서드(SQLServerDataSource)
title: setTrustStore 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setTrustStore Method (SQLServerDataSource)
apilocation:
- setTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: bab5485d-4547-426c-adbe-44e2b5702d1d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be69bd333d0264e4833dd053979f1e3dfe5a9b39
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88354929"
---
# <a name="settruststore-method-sqlserverdatasource"></a>setTrustStore 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  인증서 trustStore 파일의 경로(파일 이름 포함)를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setTrustStore(java.lang.String trustStore)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *trustStore*  
  
 인증서 trustStore 파일의 경로(파일 이름 포함)가 들어 있는 **문자열**입니다.  
  
## <a name="remarks"></a>설명  
 trustStore 속성이 지정되어 있지 않거나 null로 설정되어 있으면 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 트러스트 관리자 팩터리의 조회 규칙에 따라 사용할 인증서 저장소를 결정합니다. 기본 SunX509 TrustManagerFactory에서는 다음 위치의 순서에 따라 트러스트 자료를 찾으려고 합니다.  
  
-   1. "javax.net.ssl.trustStore" JVM(Java Virtual Machine) 시스템 속성에 지정된 파일  
  
-   2. "\<java-home>/lib/security/jssecacerts" 파일  
  
-   3. "\<java-home>/lib/security/cacerts" 파일  
  
 자세한 내용은 Sun Microsystems 웹 사이트에서 SunX509 TrustManager 인터페이스 설명서를 참조하십시오.  
  
 trustStore 속성이 문자열이나 빈 문자열 “”로 설정되어 있으면, 드라이버는 해당 값으로 trustStore 파일을 찾아서 서버 TLS/SSL 인증서의 유효성을 검사합니다.  
  
 trustStorePassword 속성은 trustStore 속성과 함께 지정할 수 있으며 해당 값을 사용하여 trustStore 파일을 엽니다. 자세한 내용은 [setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

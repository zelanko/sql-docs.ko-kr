---
title: JDBC 드라이버 응용 프로그램 보안 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 90724ec6-a9cb-43ef-903e-793f89410bc0
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11330ade60084a5e3995b5acf565d26f3b4da62b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="securing-jdbc-driver-applications"></a>JDBC 드라이버 응용 프로그램 보안
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  향상 된 보안은 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 응용 프로그램에서는 일반적인 코딩 실수를 피하는 것입니다. 데이터에 액세스하는 응용 프로그램에는 공격자가 주요한 데이터를 검색, 조작 또는 파괴하는 데 사용할 수 있는 수많은 잠재적인 오류 지점이 있습니다. 응용 프로그램의 디자인 단계 동안 위협 모델링 프로세스에서 결과 배포에 이르기까지, 그리고 진행 중인 유지 관리에서 지속적으로 모든 보안 측면을 이해하고 있어야 합니다.  
  
 이 섹션의 항목에서는 연결 문자열, 사용자 입력의 유효성 검사 및 일반 응용 프로그램 보안을 포함한 일반적인 보안 문제에 대해 설명해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[연결 문자열 보안](../../connect/jdbc/securing-connection-strings.md)|데이터 원본에 연결하는 데 사용되는 정보를 보호하는 기술에 대해 설명합니다.|  
|[사용자 입력 유효성 검사](../../connect/jdbc/validating-user-input.md)|사용자 입력의 유효성을 검사하는 기술에 대해 설명합니다.|  
|[응용 프로그램 보안](../../connect/jdbc/application-security.md)|Java 정책 권한을 사용하여 JDBC 드라이버 응용 프로그램의 보안을 유지하는 방법에 대해 설명합니다.|  
|[SSL 암호화 사용](../../connect/jdbc/using-ssl-encryption.md)|보안 통신 채널을 설정 하는 방법을 설명는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Secure Sockets Layer (SSL)를 사용 하 여 데이터베이스입니다.|  
|[FIPS 모드](../../connect/jdbc/fips-mode.md)|FIPS 규격 모드에서 JDBC 드라이버를 사용 하는 방법을 설명 합니다.| 
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

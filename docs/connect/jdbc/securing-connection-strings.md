---
title: "연결 문자열 보안 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 69ce8557-5260-4ea4-81b8-d0c5481f0868
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 588166b41e7a66a442b1b5b49fbdcaf0d6d13320
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="securing-connection-strings"></a>연결 문자열 보안
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  데이터 원본에 대한 액세스를 보호하는 일은 응용 프로그램의 보안을 유지하는 가장 중요한 목표 중 하나입니다. 데이터 원본에 대한 액세스를 제한하려면 사용자 ID, 암호 및 데이터 원본 이름 같은 연결 정보의 보안을 유지하도록 사전에 주의를 기울여야 합니다. 사용자 ID와 암호를 소스 코드에서처럼 일반 텍스트로 저장하면 심각한 보안 문제가 발생합니다. 사용자 ID와 암호 정보가 외부 원본에 들어 있는 컴파일된 버전의 코드를 제공하는 경우에도 컴파일된 코드가 디스어셈블되어 사용자 ID와 암호가 노출될 수 있습니다. 따라서 사용자 ID 및 암호 같은 중요한 정보가 코드에 들어 있어서는 안 됩니다.  
  
 또한 응용 프로그램 소스 코드에 암호와 연결 URL을 함께 저장하지 않도록 합니다. 대신 액세스가 제한된 별도의 파일에 암호를 저장하는 방법을 고려합니다. 이러한 파일에 대한 액세스 권한은 응용 프로그램에서 실행하는 컨텍스트에 부여될 수 있습니다.  
  
 또 다른 접근 방식은 암호화된 암호를 파일에 저장하는 것입니다. 이때 키를 특정 위치에 저장할 필요가 없으며 사용자의 암호에서 파생되지 않은 암호화 API를 사용해야 합니다. 예를 들어, 인증서 기반의 공개/개인 키 쌍을 사용하는 방법을 고려하거나 두 당사자가 키 계약 프로토콜(Diffie-Hellman 알고리즘)을 사용하여 비밀 키를 전송하지 않고 암호화를 위해 동일한 비밀 키를 생성하는 접근 방식을 사용할 수 있을 것입니다.  
  
 사용자 ID와 암호를 제공하는 사용자처럼 외부 원본에서 연결 문자열 정보를 가져오는 경우 원본 입력의 유효성을 검사하여 입력이 올바른 형식을 따르며 연결에 영향을 주는 추가 매개 변수가 들어 있지 않은지 확인해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 응용 프로그램 보안](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  

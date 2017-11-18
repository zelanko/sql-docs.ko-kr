---
title: "setIntegratedSecurity 메서드 (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.setIntegratedSecurity
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c968ee4-b041-424a-bf69-cc2c4a4f51c6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b0480212d2216f66d917debcd7565093d89c9d78
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setintegratedsecurity-method-sqlserverdatasource"></a>setIntegratedSecurity 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  설정 된 **부울** integratedSecurity 속성이 사용 되는지 여부를 나타내는 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setIntegratedSecurity(boolean enable)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *사용 하도록 설정*  
  
 **true 이면** integratedSecurity가 사용 되는 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>주의  
 로 설정 "**true**" 증명에서 Windows 자격 증명을 사용 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 응용 프로그램의 사용자를 인증 합니다. 경우 "**true**", [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 컴퓨터 또는 네트워크 로그온 시 이미 제공 된 자격 증명에 대 한 로컬 컴퓨터 자격 증명 캐시를 검색 합니다. 경우 "**false**", 사용자 이름 및 암호를 제공 해야 합니다.  
  
> [!NOTE]  
>  이 속성은 에서만 지원 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Windows 운영 체제.  
  
 통합된 인증을 사용 하는 방법에 대 한 자세한 내용은 참조 [연결 URL 작성](../../../connect/jdbc/building-the-connection-url.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

